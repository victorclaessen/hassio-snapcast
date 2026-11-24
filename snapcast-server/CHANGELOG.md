<!-- https://developers.home-assistant.io/docs/add-ons/presentation#keeping-a-changelog -->
## 0.4.12

- feat: keep snapserver state (groups, client names, volumes, stream per group) in /data/snapserver so it survives restarts
- change: Spotify is now the first (default) stream, before DLNA and user-defined streams; new clients start on Spotify

## 0.4.11

- fix: install snapweb~0.9.2 instead of the exact 0.9.2-r0 (edge/testing now has 0.9.2-r1)

## 0.4.10

- fix: let cargo fetch the librespot git source with the git CLI (CARGO_NET_GIT_FETCH_WITH_CLI, git as build dependency)

## 0.4.9

- fix: unpin musl/musl-utils and upgrade base packages before installing build dependencies (base image 18.1.0 pins musl 1.2.5-r10, Alpine 3.22 musl-dev needs r13)

## 0.4.8

- update: build librespot from git: dev + PR #1861 (3372e62), fixes the spirc restart loop on dealer websocket drops
- update: librespot source selectable via LIBRESPOT_VERSION / LIBRESPOT_GIT_REV in the Dockerfile
- chore: drop `image:` from config.yaml so Home Assistant builds the add-on locally from the Dockerfile
- docs: UPGRADING.md

## 0.4.5

- update: librespot 0.8.0, snapweb 0.9.2

## 0.4.4

- update: bump ghcr.io/hassio-addons/base to v18.1.0
- update: bump librespot to 0.7.0 (fixes #10)
- chore: cleanup Dockerfile

## 0.4.3

- fix: respect samplerate in DLNA Media Render
- fix(snapserver): typo in config

## 0.4.2

- fix dbus long startup by @unex in #4

## 0.4.1

- Fix snapweb. Drop support for 32bit platforms

## 0.4.0

- Dependcy Updates. Please migrate to libresport / Spotify token auth.

## 0.3.0

- Add support for DLNA Media Renderer: Connect Homeassitant with snapcast through DLNA

## 0.2.1

- Wait before starting snapcast-client until snapcast-server is started. 
- Use host `127.0.0.1` for snapcast-client 

## 0.2.0

- Add Snapcast client for local playback through Home Assistant.

## 0.1.0

- Add support for Snapweb: a web-interface for Snapcast.

## 0.0.1

- Initial version based on the Home Assistant Add-on example. Supports Snapcast server and Spotify connect.
