<p align="center">
  <img src="Design/AppIcon-1024.png" alt="YT Music icon" width="112" />
</p>

# YT Music for macOS

**Your music, at home on your Mac.**

An unofficial native macOS client for YouTube Music, with a SwiftUI interface, translucent surfaces, smooth transitions and artwork-inspired colours. Browse your library, play music and keep track of discoveries without leaving a familiar Mac interface.

**Not affiliated with, sponsored by or endorsed by Google or YouTube.** YouTube and YouTube Music names, content and associated trademarks belong to their respective owners.

| Current version | Supported Macs | Minimum macOS | Distribution |
| --- | --- | --- | --- |
| 1.0 (build 1) | Apple silicon (M-series) | macOS 27.0 | DMG / ZIP; ad-hoc signed, unnotarized |

This is a native interface backed by YouTube Music's online service. Login and audio playback use an embedded WebKit browser; browsing and library screens are native. It is not an independent audio service and does not download music for offline listening.

## Contents

- [Screenshots](#screenshots)
- [Features](#features)
- [What stays local and what changes your account](#what-stays-local-and-what-changes-your-account)
- [Installation](#installation)
- [Using the app](#using-the-app)
- [Privacy, storage and cache](#privacy-storage-and-cache)
- [Development](#development)
- [Checks and testing](#checks-and-testing)
- [Packaging releases](#packaging-releases)
- [Architecture](#architecture)
- [Limitations and troubleshooting](#limitations-and-troubleshooting)
- [Contributing and reporting issues](#contributing-and-reporting-issues)
- [License and acknowledgements](#license-and-acknowledgements)

## Screenshots

<p align="center">
  <img src="Screenshots/YT0.png" width="48%" alt="YT Music screenshot 1" />
  <img src="Screenshots/YT1.png" width="48%" alt="YT Music screenshot 2" />
</p>
<p align="center">
  <img src="Screenshots/YT2.png" width="48%" alt="YT Music screenshot 3" />
  <img src="Screenshots/YT3.png" width="48%" alt="YT Music screenshot 4" />
</p>
<p align="center">
  <img src="Screenshots/YT4.png" width="48%" alt="YT Music screenshot 5" />
</p>

## Features

### Browse and discover

- Home recommendations, Explore, new releases, charts, moods and genres.
- Search songs, artists, albums, videos, playlists and other available results.
- Library playlists, songs, liked music, albums, artists, subscriptions and history.
- Podcasts, saved podcasts, channels and uploads when exposed for your account.
- Playlist cards and sidebar navigation, plus song, artist and album destinations.
- **Search in playlist** to filter the playlist content already loaded in the app.

### Playback made for the Mac

- Song and playlist playback, previous/next, seeking, time display and app-level volume/mute.
- Shuffle, repeat song/queue, continuous playback and Start Mix / Radio from a song.
- Queue view and current-track highlighting with animated playback indicators.
- Bottom Now Playing bar and an expanded player with a blurred backdrop and growing transition.
- Song actions in the expanded player: Go to song, Go to artist, Go to album and Add to playlist.
- Waveform menu bar mini-player, macOS Now Playing integration and media-key support.
- Lyrics with source credits when available; currently plain text rather than synchronised lines.
- High-resolution artwork where available, with fallback to usable originals.
- Hover highlights, gentle lift/glow effects and support for Reduce Motion in animated UI.

### Library actions

- Read a song's like status and like/unlike it.
- Add songs to writable playlists, search destinations, or create a private playlist in the picker.
- Check whether a song is already in the destination before adding it.
- Remove the exact song entry from its current playlist when the service exposes removal rights.

### Personal listening tools

Open the **sparkle / Listening tools** menu in the top toolbar.

| Tool | What it does |
| --- | --- |
| **Hold my place** | Save the current song, elapsed position, queue, playing/paused state, shuffle and repeat. Return later; a paused saved song remains paused. |
| **Playlist Doctor** | Read full playlists to find exact duplicates and entries flagged unavailable/restricted. Compare two playlists for shared songs. Review selected extra copies before confirming removal. |
| **Radio breadcrumbs** | Remember a radio's starting song and the songs actually played in this app. Repeated player reports do not create duplicate visits. |
| **Discovery tray** | Bookmark interesting songs locally, then play/open them or explicitly add them to an online playlist later. |
| **Artwork atmosphere** | Sample colours from the current cover and softly tint the main background and expanded Now Playing panel, blending into the next palette as songs change. |

**Artwork atmosphere** is a background mood effect: artwork and controls stay readable. Enable/disable it and adjust intensity in **Listening tools → Artwork atmosphere** or **Settings**. The default is subtle; increase intensity for a stronger tint. Missing/unusable artwork falls back to the app's usual colours. Reduce Motion disables animated colour transitions. This visual preference does not affect audio or your online account.

Tool bounds:

- Held queues retain up to **1,000 tracks**, keeping a window around the current song for larger queues. Finite playlists are read in full before saving; radio saves currently available recommendations.
- Radio history keeps **12 trails**, up to **100 songs per trail**; the discovery tray keeps **80 songs**.
- Playlist Doctor compares exact video IDs, not similar titles or different uploads/remixes. Read-only entries remain findings. Removal is limited to **100 selected extra entries per operation**, with a fresh check to protect the last copy.

## What stays local and what changes your account

“Local” describes where a save or preference changes. It does **not** mean the operation works offline: playlist scans, music, artwork and lyrics still require internet access.

| Action | Effect |
| --- | --- |
| Hold/restore a listening place | Saves a local snapshot; restoring uses normal online playback. Does not create an online playlist. |
| Radio breadcrumbs, discovery bookmarks and clearing trails | Changes this Mac's local listening data. Bookmarking does not like a song or add it to a playlist. |
| Atmosphere, app volume/mute and presentation preferences | Changes the local app experience. App volume does not change macOS system volume. |
| Search in playlist | Filters already-loaded content; does not change the online playlist. |
| Playlist Doctor scan/comparison | Reads online playlist information; no playlist changes during scanning. |
| Clear cache | Removes temporary local data while preserving login and saved listening tools. |
| Like/unlike | Changes the song's YouTube Music rating. |
| Add to playlist / create playlist | Changes your online library; new playlists created here are private. |
| Remove from current playlist / confirmed Doctor removal | Removes the selected entries from the online playlist. |
| Streaming, radio and playback controls | Operate this app's player; normal listening may update YouTube Music history and recommendations according to your account settings. |

Online account changes can appear on other devices. Local listening tools and preferences do not sync to other devices.

## Installation

You need an Apple silicon Mac running **macOS 27 or later**, an internet connection and your own YouTube Music account. Available content and features depend on the service, subscription, region and account permissions.

If prebuilt packages have been published, find them in the repository's **Releases** section:

1. Open the DMG and drag **YT Music** to **Applications**. For ZIP, extract it and move the app to Applications.
2. Eject the disk image, then open the app from Applications.
3. Sign in through the app's account window. The session stays saved for later launches.

Current packages are **ad-hoc signed and unnotarized**, not signed with a Developer ID certificate. macOS may block the first launch. If you trust the copy you downloaded, try opening it, then use **System Settings → Privacy & Security → Open Anyway**. See [Apple's guidance](https://support.apple.com/en-us/102445). There is no need to disable Gatekeeper globally.


## Using the app

- Click a playlist's card or sidebar name to open it; use its Play button to start playback.
- Click the **bottom-player artwork** to open the current Song view.
- Click **empty space in the bottom Now Playing bar** to expand the player. Collapse with Escape, the down arrow or a click outside the panel.
- Use a song's **…** menu for available navigation and playlist actions. Missing artist/album destinations are disabled rather than guessed.
- Open the **waveform menu bar item** for the mini-player.
- Open **YT Music → About YT Music** for the description, full feature summary, local/account explanations and installed version/build in a resizable native window.

| Shortcut | Action |
| --- | --- |
| Space | Play/pause |
| Command–Right Arrow | Next song |
| Command–Left Arrow | Previous song |
| Command–comma | Settings |
| Escape | Collapse expanded Now Playing |

## Privacy, storage and cache

- Google sign-in takes place in the app's WebKit account window. This project does not require a Chrome extension, an external browser callback, a Google Cloud OAuth client or a developer-supplied API secret for the current login flow.
- The WebKit profile retains the login session. Native service requests use the relevant session cookies and client context; treat this profile as sensitive account data.
- Held places, radio trails and discoveries are stored as local JSON under the app's Application Support directory in `YTMusic/Listening`. In a sandboxed build, macOS resolves this inside the app container.
- Local listening files are separated using a hash of the available stable account identity. If only an ambiguous account slot is available, tools use memory for that session. Hashing the filename is **not encryption**; song titles and listening data in the file remain local readable data.
- Listening snapshots do not store credentials. Saved rating/removal-permission hints are discarded so stale local data cannot stand in for current account state. Save/read failures are surfaced in the tools UI.
- Preferences such as volume and atmosphere use local app preferences.
- Artwork has a bounded in-memory cache; WebKit also maintains temporary streaming/site caches. Cleanup runs at launch and every six hours when paused. **Settings → Cache & storage → Clear cache** waits for a pause if requested during playback.
- Cleanup removes the allowed temporary cache types and artwork cache; cookies, account storage, held places, trails, discoveries and preferences are preserved. It is not a sign-out or complete data-erasure feature.
- Requests go to YouTube/Google services and artwork hosts. Using the app is not private listening or an alternative to the service's own account/privacy settings.

To uninstall, quit and move the app to Trash. This does not delete your YouTube Music account or online playlists; local app/container data may remain.

## Development

### Requirements

- An Apple silicon Mac and **Xcode 27.1** with the macOS 27 SDK, matching the currently verified toolchain.
- Swift is supplied by Xcode; the project currently uses **Swift 5 language mode** with default MainActor isolation.
- **Node.js** for JavaScript bridge checks. **Python 3** is used by the optional all-source Swift check runner below.
- No third-party package installation is currently required. The app uses Apple system frameworks and a bundled JavaScript bridge.

The deployment target is currently macOS 27.0. Older macOS versions and Intel Macs are not supported by the distributed builds.

### Run in Xcode

1. Clone/download this repository and open `YTMusic.xcodeproj`.
2. Select the **YTMusic** scheme and **My Mac** destination.
3. For automatic signing, select your own development team under Signing & Capabilities. For a fork, choose your own bundle identifier as appropriate; the checked-in identifier/team refer to the original project.
4. Build and run. Sign in through the app's account window.

Changing the bundle identifier or WebKit profile identity may result in a separate local login/data container.

### Command-line Debug build

Run from the repository root with Xcode selected as the active developer directory:

```sh
xcodebuild -project YTMusic.xcodeproj \
  -scheme YTMusic -configuration Debug \
  -destination 'platform=macOS,arch=arm64' \
  -derivedDataPath /tmp/ytmusic-debug-build \
  ARCHS=arm64 ONLY_ACTIVE_ARCH=YES \
  CODE_SIGN_IDENTITY=- CODE_SIGN_STYLE=Manual build
```

The app is produced at `/tmp/ytmusic-debug-build/Build/Products/Debug/YTMusic.app`. This command uses local ad-hoc signing rather than your developer account.

## Checks and testing

These are standalone regression executables/scripts, not an XCTest target. See [Tests/README.md](Tests/README.md) for coverage details.

Quick parser and playback bridge checks:

```sh
mkdir -p /tmp/ytmusic-checks/cache
xcrun swiftc -module-cache-path /tmp/ytmusic-checks/cache -parse-as-library \
  YTMusic/MusicModels.swift YTMusic/PlaybackContext.swift YTMusic/MusicParser.swift \
  Tests/MusicParserChecks.swift -o /tmp/ytmusic-checks/parser
/tmp/ytmusic-checks/parser
node Tests/PlayerBridgeChecks.cjs YTMusic/PlayerBridge.js
```

Run the remaining Swift suites on macOS from the repository root:

```sh
python3 - <<'PY'
from pathlib import Path
import subprocess

root = Path.cwd()
output = Path('/tmp/ytmusic-checks')
output.mkdir(parents=True, exist_ok=True)
sources = sorted(str(p) for p in (root / 'YTMusic').glob('*.swift')
                 if p.name != 'MyApp.swift')
suites = [
    'MusicSessionChecks', 'PlaybackFeatureChecks', 'CacheMaintenanceChecks',
    'NavigationArtworkChecks', 'ListeningToolsChecks', 'ReviewChecks',
]
for suite in suites:
    binary = output / suite
    subprocess.run([
        'xcrun', 'swiftc', '-module-cache-path', str(output / 'cache'),
        '-parse-as-library', '-default-isolation', 'MainActor',
        *sources, str(root / 'Tests' / (suite + '.swift')), '-o', str(binary),
    ], check=True)
    subprocess.run([str(binary)], check=True)
PY
```

Coverage includes parser identity/pagination, playlist occurrences, navigation/artwork fallback, session invalidation, lyrics/modes, local persistence/account separation, duplicate-removal preflight, palette extraction, cache cleanup and login-storage preservation. The JavaScript suite checks transport acknowledgements, shuffle/repeat, held-place restoration, autoplay suppression and 10,000 simulated website volume writes.

The default checks use fixtures, mock responses and/or temporary local storage; they do not sign in or send real playlist mutations. `NavigationArtworkChecks --live` is an optional public-thumbnail network check; it needs internet access and does not use login credentials.

Passing checks do not guarantee behavior against every live service response. Manually check login, song/playlist playback, queue transitions, volume, navigation, high-resolution/fallback artwork, About, atmosphere and persistence before a release. Test account-changing actions only with deliberate selections in playlists you control.

## Packaging releases

From the repository root:

```sh
bash Distribution/package-release.sh
```

The script builds an optimized, hardened-runtime **arm64 Release**, uses the sandbox/network entitlements in [Distribution/Release.entitlements](Distribution/Release.entitlements), verifies the ad-hoc signature and architecture, and creates:

```text
Distribution/YT-Music-1.0-apple-silicon-unnotarized.dmg
Distribution/YT-Music-1.0-apple-silicon-unnotarized.zip
Distribution/SHA256SUMS.txt
```

Both formats include the app and [end-user installation guide](Distribution/README.txt); the DMG includes an Applications shortcut. The script verifies disk image integrity and writes SHA-256 checksums. Its default build directory is `/private/tmp/ytmusic-distribution-build`; override it with `YT_MUSIC_BUILD_ROOT` if needed.

The script intentionally does **not** use Developer ID signing or notarization. An ad-hoc signature verifies bundle integrity but does not identify an Apple-verified publisher. No notarized build is currently provided.

For a version change, update `MARKETING_VERSION` and `CURRENT_PROJECT_VERSION` in the Xcode target. Also update the versioned filenames in `package-release.sh`, the distribution guide and this README. About reads the version/build from the built bundle.

Publish DMG, ZIP and checksums together as GitHub Release assets. Build outputs do not need to be committed to the source repository.

## Architecture

| Area | Main files | Responsibility |
| --- | --- | --- |
| App and UI | `MyApp.swift`, `ContentView.swift`, `MusicPageView.swift`, `MusicStyle.swift` | Window/menu setup, native navigation, lists and visual styles |
| Session coordinator | `MusicSession.swift`, `PlaybackContext.swift` | Account generations, navigation/cache state, player commands, queue and restoration |
| Service access | `MusicAPI.swift`, `MusicParser.swift`, `MusicModels.swift` | Authenticated service requests, response parsing, routes and item identity |
| Playback bridge | `PlayerBridge.js`, `PlaybackMetadata.swift`, `PlaybackFeatures.swift` | WebKit player reporting/control, exact-song metadata and playback features |
| Player surfaces | `PlaybackBar.swift`, `ExpandedNowPlayingView.swift`, `SongActionsMenu.swift` | Bottom/expanded player and song actions |
| System integration | `SystemMediaControls.swift` | macOS Now Playing information and remote commands |
| Listening tools | `ListeningTools.swift`, `ListeningModels.swift`, `ListeningToolsViews.swift`, `PlaylistDoctorView.swift` | Local persistence, held places, trails, discoveries and playlist auditing |
| Artwork | `ArtworkLoader.swift`, `ArtworkAtmosphere.swift` | Bounded/coalesced downloads, fallback validation and off-main palette extraction |
| Cache and settings | `CacheMaintenance.swift`, `CacheSettingsView.swift` | Temporary-cache allowlist, scheduling and preferences |
| About | `AppAbout.swift`, `Credits.rtf` | Native resizable About window and bundled feature descriptions |
| Distribution/design | `Distribution/`, `Design/`, `Assets.xcassets` | Packaging, entitlements, user guide and icon assets |

The main UI uses SwiftUI/AppKit. A persistent `WKWebView` provides the YouTube Music session and actual media playback. Native requests use session-derived authentication and the service's internal web endpoints; this is **not** the supported public YouTube Data API or a Google OAuth SDK integration. No separate audio downloader/decoder is bundled.

Account-generation checks discard stale responses/actions across account changes. Playlist operations retain exact occurrence IDs and perform fresh checks before mutations. Artwork requests are coalesced with bounded memory/failure caching; colour extraction uses a small thumbnail away from the main thread.

## Limitations and troubleshooting

- **Service compatibility:** internal endpoints, response layouts and browser behavior can change without notice. Features may require maintenance or become unavailable.
- **Login:** if the session expires, use the account window to sign in again. Embedded sign-in behavior depends on Google/WebKit; successful past login is not a guarantee for every account or future service policy.
- **Missing sections/content:** availability depends on account, subscription, region and what the service exposes. The app does not unlock restricted or subscription-only content.
- **Artwork:** some uploads have only small images or no useful cover. Larger artwork is preferred when usable; fallback quality is limited by the source.
- **Playlist search:** searches loaded entries, not a guaranteed server-side search of every unloaded entry.
- **Playlist Doctor:** unavailable flags may reflect account/region restrictions. A fresh removal preflight cannot atomically lock the playlist against edits made from another device between checking and writing.
- **Saved queues:** bounded snapshots do not preserve unlimited radio recommendations or guarantee that previously available tracks remain playable later.
- **Lyrics:** plain text only when provided; timed line highlighting is not implemented.
- **Cache:** clearing temporary caches intentionally preserves authentication and local listening data; it is not a complete reset.
- **Distribution:** unnotarized packages may prompt macOS security controls. Clean-machine Gatekeeper behavior and hardware media keys have not been exhaustively tested.
- **Offline use:** there are no downloaded songs, offline playback or cross-device sync for the local tools.

For an apparently missing atmosphere effect, confirm it is enabled, increase intensity and use a song with colourful artwork. Dark/neutral covers produce a subtle tint. It is visible in background gradients, including the expanded player, rather than as a filter on the cover itself.

## Contributing and reporting issues

When reporting a bug, include the app version/build, macOS version, Mac model/chip, reproduction steps and expected/actual behavior. A public track/playlist link or redacted screenshot can help with parsing/artwork issues. Explain whether the issue affects reading, playback or an account-changing action.

**Never post passwords, cookies, authorization headers, browser-profile files, account identifiers or private listening data.** Review logs, screenshots and crash reports before sharing. Do not open a public issue containing credentials or an exploitable account-data exposure; arrange a private report with the repository maintainer.

For changes, keep account isolation, exact playlist-entry identity, user-initiated mutations, cache/login separation and Reduce Motion behavior intact. Add meaningful regression checks for parser, persistence, playback or mutation-safety changes, and update user-facing documentation when behavior changes.

Before the first public upload, review the files you plan to publish. Exclude Xcode user state (`xcuserdata`), DerivedData/build output, `.DS_Store`, local credentials, diagnostics and runtime data; review development notes/screenshots for personal information. Commit the source, assets, project configuration, tests and documentation. This README does not publish the repository or create releases.

## License and acknowledgements

Open-Source. See LICENSE file for details.

Built with Apple's SwiftUI, AppKit, WebKit, MediaPlayer, ImageIO and CryptoKit frameworks. Music, artwork, metadata and lyrics are supplied by the relevant online services and rights holders; their inclusion in the app does not transfer ownership or grant redistribution rights. Use remains subject to the applicable service terms and content permissions.
