# Deploy

Static site. Nothing to build at deploy time — everything is generated.

## Option A — €0 forever (recommended to start)

**GitHub Pages, user site.** Repo name must be exactly `cyril-enko-business.github.io`
(all lowercase — the username has capitals, the repo name may not). Drop these
files in the root and enable Pages in Settings. Live at
`https://cyril-enko-business.github.io/`, HTTPS included, indexable, no cost ever.

The canonical tags and sitemap in this build already point there. If you ever
move to a custom domain, change `DOMAIN` in `build.py` and rebuild.

Use a *user* site (repo named `<username>.github.io`) rather than a project
site, so the pages sit at the domain root. Internal links are relative, so a
project subpath also works, but the root is cleaner.

Then set `DOMAIN` in `build.py` to your Pages URL and rebuild, so the canonical
tags and sitemap match where the site actually lives. A mismatched canonical is
the one mistake that quietly stops a page being indexed.

Netlify (`<project>.netlify.app`) works identically and is also indexed.

**Why free hosting is defensible here:** publishing the repo publicly means
anyone can verify every figure against the sources. For a tool about someone's
tax and social obligations, from an author nobody knows, an auditable source
tree is a stronger trust signal than a €15 domain.

## Option B — a custom domain, later

A `.be` costs roughly €10–15/year. Worth buying *after* the tool shows anyone
uses it, not before. Moving is cheap: point the domain at the same host, update
`DOMAIN`, rebuild, and file a change of address in Search Console.

## After it is live

- Google Search Console: verify, submit `/sitemap.xml`, check the hreflang
  pairs are recognised (nl-BE / fr-BE / x-default).
- Bing Webmaster Tools: same. It feeds several AI answer engines.
- Rich Results Test: confirm the FAQ structured data validates.

## Files
```
index.html    language chooser, x-default
nl/index.html Dutch page
fr/index.html French page
robots.txt
sitemap.xml   with hreflang alternates per URL
```

## Regenerating
`build.py` renders both languages from `strings.json`, `css.css` and `app.js`.
Change a figure in one place, rebuild, redeploy. When the 2027 barema's are
published, only `strings.json` and the constants at the top of `app.js` need
editing.
