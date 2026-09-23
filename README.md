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
