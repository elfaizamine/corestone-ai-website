# Company logos (About page — "Track record")

The About page currently shows each prior company as its **name in text**. To
show a real logo instead:

1. Get the company's official logo from its own press / brand / media kit
   (not a random image search — those are usually outdated or low-res).
   Prefer a single-color or black SVG; the site renders it at 22px tall and
   slightly dimmed to sit calmly next to the text.

   Suggested filenames:
   - `forbes.svg`
   - `legacy-south.svg`
   - `ship-angel.svg`
   - `pubt.svg`
   - `artefact.svg`
   - `inwi.svg`

2. In `src/pages/about.astro`, add `logo` to that company in the `experience`
   array:
   ```js
   { company: 'Forbes', logo: '/logos/forbes.svg', note: '…' },
   ```

Any company without a `logo` value keeps showing its name as text — so you can
add logos one at a time, and it's fine to leave some as text permanently.

Only use logos of companies you actually worked for/with, shown unmodified, to
describe that prior work. Don't recolor, stretch, or redraw them.
