# HarmonyOS release target

The HarmonyOS target is an ArkTS/ArkUI Web container for the same Deeix Chat website.
It owns Harmony-specific file selection, downloads, permissions, safe-area behavior,
URI abilities, and application signing.

Expected project path for CI:

```text
harmony/DeeixChat
```

The release workflow detects that project and builds a `.hap` when a compatible
DevEco/ohpm toolchain is available on the configured runner. The current repository
keeps this contract documented without pretending that an HAP can be built by the
Android toolchain.
