# Sigma GitOps

A single-file, browser-based app for managing Sigma Computing **data models and workbooks as code**, backed by GitHub. It connects to the Sigma API and to your GitHub repo. You pull specs, edit them, and commit changes through PRs. GitHub Actions sync approved changes back to Sigma.

**Live app:** https://twells89.github.io/sigma-data-model-gh-manager/
**Companion repo (Actions and scripts):** https://github.com/twells89/sigma-gitops

> Sigma is always the source of truth. This tool tracks changes, enables PR review, and keeps history. Credentials live in browser memory and localStorage only. They go to Sigma and GitHub, nowhere else.

> 🧪 **Workbooks as code is in a limited private beta.** The workbook spec API doesn't cover everything yet. To get added to the access list, reach out to your CSM with your use case. Data models as code is generally available.

## What it does

- **Connect** to Sigma (Client ID and Secret) and GitHub (PAT and repo).
- **Data Models** tab: list, edit, and commit data model specs (`data-models/`).
- **Workbooks** tab (private beta): manage workbooks as code (`workbooks/`).
  - **⬇ Folder**: pull every workbook spec in a chosen Sigma folder. Folder choice is the trust boundary.
  - **+ Adopt**: bring a single workbook under management by ID.
- **Branches, PRs, diff, and version history** built in. The editor supports JSON and YAML, undo/redo, and AI-assisted edits.

## Quick start

1. Open the live app, or `index.html` locally.
2. Create Sigma API credentials: **Administration → Developer Access → Create New**.
3. Point it at a repo created from [`sigma-gitops`](https://github.com/twells89/sigma-gitops) (Use this template). Set that repo's secrets and variables (`SIGMA_CLIENT_ID`, `SIGMA_SECRET`, `SIGMA_CLOUD`, `SIGMA_FOLDER_ID`). Turn on read/write workflow permissions.
4. Create a GitHub PAT (`repo` scope), connect, and start managing models and workbooks.

See the in-app **📖 Setup Guide** for the full walkthrough.

## Workbooks: safety

Workbook spec coverage isn't complete, so the sync workflow runs a **round-trip guard**. Before it updates a live workbook, it blocks any push that would remove pages, elements, or fields present in the live version. Override on purpose with `ALLOW_WORKBOOK_REMOVALS=true`. Pull the folders you trust are spec-built. The guard backs you up on write.
