# SEO change log

Changes made in Webflow to resolve SE Ranking site-audit issues. All were published to yegcustomwindows.ca and www.yegcustomwindows.ca.

## 2026-11-26: /thanks page audit issues

- **Multiple H1 tags:** the hidden catalogue section on /thanks had a CMS card heading set to H1 (style `heading-style-h5`). Changed it to H3, so "We will give you a call shortly!" is the only H1.
- **External link to 3XX:** the "Caliph Digital" credit link in `footer_component` pointed to `caliphdigital.ca` (no scheme), which redirects. Changed it to `https://www.caliphdigital.ca/`. Site-wide, as the footer is on every page.
- **Internal link missing anchor:** the navbar and footer logo links (`navbar_logo-link`, `footer_logo-link`) to the homepage contained only an image with no alt text. Added `aria-label="YEG Custom Windows home"` to both and gave the logo image alt text (below).
- **Alt text missing:**
  - Logo asset (`ChatGPT Image Sep 14, 2026, 09_13_15 AM 1.webp`): alt "YEG Custom Windows logo". Site-wide, wherever the image inherits asset alt.
  - Hero background `window-condensation-in-winter.webp`: alt "Condensation on a window in winter".
  - Meta Pixel `<noscript>` tracking image in the /thanks head code: added `alt=""` (decorative 1x1 pixel).
- **Restored noindex:** the /thanks head code no longer had the `<meta name="robots" content="noindex, follow">` added on 2026-11-19 (it was replaced when the Meta Pixel was added). Re-added it above the pixel code.
- **No inbound links:** expected for a form confirmation page that is noindexed; no change.

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
