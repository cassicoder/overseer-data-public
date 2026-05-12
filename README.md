# overseer-data-public

Public data files Claude writes to. Read by `cassicoder/overseer-dashboard` as a fallback when localStorage is empty for a given day.

**Schema:** one file per dashboard section. Each file is a flat JSON object keyed appropriately for that section.

- `nutrition.json` — `{ days: { "YYYY-MM-DD": [ {name, cal, p, c, f, meal} ] }, version: 1 }`

## Rules for Claude

1. Always read the file first, merge new entries into the correct date array, then write back.
2. `meal` is one of: `breakfast`, `lunch`, `dinner`, `snacks`.
3. Do not delete past entries. Append only, unless Isaac explicitly says delete/replace.
4. Commit message format: `Log YYYY-MM-DD: <short summary>`.

## Rules for the dashboard

1. On load, for each visible day, if localStorage `nutrition:YYYY-MM-DD` is empty, fetch from this repo and populate.
2. Never overwrite localStorage entries with public data — local wins. Public only fills gaps.
3. Cache-bust with a query string if needed.
