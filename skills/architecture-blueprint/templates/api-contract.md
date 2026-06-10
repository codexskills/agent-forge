## API Endpoint: [METHOD] [/path]

**Purpose:** [What this endpoint does]
**Auth:** Required / Optional / None
**Permissions:** [Who can call this]

### Request
Headers:
  Authorization: Bearer {token}

Path params:
  - paramName: type — description

Query params:
  - paramName: type (default: X) — description

Body (JSON):
  - fieldName: type (required/optional) — description, constraints

### Response

**Success [STATUS CODE]:**
```json
{
  "data": {}
}
```

**Error responses:**
| Status | Code | When |
|---|---|---|
| 400 | VALIDATION_ERROR | Request body fails schema validation |
| 401 | UNAUTHORIZED | No valid session / token expired |
| 403 | FORBIDDEN | Authenticated but no permission |
| 404 | NOT_FOUND | Resource does not exist |
| 409 | CONFLICT | Duplicate resource |
| 429 | RATE_LIMITED | Too many requests |
| 500 | INTERNAL_ERROR | Unexpected server error |
