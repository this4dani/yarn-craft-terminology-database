# Yarn Craft Terminology Database API Documentation

## Overview

The Yarn Craft Terminology Database provides free, open access to yarn craft terminology across 8 fiber arts disciplines. All data is served as static JSON files via GitHub's CDN — no authentication required.

## Base URL

```
https://raw.githubusercontent.com/this4dani/yarn-craft-terminology-database/main/data/
```

## Data Files

| File | Description |
|------|-------------|
| `terms.json` | Core terminology records |
| `craft_types.json` | 8 yarn craft disciplines |
| `categories.json` | 25 term categories |
| `sources.json` | Authority references |
| `tags.json` | Searchable tags |
| `term_tags.json` | Junction: terms ↔ tags |
| `term_sources.json` | Junction: terms ↔ sources |

Schema definitions: `schemas/term.schema.json` ([JSON Schema draft-07](https://json-schema.org/))

## Data Structures

### Term Object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `term_id` | string | Yes | Unique identifier (e.g., "SC") |
| `entry_type` | string | Yes | One of: stitch, technique, tool, material, pattern-term |
| `craft_type` | string | Yes | References `craft_types.craft_id` |
| `category` | string | Yes | References `categories.category_id` |
| `name_us` | string | Yes | Full US English name |
| `name_uk` | string/null | No | Full UK English name if different |
| `abbrev_us` | string/null | No | US abbreviation |
| `abbrev_uk` | string/null | No | UK abbreviation |
| `description` | string | Yes | Original definition |
| `instruction` | string/null | No | Step-by-step instructions |
| `difficulty` | integer | Yes | Skill level: 1 (beginner) to 5 (expert) |
| `time_to_learn` | string/null | No | Estimated learning time |
| `best_for` | string/null | No | Common project applications |
| `common_mistakes` | string/null | No | Frequent errors |
| `pro_tips` | string/null | No | Expert guidance |
| `hook_sizes` | string/null | No | Recommended hook or needle sizes |
| `left_handed_note` | string/null | No | Left-handed adaptation guidance |
| `tags` | array | No | Array of tag IDs |
| `sources` | array | No | Array of source IDs |
| `status` | string | Yes | One of: active, draft, review |

### Craft Type Object

| Field | Type | Description |
|-------|------|-------------|
| `craft_id` | string | Unique identifier (e.g., "crochet") |
| `name` | string | Display name |
| `description` | string | Brief description of the discipline |

### Category Object

| Field | Type | Description |
|-------|------|-------------|
| `category_id` | string | Unique identifier (e.g., "basic") |
| `name` | string | Display name |
| `description` | string | Category description |

### Source Object

| Field | Type | Description |
|-------|------|-------------|
| `source_id` | string | Unique identifier (e.g., "cyc") |
| `name` | string | Full source name |
| `description` | string | Source description |

### Tag Object

| Field | Type | Description |
|-------|------|-------------|
| `tag_id` | string | Unique identifier (e.g., "basic") |
| `name` | string | Display name |

### Junction Tables

**term_tags.json** — Links terms to tags:

| Field | Type | Description |
|-------|------|-------------|
| `term_id` | string | References `terms.term_id` |
| `tag_id` | string | References `tags.tag_id` |

**term_sources.json** — Links terms to authority sources:

| Field | Type | Description |
|-------|------|-------------|
| `term_id` | string | References `terms.term_id` |
| `source_id` | string | References `sources.source_id` |

## Usage Examples

### JavaScript — Fetch All Terms

```javascript
const response = await fetch(
  'https://raw.githubusercontent.com/this4dani/yarn-craft-terminology-database/main/data/terms.json'
);
const terms = await response.json();

// Find a specific term
const sc = terms.find(t => t.term_id === 'SC');
console.log(sc.name_us); // "Single Crochet"
console.log(sc.name_uk); // "Double Crochet"
```

### JavaScript — Filter by Category

```javascript
const terms = await fetch(
  'https://raw.githubusercontent.com/this4dani/yarn-craft-terminology-database/main/data/terms.json'
).then(r => r.json());

const basicStitches = terms.filter(t => t.category === 'basic');
```

### JavaScript — Search Implementation

```javascript
function searchTerms(query, terms) {
  const q = query.toLowerCase();
  return terms.filter(term =>
    term.name_us.toLowerCase().includes(q) ||
    (term.name_uk && term.name_uk.toLowerCase().includes(q)) ||
    term.tags.some(tag => tag.toLowerCase().includes(q))
  );
}
```

### Python

```python
import requests

url = "https://raw.githubusercontent.com/this4dani/yarn-craft-terminology-database/main/data/terms.json"
terms = requests.get(url).json()

# Filter by entry type
stitches = [t for t in terms if t['entry_type'] == 'stitch']
```

### cURL

```bash
# Fetch all terms
curl -s https://raw.githubusercontent.com/this4dani/yarn-craft-terminology-database/main/data/terms.json | jq '.[0]'

# Fetch craft types
curl -s https://raw.githubusercontent.com/this4dani/yarn-craft-terminology-database/main/data/craft_types.json | jq '.'
```

## Rate Limits and Usage

**No authentication required.** This is a public dataset hosted on GitHub.

- GitHub raw file serving limits apply
- Cache responses for production use — data does not change frequently
- For heavy usage, download JSON files locally

## Best Practices

- Use `terms.json` for full term data
- Cache responses — files update infrequently
- Handle errors gracefully for network issues
- Use the `status` field to filter for `active` terms in production

## Support and Updates

- **Issues:** Report via [GitHub Issues](https://github.com/this4dani/yarn-craft-terminology-database/issues)
- **Schema:** Validated against `schemas/term.schema.json`
- **Updates:** Monitor the repository for changes

## License

This data is provided under **CC BY-SA 4.0**.

**Attribution:** When using this data, please credit the Yarn Craft Terminology Database.

**Repository:** [github.com/this4dani/yarn-craft-terminology-database](https://github.com/this4dani/yarn-craft-terminology-database)
