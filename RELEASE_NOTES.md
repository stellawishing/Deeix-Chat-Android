# Deeix-Chat 1.2.0

This release starts the tag-driven, multi-platform release line.

- Android versionCode 3 and versionName 1.2.0.
- Android production APK is built and signed from the persistent GitHub Secrets.
- iOS and HarmonyOS release targets now have documented project contracts and CI entry points.
- All release metadata is kept in `release-config.json`.
- The repository uses `main` for development and `v*` tags for production releases.

The Android APK is a WebView client for https://chat.stella-wishing.xyz/ and includes
status-bar-safe edge-to-edge layout, WebView recovery, file upload, downloads,
cookies, server configuration, and HTTPS Deep Links.

`v1.2.0` uses the signing key saved for the 1.1.0 release line. Android users with
the old 1.0.0 package must uninstall it before installing this release.
