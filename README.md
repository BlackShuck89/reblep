# reFloofgens

**An independently maintained enhancement userscript for [floofgens.net](https://floofgens.net/), derived from re6AI and re621.**

reFloofgens continues the original [re6AI](https://github.com/re621/re6ai) adaptation of bitWolfy's [re621](https://github.com/re621/re621.Legacy) userscript. The current target, **floofgens.net**, is the site launched by the original e6AI team in November 2026.

Both the userscript and repository are now named **reFloofgens**, at [BlackShuck89/refloofgens](https://github.com/BlackShuck89/refloofgens). Earlier releases under the reBlep and re6AI Personal names are preserved for historical reference; they are **not** Floofgens builds.

This is independent GPLv3 derivative software, not an official re621, re6AI, e6AI or Floofgens release. The original authors and contributors retain their attribution.

## Current status

**Floofgens beta source: v1.3.0-beta.1.** The port has been integrated into [master](https://github.com/BlackShuck89/refloofgens/tree/master) after initial maintainer browser testing. **A Floofgens release has not yet been published.** The previous release (reBlep v1.2.0-beta.8) targets the former site.

- [Master branch](https://github.com/BlackShuck89/refloofgens/tree/master): current Floofgens source and reviewed fixes.
- [Releases](https://github.com/BlackShuck89/refloofgens/releases): currently historical builds; no Floofgens release tag yet.
- [Pull requests](https://github.com/BlackShuck89/refloofgens/pulls): review and browser-testing progress.

The code is based on the re621/re6AI 1.x architecture. Useful re621 2.x features are ported selectively rather than claiming full parity.

## Features and goals

The inherited modules include subscriptions and notifications, custom and bulk downloads, post viewing, search and thumbnail enhancements, tag utilities, keyboard shortcuts and appearance settings. Individual modules may still need Floofgens-specific fixes.

Our goals are to:

- Keep those features compatible with Floofgens without calling the previous site or retired e6AI hosts.
- Preserve historical releases without mixing account IDs, subscriptions or settings between services.
- Maintain independent project identity, issue tracking, release downloads and GPLv3 attribution.
- Improve compatibility through automated fixtures and live browser testing.

## Testing installation

1. Install [Tampermonkey](https://www.tampermonkey.net/) or [Violentmonkey](https://violentmonkey.github.io/).
2. From [the Floofgens port PR](https://github.com/BlackShuck89/refloofgens/pull/7), download `script.user.js` from a successful **Development checks** workflow artifact. This is a **test build**, not a published release.
3. Confirm the installed script is **reFloofgens 1.3.0-beta.1** and matches **https://floofgens.net/** only.
4. Disable old reBlep installations and follow the [test checklist](docs/FLOOFGENS_PORT.md).

**New installation identity:** This port uses its own userscript `@namespace` (https://github.com/BlackShuck89/refloofgens/floofgens.net), so previous site's GM storage and numeric subscription IDs are not silently reused. Back up settings before switching. Do not import old subscription IDs without verifying their meaning.

Floofgens says e6AI posts and tags were transferred, but user accounts were not. Use Floofgens' own account creation and data-import process where available. This script does not automatically migrate historical favorites, archives or settings. Past prereleases have pinned update URLs and will not automatically upgrade to this port.

## Building from source

Install [Bun](https://bun.sh/), then run:

```sh
git clone https://github.com/BlackShuck89/refloofgens.git
cd refloofgens
git checkout master
bun install --frozen-lockfile
bun run compile-typescript:prod
bun run compile-sass:prod
bun run compose-userscript:prod
```

The output is `build/userscript/script.user.js`. Automated checks build and exercise API response fixtures; additional browser testing remains welcome. The inherited browser-extension build is not a supported release target.

## Origins, licensing and credits

This is a **derivative work**, not a clean-room rewrite:

| Project or contributor | Contribution |
| --- | --- |
| [bitWolfy](https://github.com/bitWolfy) | Original author of re621 — e621 Reimagined |
| [re621 Legacy](https://github.com/re621/re621.Legacy) | Original 1.x enhancement codebase |
| [re6AI](https://github.com/re621/re6ai) | Direct source of the initial e6AI adaptation |
| Sindrake | Credited contributor to re6AI |
| Earlopain | Credited contributor to re621 and re6AI |
| [BlackShuck89](https://github.com/BlackShuck89) | Independent maintainer of the continuation and port |

**License:** GNU General Public License version 3 (GPLv3). See [LICENSE](LICENSE). Independent maintenance does not transfer exclusive ownership of upstream work or remove upstream notices.

Please report issues to the [project's issue tracker](https://github.com/BlackShuck89/refloofgens/issues). Changes are reviewed and integrated manually; this repository does not automatically synchronize with upstream.
