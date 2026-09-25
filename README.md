# Deeix-Chat

Multi-platform WebView clients for `https://chat.stella-wishing.xyz/`.

The Android client is production-ready. iOS and HarmonyOS targets share the same
website and release metadata, with native platform adapters for permissions, file
providers, downloads, cookies, safe areas, links, and signing.

## Repository layout

```text
app/                       Android application module
platforms/ios/             iOS project contract and future WKWebView target
platforms/harmony/         HarmonyOS project contract and future ArkTS target
scripts/deeix-release      Local release CLI
release-config.json        Single source of version and artifact metadata
.github/workflows/release  Tag-driven multi-platform release pipeline
```

`main` is the only long-lived development branch. Production releases start from a
version tag such as `v1.2.0`; release branches are not required.

## Local CLI

```bash
./scripts/deeix-release version
./scripts/deeix-release check
./scripts/deeix-release set-version 1.2.0 3
./scripts/deeix-release android-debug
./scripts/deeix-release tag
./scripts/deeix-release publish
```

`tag` only creates a local annotated tag. Push it after reviewing the commit:

```bash
git push origin main
git push origin v1.2.0
```

For an authenticated checkout with a clean `main` branch, `publish` performs the
version check, creates or verifies the annotated tag, pushes `main`, and pushes the
tag in one step. The tag push starts the GitHub Release workflow.

## Android

The Android app requires network access and wraps the live website. It supports
persistent cookies and DOM storage, file selection, downloads, external links,
web camera/microphone requests, server configuration, HTTPS Deep Links, safe-area
insets, loading/error recovery, and renderer recovery. Location requests are disabled.

Build locally with JDK 17, Android SDK 35, and Gradle 8.7:

```bash
./scripts/deeix-release android-debug
```

Every push to `main` also builds a debug APK artifact in GitHub Actions. The production
workflow requires these repository Secrets:

```text
RELEASE_KEYSTORE_BASE64
RELEASE_STORE_PASSWORD
RELEASE_KEY_ALIAS
RELEASE_KEY_PASSWORD
```

Keep the v1.1.0 signing backup private. From v1.2.0 onward, every Android update must
use the same key stored in those Secrets.

## Multi-platform release

Pushing a `v*` tag starts one release pipeline. Android always produces the signed APK.
The iOS job activates when `platforms/ios/DeeixChat.xcodeproj` exists, and the HarmonyOS
job activates when `platforms/harmony/DeeixChat/oh-package.json5` exists. This keeps the
release entry point synchronized while allowing each platform to use its native build
and signing toolchain.

The first v1.2.0 release is an Android release with iOS and HarmonyOS project contracts
in place. Add the native projects and their signing credentials before enabling those
artifacts in the same pipeline.
