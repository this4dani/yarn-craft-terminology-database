# Yarn Craft Terminology Database

The first comprehensive, open, API-accessible database of yarn craft terminology. Starting from a crochet foundation and expanding across all fiber arts disciplines — knitting, weaving, embroidery, and more.

## Project Plan

The complete project documentation — sustainability plan, grant framework, board recruitment, feasibility research, financial projections, and outreach strategy:

**[YCTD Project Plan](https://docs.google.com/document/d/1hrBfMFKMJB5VUqZEWdi-CVV3I0Ft3GlMfUwlJGWKYQQ/edit?usp=sharing)**

## Key Features

- **Multi-discipline coverage:** 8 yarn craft disciplines — crochet, knitting, weaving, embroidery, tapestry, macramé, lace-making, and Tunisian crochet
- **Rich data structure:** Each term includes US/UK names, abbreviations, entry type, craft type, category, difficulty level, instructions, and expert tips
- **Relational database design:** 7 interconnected tables following a documented JSON Schema (draft-07) with a 3-phase migration path toward PostgreSQL + API
- **Authority-sourced:** Definitions cross-referenced against Craft Yarn Council, CGOA, TKGA, and JIS standards
- **Open and extensible:** CC BY-SA 4.0 licensed, community-driven contributions welcome

## Database Structure

All data lives in the `data/` directory. Each file represents one table in the database:

| File | Description |
|------|-------------|
| `terms.json` | Core terminology records with definitions, instructions, and metadata |
| `craft_types.json` | 8 yarn craft disciplines |
| `categories.json` | 25 term categories (basic, shaping, lace, tunisian, etc.) |
| `sources.json` | Authority references (CYC, CGOA, TKGA, JIS, YCTD original) |
| `tags.json` | Searchable tags for filtering and discovery |
| `term_tags.json` | Junction table linking terms to tags |
| `term_sources.json` | Junction table linking terms to authority sources |

Schema definitions are in `schemas/term.schema.json` ([JSON Schema draft-07](https://json-schema.org/)).

## Term Data Structure

```json
{
  "term_id": "SC",
  "entry_type": "stitch",
  "craft_type": "crochet",
  "category": "basic",
  "name_us": "Single Crochet",
  "name_uk": "Double Crochet",
  "abbrev_us": "sc",
  "abbrev_uk": "dc",
  "description": "The most basic crochet stitch...",
  "instruction": "Insert hook, yarn over, pull through...",
  "difficulty": 1,
  "tags": ["basic", "common", "beginner-friendly"],
  "sources": ["cyc", "cgoa"],
  "status": "active"
}
```

## Quick Start

```javascript
// Fetch all terms
const response = await fetch(
  'https://raw.githubusercontent.com/this4dani/yarn-craft-terminology-database/main/data/terms.json'
);
const terms = await response.json();

// Find a term
const sc = terms.find(t => t.term_id === 'SC');
console.log(sc.name_us); // "Single Crochet"
console.log(sc.name_uk); // "Double Crochet"
```

**Base URL:** `https://raw.githubusercontent.com/this4dani/yarn-craft-terminology-database/main/data/`

## Use Cases

- **Websites:** Term tooltips within patterns
- **Mobile apps:** Offline-capable glossaries
- **Educational platforms:** Learning tools with term definitions
- **WordPress plugins:** Shortcodes for on-demand term definitions
- **Downstream API products:** Pattern adjustment tools, learning systems, and more

## Contributing

We welcome contributions to improve the database! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

- Submit corrections or suggest new terms
- Report US/UK terminology differences
- Help expand into knitting, weaving, and embroidery terminology
- Improve documentation and API examples

## Who's Using This Database

[Add your project here by submitting a PR!]

## License

**CC BY-SA 4.0** — Free to use, share, and adapt with attribution. Share-alike required for derivative works.
