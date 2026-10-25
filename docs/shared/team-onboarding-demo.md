# Shared: Software and HR onboarding demonstration

Document type: realistic sample document for the fictional Cedar Works demo company.
Classification: company-wide shared content containing Software and HR sections.
Created: 2026-10-20 (simulated source date).
Last updated: 2026-10-24 (simulated source date).

This synthetic document supports the milestone-1 mixed-team retrieval demonstration. The team markers below are ordinary text, not authorization labels or ingestion filters. Dates are simulated source metadata, not Git commit timestamps.

## Software: prepare the local backend

team = software

Accept the Software team invitation and confirm that your account can open the assigned development material. Prepare the local backend by installing the documented Python runtime and using uv to synchronize the repository's locked dependencies.

Create the repository's own virtual environment; do not reuse another project's `.venv`. Configure local database access using the safe environment template and keep generated credentials out of Git. Start the database using that repository's documented command and check that the backend can connect.

Before changing code, run the existing checks so that a pre-existing failure is not confused with a new regression. Make the change on a feature branch and open a reviewed merge request. Ask the Software onboarding buddy if setup instructions and observed behavior disagree.

## HR: prepare the employee's first day

team = HR

Confirm the new employee's start date, role, team contact, and onboarding buddy. Coordinate the account invitation with an administrator. If the person already has an account, use an additional team invitation rather than creating a second identity.

On the first day, check that the employee can sign in, see assigned learning paths, and open their linked source documents. Explain how to resume learning and where to report an access problem. Keep confidential employee records in the designated HR system, outside this demo repository and chatbot conversations.

## Shared: interpret the result

A question about preparing the local backend should retrieve Software setup evidence because it is relevant. The HR section remains in the common pool and can answer a question about first-day coordination. Retrieval must not discard the HR section merely because the caller belongs to Software.

This milestone demonstrates retrieving evidence for a basic saved path. It does not require AI-generated paths or automatic publication. A later ticket supplies those generation workflows.
