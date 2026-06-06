# Sigma GitOps

A single-file, browser-based app for managing Sigma Computing **data models and workbooks as code**, backed by GitHub. It connects directly to the Sigma API and to your GitHub repo so you can pull specs, edit them, and commit changes through PRs — with GitHub Actions syncing approved changes back to Sigma.

**Live app:** https://twells89.github.io/sigma-data-model-gh-manager/
**Companion repo (Actions + scripts):** https://github.com/twells89/sigma-gitops

> Sigma is always the source of truth. This tool tracks changes, enables PR review, and maintains history. Credentials live in browser memory / localStorage only — never sent anywhere but Sigma and GitHub.

## What it does

- **Connect** to Sigma (Client ID + Secret) and GitHub (PAT + repo).
- **Data Models** tab — list, edit, and commit data model specs (`data-models/`).
- **Workbooks** tab — manage workbooks as code (`workbooks/`):
  - **⬇ Folder** — pull every workbook spec in a chosen Sigma folder (folder selection is the trust boundary).
  - **+ Adopt** — bring a single workbook under management by ID.
- **Branches, PRs, diff & version history** built in. Editor supports JSON/YAML, undo/redo, and AI-assisted edits.

## Quick start

1. Open the live app (or `index.html` locally).
2. Create Sigma API credentials: **Administration → Developer Access → Create New**.
3. Point it at a repo created from [`sigma-gitops`](https://github.com/twells89/sigma-gitops) (Use this template). Configure that repo's secrets/variables (`SIGMA_CLIENT_ID`, `SIGMA_SECRET`, `SIGMA_CLOUD`, `SIGMA_FOLDER_ID`) and enable read/write workflow permissions.
4. Create a GitHub PAT (`repo` scope), connect, and start managing models/workbooks.

See the in-app **📖 Setup Guide** for the full walkthrough.

## Workbooks: safety

Workbook spec coverage isn't 100%, so the sync workflow runs a **round-trip guard**: before updating a live workbook it blocks any push that would remove pages, elements, or fields present in the live version (override with `ALLOW_WORKBOOK_REMOVALS=true`). Pull the folders you trust are spec-built; the guard backs you up on write.
