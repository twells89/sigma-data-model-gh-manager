# Update: Workbooks as Code + Sigma GitOps

> Follow-up to [Programmatic Data Model Management: Open-Source Tools](https://community.sigmacomputing.com/t/programmatic-data-model-management-open-source-tools/6445). Draft for posting to the community thread.

A few of you asked: *"This is great for data models — can it do workbooks too?"* Now it can. The GitHub-integrated tool has been extended to manage **workbooks as code** alongside data models, and renamed to **Sigma GitOps** to reflect that it's no longer data-models-only.

## What's new

- **Workbooks as code.** Pull workbook specs from Sigma into your repo, review/edit them as JSON, and let GitHub Actions sync approved changes back — the same PR-reviewed loop you already use for data models. Backed by `GET /v2/workbooks/{id}/spec`, `POST /v2/workbooks/spec`, and `PUT /v2/workbooks/{id}/spec`.
- **Folder-scoped pull.** In the app's new **Workbooks** tab, click **⬇ Folder**, pick a Sigma folder, and it pulls every workbook spec in it into `workbooks/`. Folder selection is the trust boundary — point it at folders you know are built through the spec.
- **A round-trip safety guard.** Workbook spec coverage isn't 100% yet, so on sync the tool fetches the live spec and **blocks any push that would drop pages, elements, or fields present in the live workbook** — an incomplete spec can't silently break a dashboard. Override intentionally with `ALLOW_WORKBOOK_REMOVALS=true`.
- **Separate paths.** Data models commit to `data-models/`, workbooks to `workbooks/` — each configurable, and the active path follows the Data Models / Workbooks toggle.

## Why workbooks as code?

The same wins as data models — version control, code review, collaboration, automated deployment, and backup/restore — now for the dashboards themselves. Diff a workbook change in a PR. Roll back a bad edit. Promote a workbook across environments from git.

## Getting started

1. Open the app: **https://twells89.github.io/sigma-data-model-gh-manager/**
2. Create a repo from the template: **https://github.com/twells89/sigma-gitops** (*Use this template*).
3. Configure repo secrets/variables (`SIGMA_CLIENT_ID`, `SIGMA_SECRET`, `SIGMA_CLOUD`, `SIGMA_FOLDER_ID`) and enable read/write workflow permissions — same as before.
4. Connect Sigma + GitHub, switch to the **Workbooks** tab, and hit **⬇ Folder**.
5. In `config.yml`, set `manage_workbooks: true` and list your `workbook_folders` to keep the daily pull in sync.

## A note on the spec

Workbook spec coverage is still growing. Folder selection + the round-trip guard are deliberate guardrails: pull the folders you trust are spec-built, and the guard prevents a partial spec from overwriting richer live content. As coverage expands, more workbooks become safe to round-trip.

## Resources

- **App (Sigma GitOps):** https://twells89.github.io/sigma-data-model-gh-manager/
- **Template repo (Actions + scripts):** https://github.com/twells89/sigma-gitops
- **Sigma API docs:** workbook + data model `/spec` endpoints

As always — fork it, extend it, and share what you build. 🚀
