# Anikoto for Sora / Shirox

Two modules are included: **Anikoto (SUB)** and **Anikoto (DUB)**. Each has its own JSON manifest and a self-contained JavaScript file. You may install either or both.

## Install

These files are ready to host, but are not published. The supplied manifests contain `https://YOUR-HOST/` placeholders; they will not work until configured.

1. Upload this folder to a public GitHub repository, or another static file host.
2. Open `configure.html` locally in your browser. Paste the **raw folder URL** where you uploaded the files, for example `https://raw.githubusercontent.com/YOUR-USERNAME/YOUR-REPOSITORY/main/anikoto/`.
3. Download the configured Sub and/or Dub JSON manifest. Replace the corresponding JSON file in your repository with that download. The JavaScript files need no edits.
4. In Sora or Shirox, open **Settings → Modules → Add (+)** and paste the raw URL of `anikoto-sub.json` or `anikoto-dub.json`.

You can also configure manually: change only `scriptUrl` in each JSON manifest to the public raw URL of its matching `.js` file. Use raw file links, not GitHub `/blob/` page links. The ZIP itself is not an import URL.

## Features

- Search with posters and titles, filtered by available Sub or Dub episodes.
- Descriptions, alternate names, and air dates.
- Ordered episode lists, including long-running series.
- MegaPlay HLS streams with HD-1 and Vidstream fallback choices.
- English subtitles for Sub, with compatibility fields for differing host versions.
- No external extraction service, browser extension, npm installation, or API key needed.

Search returns the site's first result page, up to 30 matches. Narrow the search if your title is missing. Quality depends on the source; the manifest's 1080p label is not a guarantee. Downloads are not advertised because download behavior has not been tested.

## Validation

Validated against the live website on October 2, 2026 in a bare JavaScript VM without DOM, Web Crypto, Node imports, or browser globals inside the module. Both Sora-style fetch interfaces were exercised.

| Check | Sub | Dub |
|---|---:|---:|
| Search results for `naruto` | 26 | 18 |
| One Piece episodes | 1,180 | 1,155 |
| Episode 1 stream choices | 2 | 2 |
| Master and media playlists | HTTP 200, valid HLS | HTTP 200, valid HLS |
| English subtitle | HTTP 200, valid WebVTT | Omitted |

Native playback and import in Sora/Shirox have **not** been tested here. Playlist validation does not establish successful full-episode playback. Host app versions and future site changes may affect compatibility.

## Troubleshooting

- **Module will not import:** open the manifest and script raw URLs in a browser. Both must return file text, with no login or HTML preview page. Confirm that `YOUR-HOST` has been replaced.
- **Empty results:** try a shorter title and check that you installed the desired Sub/Dub variant.
- **Playback link expired:** reopen the episode to get fresh source links. Player tokens are short-lived; saved stream URLs are not permanent.
- **One server fails:** try the other stream choice. Current extraction supports `megaplay.buzz`; a new player host will require an update.
- **All streams stop working:** inspect the app logs for `Anikoto:`. The player protocol, public player constants, or domain may have changed. Reinstall an updated module after replacing its hosted files.

## Files and attribution

- `anikoto-sub.json` / `anikoto-sub.js`: Sub module.
- `anikoto-dub.json` / `anikoto-dub.js`: Dub module.
- `configure.html`: offline manifest setup helper. It sends no network requests.
- `CRYPTOJS-LICENSE.txt`: MIT license for CryptoJS 4.2.0, bundled in each script.

The custom module logic is provided under the MIT license in `LICENSE.txt`. This is an unofficial module, unaffiliated with Anikoto, Sora, or Shirox.

References: [Sora module schema](https://sora.jm26.net/docs/modules/json-schema.html), [Sora distribution instructions](https://sora.jm26.net/docs/modules/distributing.html), [Sora fetch runtime](https://github.com/cranci1/Sora/blob/main/Sora/Utlis%20%26%20Misc/Extensions/JavaScriptCore%2BExtensions.swift), [Shirox](https://github.com/xibrox/Shirox), [CryptoJS](https://github.com/brix/crypto-js).
