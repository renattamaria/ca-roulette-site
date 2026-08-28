# Combat Achievement Roulette (website)

Single self-contained `index.html`. Loads the JSON written by the **CA Roulette Export**
RuneLite plugin, then spins a random Combat Achievement you haven't done yet.

- All 655 CA tasks are baked in (id, boss, name, description, type, tier, community completion %),
  sourced from the [OSRS Wiki](https://oldschool.runescape.wiki/w/Combat_Achievements/All_tasks)
  and joined to your export by the stable task id.
- Your progress is stored in the browser (`localStorage`). Nothing is uploaded.
- Filters: tier, task type, boss/activity, and "hide tasks I can't start yet" (checks your
  quests and stats from the export against a curated boss-requirement table).

## Where it's hosted

Published as a Claude Artifact:
<https://claude.ai/code/artifact/d4d301f7-102d-4c36-a7da-6bceb8129535>

It starts private. Use the **Share** menu on that page to give friends a link.

## Self-hosting (optional, e.g. Vercel)

`index.html` is fully static and standalone — no build step, no server code.

**Vercel:**
1. Put `index.html` in a folder on its own (this folder works).
2. `npx vercel` in that folder, or drag the folder onto the Vercel dashboard.
3. It serves `index.html` at the root. Done.

**Anything else:** GitHub Pages, Netlify drop, Cloudflare Pages, or just open the file
locally — all work, because it's one HTML file with everything inlined.

## Editing the task data

The dataset lives in the first `<script>` block as `window.CA_DATA`. It was generated from
the wiki's "All tasks" table. To refresh it after a game update, re-scrape that table and
rebuild the same `[id, monsterIdx, name, desc, typeIdx, tierIdx, comp]` rows.

The boss-requirement table for the "can I attempt this" filter is the `REQS` object in the
second `<script>` — plain `{ "Boss Name": { quests: [...], skills: { Slayer: 95 } } }`.
It's deliberately conservative (only well-known hard gates); add entries as needed.
