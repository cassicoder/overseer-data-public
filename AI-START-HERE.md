# AI START HERE — overseer-data-public

Public data repo Claude writes to. Lets Claude log into Overseer dashboard sections (currently: nutrition) without touching the private sync repo.

## Files
- `nutrition.json` — meal logs by date (Overseer Dashboard fallback source)

## Workflow for Claude
1. `git clone https://<PAT>@github.com/cassicoder/overseer-data-public.git`
2. Read JSON, modify the right date's array, write back.
3. Commit + push. Dashboard reads via `fetch()` on next load.

## Workflow for the dashboard
- Section pages fetch from `https://cassicoder.github.io/overseer-data-public/<file>.json`
- Local storage wins. Public fills gaps.

## Cross-repo
- `cassicoder/overseer-dashboard` — UI (consumer)
- `cassicoder/overseer-data` — private sync (phone-side state)
- `cassicoder/nutrition` — legacy nutrition iframe (Obsidian)
