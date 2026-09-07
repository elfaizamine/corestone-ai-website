# CoreStone AI — website

A 5-page marketing site built with [Astro](https://astro.build/). Static output, no
database, no server. Home · Services · Case study · About · Contact.

---

## Run it locally

You need [Node.js](https://nodejs.org/) 20.3+ (22 LTS recommended).

```bash
npm install
npm run dev
```

Open <http://localhost:4321>. Edits reload automatically.

To preview the real production build:

```bash
npm run build      # outputs to ./dist
npm run preview
```

---

## Things you'll want to change

| What | Where |
|------|-------|
| **Calendly link** (currently a placeholder) | `src/consts.ts` → `CALENDLY_URL` |
| Contact email | `src/consts.ts` → `CONTACT_EMAIL` |
| Nav items, site name, tagline | `src/consts.ts` |
| Page copy | `src/pages/*.astro` |
| Colors, type scale, spacing | `src/styles/global.css` (top of file, `:root`) |
| Favicon | `public/favicon.svg` |
| Social share image | `public/og.svg` — see note below |

### Demo video placeholders

Two "DEMO VIDEO — COMING SOON" blocks are ready for you to drop a video into:

- Home hero — `src/pages/index.astro`, the `<DemoPlaceholder />` inside `.hero__media`
- Case study — `src/pages/case-study.astro`, the `<DemoPlaceholder />` in the "Demo" section

Replace `<DemoPlaceholder ... />` with your embed, e.g.:

```html
<div style="aspect-ratio: 16 / 9; border-radius: 12px; overflow: hidden;">
  <iframe src="https://www.youtube.com/embed/VIDEO_ID"
    title="CoreStone AI demo call" loading="lazy"
    style="width: 100%; height: 100%; border: 0;" allowfullscreen></iframe>
</div>
```

### Social share image (`og.svg`)

`public/og.svg` is a placeholder. Most platforms (LinkedIn especially) render
**PNG/JPG** OG images more reliably than SVG. Before launch:

1. Export a `1200×630` **PNG** and save it as `public/og.png`.
2. In `src/layouts/BaseLayout.astro`, change `const ogImage = new URL('/og.svg', …)`
   to `'/og.png'`.

---

## The contact form

The Contact page form uses **Netlify Forms**. It only works once the site is
deployed to Netlify — locally it will just navigate to `/thank-you`.

- Submissions appear in your Netlify dashboard under **Forms → contact**.
- Set up an email notification: Netlify dashboard → **Forms → Settings & notifications**.
- A hidden honeypot field (`bot-field`) filters basic spam.

If you move off Netlify later, swap the form's `action`/attributes for another
provider (e.g. Formspree) in `src/pages/contact.astro`.

---

## Deploy for free

### Option A — Netlify (recommended, needed for the contact form)

**From the dashboard (easiest):**

1. Push this folder to a GitHub/GitLab repo.
2. In Netlify: **Add new site → Import an existing project**, pick the repo.
3. Netlify reads `netlify.toml` automatically:
   - Build command: `npm run build`
   - Publish directory: `dist`
4. Deploy. Add your domain under **Domain management** (point `corestoneai.com`'s
   DNS at Netlify, or let Netlify manage DNS).

**From the CLI instead:**

```bash
npm i -g netlify-cli
netlify deploy --build          # preview URL
netlify deploy --build --prod   # go live
```

### Option B — Vercel

1. Push to a Git repo.
2. In Vercel: **Add New → Project**, import the repo.
3. Framework preset: **Astro** (auto-detected). Build command `npm run build`,
   output directory `dist`. Deploy.

⚠️ On Vercel the Netlify Forms integration won't work — you'd need to switch the
contact form to Formspree or Vercel's own form handling.

---

## Project structure

```
public/            static files served as-is (favicon, og image, robots.txt)
src/
  consts.ts        site-wide config: name, email, Calendly URL, nav
  styles/
    global.css     the whole design system — tokens, base, components
  layouts/
    BaseLayout.astro   <head>, meta/OG tags, header + footer wrapper
  components/
    Header.astro       sticky nav + mobile menu
    Footer.astro
    Section.astro      section wrapper with white / tint background
    Stat.astro         large numeric stat element
    DemoPlaceholder.astro
    CtaBand.astro      the repeated "Book a 20-minute call" block
  pages/
    index.astro        Home
    services.astro      Services / how it works
    case-study.astro
    about.astro
    contact.astro
    thank-you.astro     shown after form submit (noindex)
    404.astro
astro.config.mjs   site URL, sitemap
netlify.toml       build config for Netlify
```

## Notes

- Fonts (Inter Tight + Inter) are self-hosted via `@fontsource-variable` — no
  Google Fonts request, no layout shift.
- One load animation only: the hero fades in. It's disabled automatically for
  visitors with "reduce motion" turned on. No scroll-triggered animation anywhere.
- The whole site is one shared design system; every section uses the same spacing
  rhythm (`--section-space` in `global.css`).
