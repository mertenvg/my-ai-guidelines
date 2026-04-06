# SQL and Data Access Patterns

---

## Prepared Statements

- Define all SQL as constants, prepared once at startup. Never construct SQL
  dynamically at request time.
- Never concatenate or interpolate user input into SQL strings.
- Use parameterized queries exclusively.

### SQL Constant Naming

Unexported, prefixed with `q`, named for the operation:

```go
const (
    qInsertUser = `INSERT INTO users (...) VALUES (...)`
    qGetByID    = `SELECT ... FROM users WHERE id = :id`
    qUpdateUser = `UPDATE users SET ... WHERE id = :id RETURNING ...`
)
```

### Parameter Structs

Unexported, defined alongside the query that uses them:

```go
type idParams struct {
    ID string `db:"id"`
}
```

### Store Initialization

`NewStore` should panic on preparation failure — these are always programmer
errors, not runtime conditions:

```go
func NewStore(db *sqlx.DB) *Store {
    stmts, err := statements.PrepareNamed(db, qInsertUser, qGetByID)
    if err != nil {
        panic(err)
    }
    return &Store{stmts: stmts}
}
```

---

## Partial Updates

Use `COALESCE` for partial updates — never build queries dynamically:

```sql
UPDATE drivers SET
    license_number = COALESCE(:license_number, license_number),
    vehicle_make   = COALESCE(:vehicle_make, vehicle_make),
    updated_at = NOW()
WHERE id = :id
RETURNING *
```

When all update fields are nil, skip the UPDATE and fall back to a read:

```go
func (s *Store) Update(ctx context.Context, id string, p UpdateParams) (*Model, error) {
    if p.FieldA == nil && p.FieldB == nil {
        return s.GetByID(ctx, id)
    }
    // run update query
}
```

---

## Optional Filters

Use static sentinel values instead of dynamic query building:

```sql
-- string filter: empty string = skip
WHERE (:customer_id = '' OR customer_id::text = :customer_id)

-- nullable filter: NULL = skip
WHERE (:status::text IS NULL OR status = :status)

-- boolean toggle
WHERE (NOT :unresolved_only::boolean OR resolved_at IS NULL)
```

---

## No-Parameter Queries

Pass `struct{}{}` as the argument to queries with no parameters:

```go
s.stmts.Get(qGetAll).SelectContext(ctx, &results, struct{}{})
```

---

## Migrations

- Each service owns its own schema and migrations.
- Migrations live alongside the service: `cmd/<service>/migrations/`.
- Migrations are applied at startup or via a dedicated migration tool.
- Never modify an existing migration that has been applied — create a new one.
