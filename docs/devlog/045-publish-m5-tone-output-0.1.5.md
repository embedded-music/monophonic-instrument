# Publish m5-tone-output 0.1.5

## Goal

Release the package-owned PCM idle policy so standalone firmware consumers can
use it without a sibling checkout.

## Release

Version `0.1.5` adds the `AudioIdlePolicy` public header and the keep-alive
behavior already validated by the metronome. The package repository metadata
now points at the `embedded-music` organization.

This release unblocks the metronome's M5Burner build from consuming only
PlatformIO Registry packages. The tag `m5-tone-output-v0.1.5` triggers the
existing isolated-consumer, package, and registry publication workflow.

## Validation

```text
pio run -d ci/consumers/m5-tone-output
pio pkg pack packages/m5-tone-output --output /tmp
```

After publication, the metronome release candidate must resolve
`fcz2/m5-tone-output@0.1.5` from a clean dependency graph and build its merged
factory image.
