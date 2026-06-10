## Entity: [EntityName]
**Table:** table_name
**Description:** [What this entity represents]

### Fields
| Field | Type | Constraints | Notes |
|---|---|---|---|
| id | UUID | PK, auto-generated | |

### Relationships
- [EntityName] has many [Other] (1:N)
- [EntityName] belongs to [Other] (N:1)

### Indexes
- field_name (btree) — reason for index

### Business Rules
- [Domain rules enforced at DB level]
