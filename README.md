# google-cloud

The Google Cloud SDK — `gcloud`, `gsutil`, and `bq` on `PATH`.

`google-cloud` downloads the official Google Cloud CLI x86_64 tarball, unpacks it
under `/var/opt/google-cloud-sdk`, runs the bundled `install.sh`, and symlinks
`gcloud`, `gsutil`, and `bq` into `/usr/bin` so every shell finds them. Each CLI
answers its own version subcommand, which is what the candy's checks assert.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `google-cloud` |
| Distro | all (official x86_64 tarball) |
| Binaries | `/usr/bin/gcloud`, `/usr/bin/gsutil`, `/usr/bin/bq` (symlinks into `/var/opt/google-cloud-sdk`) |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-gcp-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-google-cloud:v2026.241.0656'
```

Then, inside the built image:

```bash
gcloud --version         # Google Cloud SDK
gsutil version           # gsutil version
bq version               # BigQuery CLI
```

## Layout

- `charly.yml` — the `google-cloud:` candy entity: the `download:` step, the
  `install.sh` + symlink step, and the `check:` steps.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Family skill: `/charly-coder:google-cloud`
- `/charly-coder:google-cloud-npm` — the Firebase CLI (npm) for GCP Node.js tooling
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
