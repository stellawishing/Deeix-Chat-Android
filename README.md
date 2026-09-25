# Deeix-Chat Android

Android WebView client for `https://chat.stella-wishing.xyz/`.

The app requires network access: it wraps the live website and does not work offline.
It supports cookies, file selection, downloads, external app links, and web camera/
microphone requests. Android asks for those device permissions only when the website
requests them. Location requests are disabled.

## Installable build

Every push to `main` builds an installable APK under the Actions run's
`Deeix-Chat-debug-apk` artifact. Download and extract the artifact ZIP, then
install `app-debug.apk` on Android 7.0 or newer. For local builds, use JDK 17,
Android SDK 35, and Gradle 8.7:

```bash
gradle --no-daemon :app:assembleDebug
```

The output is `app/build/outputs/apk/debug/app-debug.apk`.

This is a debug-signed development build. A production release needs a persistent,
privately held signing key; do not publish a throwaway-signed release and expect
future updates to install over it. Android WebView must be available and current
on the device. Some third-party identity providers disallow signing in from
embedded browsers, depending on the website's authentication flow.

## Production releases

Production releases must use one long-lived signing identity for every update.
Keep the keystore and its passwords in a private secret store; never generate a
new key for each update and never commit it to the repository.

The release workflow expects these repository secrets: `RELEASE_KEYSTORE_BASE64`,
`RELEASE_STORE_PASSWORD`, `RELEASE_KEY_ALIAS`, and `RELEASE_KEY_PASSWORD`. Create
a tag matching `versionName` (for example `v1.1.0`) to publish a release.

Version 1.1.0 adds a status-bar-safe edge-to-edge layout, native network error
recovery, WebView renderer recovery, safer navigation, cache controls,
configurable HTTPS server addresses, and HTTPS Deep Links. A configured server
must host a Deeix-compatible web application.

Long-press the safe-area strip above the page to open the native app menu. The
menu is intentionally outside the website header so it cannot cover the site's
own buttons.

On Android 15 and newer the page respects status bar, cutout, navigation, and
keyboard insets. On mobile, swiping right from the left edge opens the website's
own sidebar through its existing control.
