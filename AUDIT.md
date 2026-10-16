# Dependabot audit: jekyll-feed 0.17.0 → 0.18.0

**PR:** [#3](https://github.com/rillus/rillus.github.io/pull/3) (`dependabot/bundler/jekyll-feed-0.18.0`)  
**Reviewed:** 2026-10-16  
**Verdict:** **Safe to merge** — no breaking changes identified; upgrade includes a security fix.

## Changelog review

Source: [jekyll-feed `History.markdown` v0.18.0](https://github.com/jekyll/jekyll-feed/blob/v0.18.0/History.markdown) and [release v0.18.0](https://github.com/jekyll/jekyll-feed/releases/tag/v0.18.0).

| Category | Notes |
|----------|--------|
| **Breaking changes** | None documented between 0.17.0 and 0.18.0. |
| **Security** | Escapes `xml:lang` values and CDATA terminators in the feed ([GHSA-3gx8-pqcm-38hw](https://github.com/advisories/GHSA-3gx8-pqcm-38hw), #396). **Recommended upgrade.** |
| **Features** | Optional `feed.icon` and `feed.logo` in `_config.yml` (#412). Not used by this site. |
| **Compatibility** | Still requires `jekyll (>= 3.7, < 5.0)` — compatible with this repo’s Jekyll 4.4.1. |

## Site impact

- **Gemfile:** `jekyll-feed` constraint updated to `~> 0.18` (Dependabot also aligned the constraint with the locked version).
- **Usage:** Plugin is loaded via the `:jekyll_plugins` group; `_includes/head.html` uses `{%- feed_meta -%}`. No custom `feed:` settings in `_config.yml` — default Atom feed at `/feed.xml`.
- **Behaviour change expected:** Stricter XML escaping in the generated feed (security hardening only).

## Verification

| Check | Result |
|-------|--------|
| Repository test suite | **None** — Jekyll blog with no automated tests or CI workflow. |
| `bundle exec jekyll build` | **Passed** (Ruby 4.0.7, Bundler 2.4.5). Log: `Jekyll Feed: Generating feed for posts`. |
| Output | `_site/feed.xml` generated (855 lines); valid Atom structure with post entries. |
| GitHub PR checks | **None reported** on the Dependabot branch. |

Pre-existing build warnings (unrelated to this bump): Liquid syntax warning in `_posts/2025-02-12-react-hooks.md`; Sass deprecation warnings from the Minima theme.

## Recommendation

Merge the Dependabot PR. The bump is a minor release with a worthwhile security fix and no configuration changes required for this site.
