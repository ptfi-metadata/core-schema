# Contributing

The golden rule: **only edit the two CSV files in `data/`.** Everything else
(`terms.js`, `palette.css`) is generated and will be overwritten — never edit
those by hand, and never edit `index.html`, `app.js` or `styles.css` to change
the schema or colours.

## Edit a variable

Open `data/schema.csv` (Excel → "Save As CSV", or any text editor) and edit the
row. Columns:

| Column | Notes |
|---|---|
| `element_id` | snake_case key, e.g. `collection_country` |
| `name` | human label shown on the card |
| `group` | `Study`, `Specimen`, `Sample`, or `Aliquot` |
| `obligation` | `Required` / `Conditional` / `Optional` / `Curator-assigned` |
| `datatype`, `occurrence`, `format` | value type, single/multiple, format hint |
| `value_scheme` | standard for the **value** (ISO 8601, Unit Ontology, FoodOn…). The link is added automatically. |
| `allowed_values`, `examples` | use `;` to separate multiple entries |
| `maps_to` | external **property** it equals: `dwc:…` or `dcterms:…`. Leave blank if the term is PTFI-original. |
| `match_type` | `exact` or `close` (only when `maps_to` is filled) |
| `definition`, `curation_note` | documentation |

To **add** a variable, add a new row. To **remove** one, delete its row.

## Add or recolour a group

Edit `data/groups.csv`. Columns: `id, name, role, blurb, fill, accent, ink,
order`. Change `fill` / `accent` / `ink` (hex) to recolour a group; the page
colours, the top bar and the grid all follow automatically. Add a row to add a
group.

## Publish

- **Just push** to `main`. A GitHub Action runs `build/build.py`, regenerates
  `terms.js` + `palette.css`, and deploys the site to GitHub Pages. Nothing is
  committed back — the generated files are not stored in the repo.

## Preview locally

```bash
python build/build.py        # generate terms.js + palette.css locally
python3 -m http.server       # open http://localhost:8000
```

(`terms.js` / `palette.css` are git-ignored and generated on deploy; build them
locally just for preview. Opening `index.html` with `file://` won't load the data.)

## One-time repo settings

- Settings → Pages → Source → **GitHub Actions**.
  (No "read and write" Actions permission is needed — deployment uses the
  least-privilege Pages permission instead.)
