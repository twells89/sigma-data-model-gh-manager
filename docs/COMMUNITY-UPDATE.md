# Update: Workbooks as Code in Sigma GitOps

> Follow-up to the original post: https://community.sigmacomputing.com/t/programmatic-data-model-management-open-source-tools/6445

> 🧪 Private beta. Workbooks as code is in private beta. The workbook spec API doesn't cover everything yet. Try it on non-critical content first. Reach out for access or to report issues.

A few of you asked if this could do workbooks, not just data models. Now it can.

The GitHub-integrated tool now manages workbooks as code next to data models. We renamed it Sigma GitOps.

## What's new

- **Workbooks as code.** Pull a workbook spec from Sigma into your repo. Review and edit it as JSON. GitHub Actions sync approved changes back. It's the same PR-reviewed loop you use for data models. It runs on the workbook spec API: GET, POST, and PUT on `/v2/workbooks/{id}/spec`.
- **Folder pull.** Open the Workbooks tab, click Folder, and pick a Sigma folder. The tool pulls every workbook spec in it. Folder choice is the trust boundary. Point it at folders you built through the spec.
- **Round-trip guard.** Spec coverage isn't complete, so the sync checks first. It blocks any push that would drop pages, elements, or fields that exist in the live workbook. An incomplete spec can't quietly break a dashboard. Override on purpose with `ALLOW_WORKBOOK_REMOVALS=true`.
- **Separate paths.** Data models commit to `data-models/`. Workbooks commit to `workbooks/`. Each path is configurable, and the active one follows the toggle.

## Why workbooks as code

You get the same wins you already get for data models, now for the dashboards themselves. Version control. Code review. Automated deploys. Backup and restore. Diff a workbook change in a PR. Roll back a bad edit. Promote a workbook across environments from git.

## Get started

1. Open the app: https://twells89.github.io/sigma-data-model-gh-manager/
2. Create a repo from the template: https://github.com/twells89/sigma-gitops (Use this template).
3. Add the repo secrets and variables (`SIGMA_CLIENT_ID`, `SIGMA_SECRET`, `SIGMA_CLOUD`, `SIGMA_FOLDER_ID`). Turn on read/write workflow permissions. Same as before.
4. Connect Sigma and GitHub. Open the Workbooks tab. Click Folder.
5. In `config.yml`, set `manage_workbooks: true` and list your `workbook_folders` to keep the daily pull in sync.

## A note on the spec

Spec coverage is still growing. That's why this is a private beta. Two guardrails keep it safe. Folder choice means you pull only the folders you trust. The round-trip guard stops a partial spec from overwriting live content. As coverage grows, more workbooks become safe to round-trip, and we'll widen the beta.

## Resources

- App (Sigma GitOps): https://twells89.github.io/sigma-data-model-gh-manager/
- Template repo (Actions and scripts): https://github.com/twells89/sigma-gitops
- Sigma API docs: workbook and data model `/spec` endpoints

Fork it, extend it, and share what you build. 🚀
