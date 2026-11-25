# SEO change log

Changes made in Webflow to resolve SE Ranking site-audit issues. All were published to yegcustomwindows.ca and www.yegcustomwindows.ca.

## 2026-11-20: Multiple H1 tags

The homepage, /promo, /catalogue and every /locations/* page had more than one H1.

- Cause: the product card title (class `heading-style-h5`) inside the catalogue collection list was set to H1, so each page got an extra H1 for every product shown.
- Fix: changed that heading from H1 to H2 on **Home**, **Promo**, **Catalogue** and the **Locations Template**. The class is unchanged, so it looks the same. Each page now has only its hero H1.
- Checked **Services Template** (already H3), **About** and **Our Work** (no such heading); no changes needed.

### Edmonton location typos

The Edmonton CMS item (Locations collection) had typos in its headings, which also fed its meta description:

| Field | Before | After |
|---|---|---|
| H1 Heading | Window & Door Services in Edmontoon | Window & Door Services in Edmonton |
| H2 Heading | Edmon Window & Door Service Companyoon | Edmonton Window & Door Service Company |

Published to yegcustomwindows.ca and www.yegcustomwindows.ca.

## 2026-11-20: Slow page loading and Speed Index

SE Ranking flagged slow loading on /locations/fort-saskatchewan and a poor Speed Index on the homepage.

- Cause: the site's images were large, uncompressed PNG/JPG files (about 13 MB in total). The hero image alone (`Hero.png`) was 1.4 MB and appears on the homepage and every location page.
- Fix 1: converted 19 PNG/JPG assets to WebP with Webflow's asset compression: 12.98 MB down to 1.29 MB (90% smaller). The conversion replaced the files in place, so the PNG/JPG originals are no longer stored in Webflow. `Hero.png` went from 1.39 MB to 27 KB.
  - Not converted: `fav-icon.png` and `web-clip.png`, which stay PNG for browser and device icon support. SVG files were already small.
- Fix 2: the hero image (`header_background-image`) on the **Home** page and **Locations Template** now has `loading="eager"` and `fetchpriority="high"`, so the browser loads it first instead of lazy-loading it.
- Published to yegcustomwindows.ca and www.yegcustomwindows.ca.

## 2026-11-19: Internal links to 3XX redirect pages

Every page linked to `https://yegcustomwindows.ca/` (non-www), which 301-redirects to `https://www.yegcustomwindows.ca/`.

- Cause: the **Offers** link in the `navbar_component` (shown on every page) was an absolute URL, `https://yegcustomwindows.ca/#offers`.
- Fix: changed it to the relative link `/#offers`, so it always stays on the current domain with no redirect.
- Checked the homepage, footer, services grid and CTA components; no other absolute non-www links found.

## 2026-11-19: Titles and meta descriptions

### Title too long (service pages)

Service page titles come from the **Services Template** (CMS collection page). Its SEO title changed:

- Before: `{Name} - Edmonton WIndow & Door Installation Company`
- After: `{Name} | YEG Custom Windows`

| Page | New title | Chars |
|---|---|---|
| /services/window-door-installation-and-repairs | Window & Door Installation and Repairs \| YEG Custom Windows | 59 |
| /services/cracked-foggy-glass-replacement | Cracked & Foggy Glass Replacement \| YEG Custom Windows | 54 |
| /services/basement-egress-windows | Basement Egress Windows \| YEG Custom Windows | 44 |

### Title too short (static pages)

| Page | Before | After |
|---|---|---|
| /about | About | About Us \| YEG Custom Windows Edmonton |
| /our-work | Our Work | Our Work \| Window & Door Projects in Edmonton |
| /catalogue | Catalogue | Window, Door & Glass Catalogue \| YEG Custom Windows |
| /contact | Contact | Contact Us \| Free Window & Door Quotes in Edmonton |
| /thanks | Thanks | Thank You \| YEG Custom Windows |

### Duplicate description

/promo and /thanks reused the homepage description. Each now has its own:

- **/promo**: Save 33% on cracked and foggy glass repairs in Edmonton. We replace just the glass, not the whole window. Claim your offer and book a free quote today.
- **/thanks**: Thanks for contacting YEG Custom Windows. We've received your request and will be in touch shortly about your window, door or glass project.

### Description too long

The service meta description is built as `{H2 Heading}. {Short Description}`. For /services/window-door-installation-and-repairs (167 chars), the CMS item's Short Description was shortened:

- Before: New installs, replacements, and repairs on existing windows and doors — done to code, done clean.
- After: New installs, replacements and repairs — done to code, done clean.

Resulting description: 136 chars.

## 2026-11-19: Orphan pages (/promo, /thanks)

Both pages had no incoming internal links but were listed in the sitemap. /thanks is a form confirmation page and /promo is a paid-ad landing page, so they should not be indexed.

- Added `<meta name="robots" content="noindex, follow">` to the page head code of /promo and /thanks.
- **To do (manual):** exclude /promo and /thanks from the sitemap in Webflow page settings (the API token lacked permission). Consider excluding /style-guide too.

## 2026-11-25: First two blog posts published

| Page | SEO title | Schema |
|---|---|---|
| /frost-inside-windows-edmonton | Frost on the Inside of Windows? Edmonton Guide | Article + FAQPage |
| /condensation-between-window-panes-edmonton | Foggy Window Repair Edmonton: Condensation Between Panes | Article + FAQPage |

- Built as static pages copied from /about, with the article in new `blog-*` classes. Source copy is in [content/blog](../content/blog/README.md).
- Published at root URLs because a `/blog` folder needs the Webflow Designer open. **To do:** move them into `/blog` and add 301 redirects.
- `/window-replacement` doesn't exist, so that link points to /services/window-door-installation-and-repairs.
