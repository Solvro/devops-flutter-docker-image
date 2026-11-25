# Flutter Web-Only Base Image

Standalone GHCR image for Flutter web-only builds.

Our custom version after discontinuation of the CirrusLabs image.

## Image tags

After pushing this directory as a repository, the publish workflow creates:

- `ghcr.io/solvro/flutter-web-only:<flutter-version>` — immutable pin for reproducible builds
- `ghcr.io/solvro/flutter-web-only:stable` — moving tag that always points at the current Flutter stable from `versions.env`

For reproducible builds, pin a version:

```dockerfile
FROM ghcr.io/solvro/flutter-web-only:3.44.1 AS build
```

For CI that should follow the latest approved stable without bumping the tag manually:

```yaml
image: ghcr.io/solvro/flutter-web-only:stable
```

## Versioning

The pinned Flutter stable version lives in `versions.env` as `FLUTTER_STABLE_VERSION`.

The scheduled updater checks the latest Flutter stable release and opens a PR that updates `versions.env`. Merging that PR triggers the publish workflow and pushes a new specific version tag plus updates the moving `stable` tag.

## Contents

This image installs Flutter from the official Flutter git tag and pre-caches only web artifacts. It does not include the Android SDK, Java runtime, or Android command-line tools.
