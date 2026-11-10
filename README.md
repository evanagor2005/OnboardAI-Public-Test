# OnboardAI Public Test

Selected public GitHub documentation repository for realistic OnboardAI test samples.

- Repository: <https://github.com/evanagor2005/OnboardAI-Public-Test>
- Selected branch: `main`
- Last corpus update: 2026-11-09

All documents under `docs/` are **realistic sample documents** for a fictional demo company, Cedar Works. They contain no real employee records, secrets, or adopted company policies. No real-document project-team approvals are asserted. Each approved document is explicitly marked as a realistic sample.

## Approved files for the test corpus

This table is the complete approved file list for the test corpus. Adding a file to the repository does not approve it automatically.

| Repository-relative path | Classification | Purpose |
| --- | --- | --- |
| [docs/software/backend-development.md](docs/software/backend-development.md) | Team-specific: Software | Local backend setup, changes, and review |
| [docs/software/databases.md](docs/software/databases.md) | Team-specific: Software | Database schema conventions, migrations, local setup, and backups |
| [docs/software/apis.md](docs/software/apis.md) | Team-specific: Software | API contracts, authentication, versioning, errors, and testing |
| [docs/software/deployment-and-releases.md](docs/software/deployment-and-releases.md) | Team-specific: Software | Verified artifacts, staging, release checks, and rollback |
| [docs/software/git-workflow-and-code-review.md](docs/software/git-workflow-and-code-review.md) | Team-specific: Software | Branches, focused changes, and code review |
| [docs/software/incident-response-and-on-call.md](docs/software/incident-response-and-on-call.md) | Team-specific: Software | On-call preparation, incident response, and escalation |
| [docs/software/secure-coding-and-secrets.md](docs/software/secure-coding-and-secrets.md) | Team-specific: Software | Input validation, authorization, and secret handling |
| [docs/software/testing-and-ci.md](docs/software/testing-and-ci.md) | Team-specific: Software | Test selection and continuous integration |
| [docs/hr/employee-onboarding.md](docs/hr/employee-onboarding.md) | Team-specific: HR | Employee preparation and first-week coordination |
| [docs/hr/benefits-enrollment.md](docs/hr/benefits-enrollment.md) | Team-specific: HR | Benefits orientation and enrollment coordination |
| [docs/hr/hiring-and-interviewing.md](docs/hr/hiring-and-interviewing.md) | Team-specific: HR | Hiring preparation and structured interviews |
| [docs/hr/payroll-and-timesheets.md](docs/hr/payroll-and-timesheets.md) | Team-specific: HR | Payroll setup and timesheet review |
| [docs/hr/performance-reviews.md](docs/hr/performance-reviews.md) | Team-specific: HR | Performance review preparation and follow-up |
| [docs/hr/required-training-and-compliance.md](docs/hr/required-training-and-compliance.md) | Team-specific: HR | Required training coordination and completion records |
| [docs/hr/time-off-and-leave.md](docs/hr/time-off-and-leave.md) | Team-specific: HR | Time-off requests and confidential leave coordination |
| [docs/shared/company-handbook.md](docs/shared/company-handbook.md) | Company-wide shared | Source evidence, access, learning, and support |
| [docs/shared/team-onboarding-demo.md](docs/shared/team-onboarding-demo.md) | Company-wide shared | One document with `team = software` and `team = HR` sections for milestone 1 |
| [docs/shared/it-accounts-and-security.md](docs/shared/it-accounts-and-security.md) | Company-wide shared | Company accounts, managed devices, and access requests |
| [docs/shared/new-hire-checklist-for-managers.md](docs/shared/new-hire-checklist-for-managers.md) | Company-wide shared | Shared HR, IT, and manager onboarding responsibilities |
| [docs/shared/travel-and-expense-reimbursement.md](docs/shared/travel-and-expense-reimbursement.md) | Company-wide shared | Travel approval and expense reimbursement |

The milestone-3 selection contains 20 realistic samples: 8 Software, 7 HR, and 5 shared documents. The Knowledge service's `config/demo-source.toml` is the executable corpus inventory; keep it aligned with this reviewed selection. Approval here covers inclusion in the synthetic evaluation corpus, not adoption as real organizational policy.

Team classifications describe content, not ownership or retrieval permissions. All selected documentation belongs to one common knowledge pool. The mixed-team document's markers are ordinary text, not filters; Software evidence should be retrieved for its relevance while HR evidence remains eligible.

## Acquisition handoff

Merge the approved files to `main` before running acquisition. For each run, resolve `main` once to a commit SHA and read the exact approved paths from that revision. Preserve repository URL, original file URL, file path, classification, sample designation, and revision for downstream source records.

Merge the public-test content change before merging corresponding manifest additions in OnboardAI-Knowledge. Acquisition is all-or-nothing, so a manifest entry for a file that is not yet on `main` makes the complete run fail.

Files outside the table must not be indexed. This includes `README.md` and the original placeholder `test.md`. Do not recursively index directories or silently add new files. A missing approved file or download failure must be reported explicitly rather than treating partial acquisition as successful.

The sample documents state creation and last-updated dates labeled as simulated source metadata. These describe fictional document history, not actual Git commit timestamps. Keep source-provided dates distinct from repository history and retrieval time; an absent source date remains unknown.

Acquisition and enforcement of this approved list belong to OnboardAI-Knowledge. This repository records the content selection; it does not implement indexing. The Knowledge service acquires approved files, stores source versions, splits and embeds content, and serves retrieval results.

## Evaluation note (not indexed)

The README is not in the approved source manifest. For the APIs sample, the intended AI-inferred step is to obtain a test-only access token from the approved development identity service before running authenticated API tests. The source describes the need for access tokens and test credentials but deliberately does not explain how to obtain one.

## Changing the approved list

Review changes to this table before acquisition uses them. Mark new samples as realistic sample documents. Before approving a real document, record the project-team approver, approval date, and review evidence here.

## Traceability

- Requirements: SR-DATA-001, SR-DATA-002, SR-DATA-005, SR-DATA-009.
- Architecture rules: AR-SYS-003, AR-DATA-001.
- GitHub selection only; website/wiki selection remains milestone 5.
