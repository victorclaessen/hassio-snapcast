# Upgrading librespot (and the add-on)

Home Assistant builds this add-on locally from `snapcast-server/Dockerfile`
(there is no `image:` in `config.yaml`), so a librespot upgrade is:

1. Pick the librespot source in `snapcast-server/Dockerfile`:
   - a release: set `LIBRESPOT_VERSION` (see https://crates.io/crates/librespot)
     and set `LIBRESPOT_GIT_REV=` (empty);
   - a git commit (dev branch or a pull request): set `LIBRESPOT_GIT_REV` to the
     full commit hash. For a PR, get it with
     `git ls-remote https://github.com/librespot-org/librespot refs/pull/<nr>/head`.
     Always pin a full hash, never a branch: PR branches get force-pushed.
2. Bump `version` in `snapcast-server/config.yaml` to something higher than the
   version currently installed (check with `ha apps info 978cbd8a_snapcast-server`).
   Home Assistant only offers an update when this number goes up.
3. Add a `CHANGELOG.md` entry, commit, push to `main`.
4. In Home Assistant: Settings > Add-ons > Add-on store > ⋮ > Check for updates,
   then update the Snapcast server add-on. The build compiles librespot and takes
   a while.
5. Check: `docker exec app_978cbd8a_snapcast-server librespot --version`
   and the add-on log (no reconnect loop every few seconds).

If the build fails with an unknown error, `ha supervisor logs` only shows the
tail. Reproduce a failing `apk` step in a throwaway container instead (the
base image uses s6 as init, so bypass it):
`docker run --rm --entrypoint /bin/sh ghcr.io/hassio-addons/base:<tag> -c 'apk add --no-cache cargo avahi-dev'`

Going back to a release once the fix is in one: set `LIBRESPOT_VERSION` to it,
empty `LIBRESPOT_GIT_REV`, and bump the version again.
