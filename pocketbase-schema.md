# PocketBase Collection Schema

## Collection: `ideas`

### Fieldsgit commit -m "first commit"

| Field | Type | Required | Options |
|-------|------|----------|---------|
| `title` | text | Yes | min: 1, max: 200 |
| `description` | editor | No | - |
| `status` | select | Yes | Options: `raw`, `brewing`, `validated`, `mvp`, `shipped`<br>Default: `raw` |
| `created` | date | Auto | Auto-generated |
| `updated` | date | Auto | Auto-updated |

### API Rules (adjust based on your auth needs)

**List/View:**
- Auth required (or public if you want no login)

**Create:**
- Auth required

**Update:**
- Auth required

**Delete:**
- Auth required

### Example JSON for manual import:

```json
{
  "name": "ideas",
  "type": "base",
  "schema": [
    {
      "name": "title",
      "type": "text",
      "required": true,
      "options": {
        "min": 1,
        "max": 200
      }
    },
    {
      "name": "description",
      "type": "editor",
      "required": false
    },
    {
      "name": "status",
      "type": "select",
      "required": true,
      "options": {
        "maxSelect": 1,
        "values": [
          "raw",
          "brewing",
          "validated",
          "mvp",
          "shipped"
        ]
      }
    }
  ],
  "indexes": [],
  "listRule": "@request.auth.id != ''",
  "viewRule": "@request.auth.id != ''",
  "createRule": "@request.auth.id != ''",
  "updateRule": "@request.auth.id != ''",
  "deleteRule": "@request.auth.id != ''"
}
```

### Notes:
- `status` tracks idea maturity lifecycle
- `editor` type for description allows rich text
- Auth rules assume user authentication enabled
- Adjust rules if you want public/anonymous access
