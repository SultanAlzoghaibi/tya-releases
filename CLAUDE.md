# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this repo is

This is the **release / auto-update artifact store** for the TyA Tauri app. It is the endpoint the deployed app pulls from to self-update via the Tauri updater plugin.

This is **not** a source repository. There is no application code to build or run here.

## Hard rules

- **Do not add source code.** No `.rs`, `.ts`, `.go`, `.py`, etc. `.gitignore` blocks source for every language by design. The only tracked files are release artifacts (installers, archives), their `.sig` signatures, the `latest.json` updater manifest, and docs (`README.md`, `CLAUDE.md`, `LICENSE.txt`).
- **Never commit the updater private signing key** or any secret. Only signatures and public manifests belong here.
- **Do not hand-edit signature values.** They come from the Tauri signer in the source repo's build.

## Common tasks

- **Publish a release:** create a `vX.Y.Z` GitHub Release, attach the signed bundles, then update `latest.json` (`version`, `pub_date`, `notes`, per-platform `signature` + `url`).
- **Update the manifest:** edit `latest.json` only — keep it valid JSON matching the Tauri updater schema (see `README.md` for shape).

## Platform target keys (Tauri updater)

`darwin-aarch64`, `darwin-x86_64`, `windows-x86_64`, `linux-x86_64`. Each maps to `{ "signature", "url" }`.

## When unsure

If a change would introduce source files, build tooling, or secrets, stop and confirm — it almost certainly belongs in the TyA source repo, not here.
