# Align CI with pioarduino stable

## Goal

Restore clean-checkout builds after the pioarduino stable channel raised its
minimum supported PlatformIO Core version.

## Cause

The embedded project manifests already select pioarduino's stable platform:

```text
https://github.com/pioarduino/platform-espressif32/releases/download/stable/platform-espressif32.zip
```

That channel now requires PlatformIO Core 6.2.0 or newer. The main CI and the
legacy GitHub release workflow still installed 6.1.19, so PlatformIO rejected
the platform before compiling any source.

## Change

Every main-CI job now installs PlatformIO 6.2.0, matching the already-working
PlatformIO Registry publication workflow. The monophonic GitHub release job is
updated at the same time so the next tag cannot rediscover the same toolchain
mismatch.

## Validation

The GitHub Actions CI matrix must pass:

- monophonic package tests, pack, and isolated consumer;
- M5 tone output pack and isolated consumer;
- Plus2 buzzer local test app;
- Core Gray speaker local test app.

The `m5-tone-output-v0.1.5` publication workflow already proved the package
consumer with PlatformIO 6.2.0 and pioarduino stable.
