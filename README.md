# Abuild Pixman archive

This repository preserves the historical Pixman source revisions formerly
used by Abuild. The authoritative project is maintained by the
[freedesktop.org Pixman project](https://gitlab.freedesktop.org/pixman/pixman);
the original Pixman 0.32.8 documentation remains available in the repository's
[upstream README](README).

The long-lived branches have deliberately separate roles:

- `master` follows the official upstream `master` branch;
- `abuild` is the final source revision used by Abuild;
- `archive/abuild-pin-d93ec571` preserves an additional revision used by an
  historical Abuild development branch; and
- `abuild-gh` adds only this maintenance README and files below `.github/` to
  `abuild`.

The `abuild` branch is exactly the official `pixman-0.32.8` tag at
`7b13cb0e`. The historical `theil-buster-wip` branch briefly selected upstream
commit `d93ec571`, eight commits after `pixman-0.40.0`; the dedicated archive
branch keeps that Gitlink target reachable without changing the final Abuild
baseline.

Abuild no longer builds the vendored Pixman sources. The historical branches
are retained for provenance and reproducibility, not as recommended Pixman
versions for new deployments.

## Continuous integration

Run the same Trixie check locally with Docker:

```sh
.github/ci/run .github/ci/check
```

The check regenerates the Autotools files, configures the historical source
without its optional GTK demonstration programs, builds it, runs the complete
upstream test suite, and checks the generated package metadata. It executes in
a non-root, read-only container without network access or Linux capabilities.

The weekly upstream monitor checks whether `master` and the mirrored release
tags still match the authoritative freedesktop.org repository. It reports
drift but never updates branches automatically.
