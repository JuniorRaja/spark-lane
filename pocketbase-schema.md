# PocketBase Collection Schema

## Collection: `brew_ideas`

### Fields

| Field | Type | Required | Options |
|-------|------|----------|---------|
| `title` | text | Yes | min: 1, max: 200 |
| `description` | editor | No | - |
| `status` | select | Yes | Options: `raw`, `brewing`, `validated`, `mvp`, `shipped`<br>Default: `raw` |
| `validation` | json | No | - |
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
  "name": "brew_ideas",
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
    },
    {
      "name": "validation",
      "type": "json",
      "required": false
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
- `validation` field stores AI validation data as JSON (score, metrics, insights)
- Auth rules assume user authentication enabled
- Adjust rules if you want public/anonymous access

### Schema Changes from Previous Version:
- **Added**: `validation` field (JSON type) to store AI-powered validation data including:
  - `score`: Validation score (0-100)
  - `marketSize`: Market size assessment
  - `competition`: Competition level
  - `feasibility`: Technical feasibility
  - `insights`: Array of insight strings
  - `metrics`: Object with marketSize, competitors, difficulty values
