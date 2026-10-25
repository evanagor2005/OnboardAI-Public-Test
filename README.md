# OnboardAI Public Test

Selected public GitHub documentation repository for OnboardAI ticket #56.

- Repository: <https://github.com/evanagor2005/OnboardAI-Public-Test>
- Selected branch: `main`
- Selection date: 2026-10-24

All documents under `docs/` are **realistic sample documents** for a fictional demo company, Cedar Works. They contain no real employee records, secrets, or adopted company policies. No real-document project-team approvals are asserted. Each approved document is explicitly marked as a realistic sample.

## Approved files for the initial index

This table is the complete approved file list for #56. Adding a file to the repository does not approve it automatically.

| Repository-relative path | Classification | Purpose |
| --- | --- | --- |
| [docs/software/backend-development.md](docs/software/backend-development.md) | Team-specific: Software | Local backend setup, changes, and review |
| [docs/hr/employee-onboarding.md](docs/hr/employee-onboarding.md) | Team-specific: HR | Employee preparation and first-week coordination |
| [docs/shared/company-handbook.md](docs/shared/company-handbook.md) | Company-wide shared | Source evidence, access, learning, and support |
| [docs/shared/team-onboarding-demo.md](docs/shared/team-onboarding-demo.md) | Company-wide shared | One document with `team = software` and `team = HR` sections for milestone 1 |

Team classifications describe content, not ownership or retrieval permissions. All selected documentation belongs to one common knowledge pool. The mixed-team document's markers are ordinary text, not filters; Software evidence should be retrieved for its relevance while HR evidence remains eligible.

## Acquisition handoff

Merge the approved files to `main` before running acquisition. For each run, resolve `main` once to a commit SHA and read the exact approved paths from that revision. Preserve repository URL, original file URL, file path, classification, sample designation, and revision for downstream source records.

Files outside the table must not be indexed. This includes `README.md` and the original placeholder `test.md`. Do not recursively index directories or silently add new files. A missing approved file or download failure must be reported explicitly rather than treating partial acquisition as successful.

The sample documents state creation and last-updated dates labeled as simulated source metadata. These describe fictional document history, not actual Git commit timestamps. Keep source-provided dates distinct from repository history and retrieval time; an absent source date remains unknown.

Acquisition and enforcement of this approved list belong to #57 in OnboardAI-Knowledge. This repository records the content selection; it does not implement indexing. Source persistence (#58), splitting/embedding (#59), vector retrieval (#60), the ingestion command (#61), and MCP retrieval (#63) also belong in OnboardAI-Knowledge.

## Changing the approved list

Review changes to this table before acquisition uses them. Mark new samples as realistic sample documents. Before approving a real document, record the project-team approver, approval date, and review evidence here.

## Traceability

- Requirements: SR-DATA-001, SR-DATA-002, SR-DATA-005, SR-DATA-009.
- Architecture rules: AR-SYS-003, AR-DATA-001.
- GitHub selection only; website/wiki selection remains milestone 5.
