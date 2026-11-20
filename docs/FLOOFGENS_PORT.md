# Floofgens port checklist — reFloofgens 1.3.0 Beta 1

## Status

**Merged source, not yet released.** This port moves the enhancement userscript to [floofgens.net](https://floofgens.net/). After initial maintainer browser testing, it has been integrated into the default `master` branch. No Floofgens release tag has been published.

Floofgens is operated by the original e6AI team. Its [official API documentation](https://floofgens.net/help/api) describes Danbooru-compatible endpoints and a hard limit of two API calls per second. The live post API currently returns `artist`, `copyright` and `contributor` tag groups. The script retains a **one-request-per-second** queue and its `_client` query parameter.

## Changes

- `@match` and extension content scripts now target **https://floofgens.net/**; the former site's domain is not registered.
- The displayed name and package identity are `reFloofgens`, with a fresh `@namespace` ending in `/floofgens.net`. This separates saved userscript settings and subscriptions from previous-site IDs.
- API calls remain relative to the current site's origin. Navigation, search, forums, post history and archive comments use Floofgens or relative URLs.
- Media fallback origin discovery accepts `floofgens.net` and its subdomains, while preferring actual `file.url`, `preview.url` and `sample.url` from API responses.
- Current Floofgens `artist` / `copyright` / `contributor` tag groups are normalized. Historical e6AI `director` / `franchise` groups remain readable.
- Historical releases and notes remain available for provenance but are no longer current installation instructions.

## Safe migration

**Do not blindly import site-specific state.** Although [Floofgens announced](https://e6ai.net/news_updates) that e6AI posts and tags were transferred, user accounts were not. Old site or Blep numeric IDs may refer to unrelated people/posts. A different `@namespace` prevents a userscript manager from automatically mixing GM state, but users should still back up their own preferences before disabling prior installs.

Existing beta releases use pinned update URLs, so they will **not** silently become the Floofgens script. The source version and update URLs point to a future `v1.3.0-beta.1` release; until such a tag is published, use a CI test artifact or build from source.

## Validation

### Automated

1. Run `node scripts/test-floofgens-target.js`.
2. Run `bun run scripts/test-floofgens-api-fixture.mjs`.
3. Run `bun run eslint` and `bun run typescript`, then the userscript build. Verify generated `@name`, `@namespace`, `@match` and update/download links.
4. Confirm no runtime source includes the former domain or the retired static CDN.

### Browser (required before publishing)

1. Install a successful CI build into Firefox/Tampermonkey or a comparable userscript manager. Disable the old script. Confirm it activates only on Floofgens and not the previous site.
2. Open post search, infinite scrolling and a single post. Check module initialization, media loading and the search fallback if API calls fail.
3. Verify preview/sample URLs from JSON and real site markup. A live API response uses `static1.floofgens.net`; check that origin discovery handles it.
4. Check tag category suggestions (artist, copyright, general, species, character), autocomplete and tag aliases. Confirm the site still exposes relevant DOM selectors.
5. Test the native post download menu and search downloads; confirm generated filenames survive Firefox download handling.
6. Test favorites, optional auto-upvote, pools and post sets on a new account. Do not modify other people's data.
7. Test subscriptions and notifications with **new** Floofgens IDs. Restart and ensure storage is isolated from old-site subscriptions.
8. Check requests for `_client` and ~1 request/second. Verify no requests go to the previous domain.
9. Check keyboard shortcuts, mobile and browser variations. Disable broken modules and document limitations before any release.

## Limitations

Static and API-shape checks do not establish full visual or interaction compatibility. Live session browser tests and user account flows are not yet signed off. Treat this as a prerelease port.

The project is independent GPLv3 derivative software based on re6AI/re621. Original contributors and upstream licenses are preserved in [README](../README.md) and [LICENSE](../LICENSE).

