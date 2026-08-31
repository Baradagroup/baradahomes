# baradahomes.com

Static site. One HTML file plus images. No build step, no framework, no database.

## Files

```
index.html              the whole site (58 KB)
assets/                 28 property photos (webp)
og-image.jpg            link preview card for WhatsApp / Facebook / X
favicon.svg             browser tab icon
icon-192.png            fallback tab icon
apple-touch-icon.png    iOS home screen icon
robots.txt              search engine instructions
sitemap.xml             search engine index
_headers                cache rules (Cloudflare Pages / Netlify read this)
```

## Before it goes live — fill these in

Open `index.html`, find `const SETTINGS` (around line 640).

```js
const SETTINGS = {
  whatsapp: "66000000000",          // real number, digits only, country code first, no + and no spaces
  email:    "hello@baradahomes.com",
  instagram:"https://instagram.com/",   // add the handle
  facebook: ""                          // leave empty to hide the icon
};
```

The WhatsApp number is currently a placeholder. Every "chat with us" button on the
site is dead until it's replaced.

## Editing the site later

Everything editable lives in two objects at the top of the `<script>` block:

- `SETTINGS` — contact details and social links
- `PROPERTIES` — the property listings: names, locations, bedrooms, prices,
  descriptions, and which images each one uses

Both are plain JavaScript objects. Change a value, save, done.

**Adding a new property photo:**
1. Drop the `.webp` file into `assets/` (name it something like `r15.webp`)
2. Add a line to the `IMG` object: `"r15": "assets/r15.webp",`
3. Reference `"r15"` in that property's `gallery` array

Photos should be roughly square (1240×1240) for apartments, portrait or landscape
(930×1240 / 1240×930) for villas. Export as WebP at ~80% quality to keep them
under 100 KB each.

**Text is bilingual.** Anywhere you see `{en: "...", ar: "..."}` you need to fill
in both languages, otherwise the Arabic toggle shows blanks.

## Deploying an update

If the site is on Cloudflare Pages connected to GitHub: edit the file in GitHub
(pencil icon → make the change → Commit changes) and the live site rebuilds
itself in about 30 seconds. Nothing else to do.

To roll back a bad change: GitHub → Commits → open the last good one → Revert.

## Notes

- Fonts (Outfit, IBM Plex Sans Arabic) load from Google Fonts. The site still
  works without them, it just falls back to system fonts.
- The Arabic version is a toggle on the same URL, not a separate page. If a
  proper `/ar/` page is ever built, the `hreflang` tags need to come back.
- There is no contact form and no server. All enquiries route to WhatsApp and
  email, which means there is nothing to hack and nothing to maintain.
