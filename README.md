# Yarn Craft Terminology Database

The first comprehensive, open, API-accessible database of yarn craft terminology. Starting from a crochet foundation and expanding across all fiber arts disciplines — knitting, weaving, embroidery, and more.

## Key Features

- **265+ Terms:** Basic stitches (SC, DC, HDC) to advanced techniques (cables, colorwork, C2C, graphgans), plus US/UK translations and community slang
- **Rich Data Structure:** Each term includes ID, US/UK names, category, difficulty, description, tags, estimated learning time, and best use cases
- **Quiz System:** 50+ auto-generated multiple-choice questions with difficulty levels and US vs. UK terminology challenges
- **Automated Updates:** Data maintained in a master Google Sheets database — community-driven, quality-controlled, and version-tracked

## Quick Start

```javascript
// Fetch all terms
const response = await fetch('https://raw.githubusercontent.com/this4dani/yarn-craft-terminology-database/main/terms.json');
const data = await response.json();
console.log(`Loaded ${data.meta.total_terms} terms!`);
```

## API Endpoints

| Endpoint | Description | Size | Use Case |
|----------|------------|------|----------|
| `terms.json` | All terms (lightweight) | ~50KB | General lookups, apps |
| `glossary.json` | Complete API with search index | ~80KB | Advanced features |
| `categories.json` | Terms grouped by category | ~60KB | Filtering, menus |
| `quiz.json` | Quiz questions & answers | ~30KB | Educational apps |
| `api-info.json` | API metadata | ~2KB | Version info |

**Base URL:** `https://raw.githubusercontent.com/this4dani/yarn-craft-terminology-database/main/`

## Data Structure

```json
{
  "id": "SC",
  "name_us": "Single Crochet",
  "name_uk": "Double Crochet",
  "category": "Basic Stitches",
  "difficulty": "1",
  "description": "The most basic crochet stitch...",
  "tags": ["basic", "fundamental", "beginner"],
  "time_to_learn": "5 minutes",
  "best_for": "Tight fabric, amigurumi"
}
```

## Use Cases

- **Websites:** Term tooltips within patterns
- **Mobile Apps:** Offline-capable glossaries
- **Educational Platforms:** Quiz questions and learning tools
- **WordPress Plugins:** Shortcodes for on-demand term definitions
- **Quiz & Badge Systems:** Categorized challenges (Stitch Master, Global Crocheter, Technique Expert)

## Examples

### Simple Term Lookup
```javascript
const terms = await fetch('https://raw.githubusercontent.com/this4dani/yarn-craft-terminology-database/main/terms.json')
  .then(r => r.json());

const singleCrochet = terms.data.find(term => term.id === 'SC');
console.log(singleCrochet.name_us); // "Single Crochet"
console.log(singleCrochet.name_uk); // "Double Crochet"
```

### Category Filtering
```javascript
const categories = await fetch('https://raw.githubusercontent.com/this4dani/yarn-craft-terminology-database/main/categories.json')
  .then(r => r.json());

const basicStitches = categories.data['Basic Stitches'];
```

### Search Implementation
```javascript
function searchTerms(query, terms) {
    return terms.filter(term =>
        term.name_us.toLowerCase().includes(query.toLowerCase()) ||
        term.name_uk.toLowerCase().includes(query.toLowerCase()) ||
        term.tags.some(tag => tag.toLowerCase().includes(query.toLowerCase()))
    );
}
```

## API Stats

- **265+ Terms** — Most comprehensive free yarn craft terminology API
- **Global Coverage** — US, UK, and international terminology
- **Mobile Ready** — Lightweight JSON, CORS enabled
- **Fast & Reliable** — Served via GitHub CDN with 99.9% uptime

## Contributing

We welcome contributions to improve the database!

**Data Improvements:**
- Submit corrections or suggest new terms
- Report US/UK terminology differences
- Help expand into knitting, weaving, and embroidery terminology

**Technical Contributions:**
- Improve quiz generation
- Add new data formats
- Enhance API documentation

## Who's Using This API

[Add your project here by submitting a PR!]

## License

CC BY-SA 4.0 — Free to use, share, and adapt with attribution. Share-alike required for derivative works.
