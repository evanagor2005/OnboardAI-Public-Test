# Shared: new-hire checklist for managers

Document type: realistic sample document for the fictional Cedar Works demo company.
Classification: company-wide shared content.
Document owner: HR onboarding coordinator and Software engineering lead.
Created: 2026-11-07 (simulated source date).
Last updated: 2026-11-09 (simulated source date).
Review status: AI-drafted; reviewed by Evan Agor for accuracy and realism and approved for the synthetic evaluation corpus.

This is synthetic evaluation content. Timing, responsibilities, and checklist items are fictional Cedar Works examples, not adopted company policy or statements of legal requirements. Dates are simulated source metadata, not Git commit timestamps.

## Coordinate one onboarding plan across HR and Software

The hiring manager coordinates the checklist for each employee, whether the employee joins HR or Software. HR owns employment paperwork and shared orientation; IT provisions managed devices and company accounts; the Software lead owns engineering access and technical preparation for roles that need it. The onboarding buddy helps the employee learn but does not approve access or collect confidential paperwork.

Start preparation at least seven business days before the agreed start date when practical. For a shorter lead time, identify incomplete tasks and responsible owners with HR instead of marking them complete. Record task status, owner, target date, and a reference to the appropriate private system. Keep identity documents, bank details, medical information, passwords, and token values out of the checklist and company chatbot.

## Before the start date: HR paperwork and employee details

- Confirm the accepted role, team, work arrangement, start date, manager, and onboarding buddy with HR. Report a change promptly so invitations and equipment match the current plan.
- Ask HR to send the required employment, identity-verification, tax, and payroll forms through the designated private HR systems. HR confirms the applicable requirements and deadlines; the manager tracks completion status without downloading the documents.
- Confirm HR has prepared the benefits invitation and welcome schedule. Eligible new hires have 30 calendar days from their start date to submit health coverage elections under the [sample benefits process](../hr/benefits-enrollment.md); first-week access checks do not replace that deadline.
- Request company identity, email, collaboration tools, and a managed laptop from IT. Identify required applications by role and the responsible approvers. Ask IT to verify an existing identity before creating a new one.
- Arrange any equipment or accessible setup needs through the private HR and IT process. Share only the practical arrangements needed for delivery and readiness.

HR schedules confidential paperwork follow-up directly with the employee. The manager should escalate a missing status to HR rather than collect a copy of the employee's form through ordinary email.

## Before the start date: Software accounts and development access

- For a role that needs engineering tools, identify the required source repositories, development services, issue tracker, and CI dashboards. Request the minimum role-appropriate permissions and record each system owner's approval.
- Have administrators prepare invitations for the start date. Do not send a coworker's credentials or request production secrets to make setup faster. Production access is a separate decision and is not part of the default new-hire account bundle.
- Assign a Software buddy to verify the setup material and prepare synthetic development fixtures. Use the documented Python runtime, uv dependency workflow, and per-repository virtual environment from [backend development](../software/backend-development.md).
- Confirm a separate local PostgreSQL environment and safe configuration template are available under the [database guidance](../software/databases.md). Development setup must not require production records, production database credentials, or downloaded backups.

For an HR employee who does not need engineering tools, record those tasks as not applicable with a brief role-based reason. An HR employee collaborating on technical work may need selected engineering access; an employee's team name alone neither grants nor rules out that access.

## First day: sign-in, laptop, and learning access

- Have the employee activate their own account, enroll MFA, and verify the managed laptop with IT using [IT accounts and security](it-accounts-and-security.md). IT confirms device compliance and any required VPN connection before restricted resources are used.
- Ask the employee to sign in and demonstrate access to the appropriate applications without revealing passwords or recovery codes. Route failed sign-in, network, and permission checks to the responsible administrator.
- Confirm the employee can see the assigned onboarding learning path, resume a step, and open its linked source documents. If the onboarding identity already exists, invite it to the appropriate team rather than creating a duplicate account.
- Introduce the manager, HR contact, buddy, and support routes, including the alternate contact method for a locked account. Explain where to report a broken source link and where confidential questions belong.

Application access, team membership, administrator appointments, and learning-path assignments are separate actions. Verify the specific action needed rather than assuming that a successful sign-in completes every access task.

## First week: HR work and engineering readiness

For HR roles, confirm the employee can find the private employee systems and understands the handling of confidential records. Employee-record handling training must precede independent access to sensitive personnel records. Payroll access additionally requires payroll controls training and Payroll coordinator approval. Interview training must be complete before participating in any interview, including a supervised interview.

For Software roles, the buddy checks that the employee can synchronize locked dependencies, connect to the isolated local database, start the application, and run its existing configuration checks. Use a small change with synthetic data to introduce the [Git and code review workflow](../software/git-workflow-and-code-review.md). The manager or system owner resolves missing permissions; the buddy must not lend credentials or copy a private `.env` file.

For both teams, reserve working time for required training. Core courses are due within 10 business days of the start date under [required training and compliance](../hr/required-training-and-compliance.md). Verify course records in the learning system; a completed onboarding path step does not substitute for course completion. A newly appointed manager also has a 30-calendar-day deadline for manager training, with the supervision arrangements defined in that guide.

## End of the first week: review blockers and hand off

Meet with the employee and buddy to check what works, which tasks remain open, and who owns each blocker. Confirm that HR forms and benefits access have been checked through their private systems, technical access fits the role, and remaining training has scheduled time. Mark only verified tasks complete; first-week closure does not declare future enrollment or training deadlines satisfied.

The employee's learning progress remains individual even when colleagues use the same source documents. A source freshness warning calls for checking the current guidance; it does not revoke completed onboarding. Follow the [employee onboarding guide](../hr/employee-onboarding.md) for continuing progress support and give the employee a clear next check-in date.

## Knowledge check

Which onboarding tasks belong to HR, IT, and the Software lead? What must happen before independent personnel-record access or interview participation? How should a manager handle an existing identity, an unresolved access problem, or a training deadline beyond the first week?
