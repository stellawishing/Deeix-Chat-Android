# iOS release target

The iOS target is a native `WKWebView` container for the same Deeix Chat website.
It is intentionally kept separate from the Android module so platform permissions,
file providers, safe-area handling, cookies, downloads, and Universal Links can be
implemented with native APIs.

Expected project path for CI:

```text
ios/DeeixChat.xcodeproj
```

The release workflow detects that project and builds an `.ipa` on a macOS runner.
Apple signing certificates and provisioning profiles must be supplied through
GitHub Secrets before enabling the job.
