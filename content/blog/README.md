# Blog posts

Source copy for blog posts on yegcustomwindows.ca. Each file holds the publishing details (SEO title, meta description, keywords, slug, schema) in its front matter, followed by the article.

| Date | Post | Live URL |
|---|---|---|
| 2026-11-24 | [Why Is There Frost or Ice on the Inside of My Windows?](frost-inside-windows-edmonton.md) | /frost-inside-windows-edmonton |
| 2026-11-26 | [Condensation Between Window Panes](condensation-between-window-panes-edmonton.md) | /condensation-between-window-panes-edmonton |

## How they are built in Webflow

- Each post is a static page copied from the About page (navbar, header, quote banner, footer), with the article inserted after the header.
- Article styles are the `blog-*` classes (`blog-section`, `blog-article`, `blog-h2`, `blog-h3`, `blog-p`, `blog-list`, `blog-li`, `blog-link`, `blog-table-wrap`, `blog-table`, `blog-th`, `blog-td`). Reuse them for new posts.
- Each page has Article + FAQPage JSON-LD in its page settings.
- The links between the two posts use page links, so they keep working if the pages move.

## To do

- Move both pages into a `/blog` folder (Webflow can only create folders from the Designer), then add 301 redirects from the current URLs and update the JSON-LD `url` values.
- The planned `/window-replacement` page doesn't exist. The frost post links to /services/window-door-installation-and-repairs instead.
- There is no blog index page or navbar link yet, so the posts are reachable only by direct link and the sitemap.
