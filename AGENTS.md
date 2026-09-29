# AGENTS.md — layer-google-cloud

Standalone candy repo for the `google-cloud` layer — the Google Cloud SDK,
landing `gcloud`, `gsutil`, and `bq` on `PATH` from the official x86_64 tarball.
The candy lives in `charly.yml` at the repo root and projects the `google-cloud`
skill entity (`family: coder`).

Canonical files:

- `charly.yml` — the `google-cloud:` candy entity and the `google-cloud-skill:`
  skill entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-coder:google-cloud` — the owning skill: the tarball install story,
  the `/var/opt` prefix, and the CLI checks. Load before editing or
  troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package
  sections). Load before editing any entity field or plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence: the
  `/usr/bin/{gcloud,gsutil,bq}` symlink checks, the `gcloud --version` /
  `bq version` / `gsutil version` exit checks, and the `/var/opt` tree check.
- The `download:` step targets the x86_64 tarball; the candy is x86_64-only as
  written.

## Modify this repo

- Edit the `google-cloud:` candy entity in `charly.yml`; keep the matching
  `google-cloud-skill:` entity in step with it.
- The install prefix and the symlink loop are one unit — a change to one is a
  change to the `/usr/bin/*` checks.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
