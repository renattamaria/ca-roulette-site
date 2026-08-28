# Combat Achievement Roulette

A single self-contained `index.html`. You import the JSON written by the
**CA Roulette Export** RuneLite plugin, and it spins a random Combat Achievement
you haven't done yet.

**Live:** <https://ca-roulette.vercel.app>

- All 655 CA tasks are baked in (id, boss, name, description, type, tier,
  community completion %), sourced from the
  [OSRS Wiki](https://oldschool.runescape.wiki/w/Combat_Achievements/All_tasks)
  and joined to your export by the stable task id.
- Your progress is stored in your browser (`localStorage`). Nothing is uploaded.
- Filters: tier, task type, boss/activity, and "hide tasks I can't start yet"
  (checks your quests and stats from the export against a curated
  boss-requirement table).

## Hosting

Deployed on Vercel from this repo — every `git push` to `master` redeploys
automatically. It's pure static HTML, no build step. Works the same on GitHub
Pages, Netlify, Cloudflare Pages, or opened locally.

## Editing

Everything is in `index.html`.

- **Task data:** the first `<script>` block, `window.CA_DATA`. Generated from the
  wiki's "All tasks" table (`data/ca_wiki.json` is the intermediate dump). After a
  game update, re-scrape that table and rebuild the
  `[id, monsterIdx, name, desc, typeIdx, tierIdx, comp]` rows.
- **Boss requirements** for the "can I attempt this" filter: the `REQS` object in
  the second `<script>` — `{ "Boss Name": { quests: [...], skills: { Slayer: 95 } } }`.
  Deliberately conservative (only well-known hard gates); add entries as needed.

## The plugin

The companion RuneLite plugin lives at
<https://github.com/renattamaria/ca-roulette-export>. It reads Combat Achievement
completion, skills, quests and items from the game client and writes the JSON this
site imports. Install it from the RuneLite Plugin Hub ("CA Roulette Export").
