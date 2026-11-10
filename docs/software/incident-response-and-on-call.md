# Software: incident response and on-call

Document type: realistic sample document for the fictional Cedar Works demo company.
Classification: team-specific; Software.
Document owner: Platform on-call lead.
Created: 2026-11-05 (simulated source date).
Last updated: 2026-11-09 (simulated source date).
Review status: AI-drafted; pending Evan's review for accuracy and realism.

This is synthetic evaluation content. Severity levels, response targets, and operating procedures are fictional Cedar Works examples, not a real support commitment or production runbook. Dates are simulated source metadata, not Git commit timestamps.

## Prepare for an on-call shift

The weekly rota identifies a primary responder, a backup responder, and an escalation lead. Before taking a shift, verify access to the paging system, operational dashboards, restricted incident records, and approved runbooks. Confirm the handoff time with the outgoing responder and test the paging route without generating a real incident.

The handoff summarizes active incidents, recent releases, outstanding mitigations, and risky scheduled work. Include owners and next checks, not passwords or raw employee data. If required access is missing, notify the on-call lead before accepting sole responsibility for the shift.

## Classify impact and acknowledge alerts

An incident is an unplanned loss or material degradation of a service, or a suspected security event requiring coordinated response. The responder assigns an initial severity from observed impact and revises it when evidence changes. A suspected exposure of sensitive data follows the security route immediately even if availability is normal.

| Severity | Example impact | Acknowledgment target | Progress update target |
| --- | --- | --- | --- |
| `SEV1` | Broad outage, a critical workflow unavailable, or suspected sensitive-data exposure | Within 5 minutes, at any time | Every 30 minutes |
| `SEV2` | Significant partial degradation with a safe workaround | Within 15 minutes, at any time | Every 60 minutes |
| `SEV3` | Limited nonurgent defect without material service interruption | By the end of the next business day | At agreed milestones |

These are internal response targets. They do not promise a resolution time or create a customer service-level agreement (`SLA`). Any actual SLA must be checked in the applicable support contract. A service-level objective (`SLO`) is an internal reliability goal measured by a service-level indicator (`SLI`), such as request success rate or latency; an SLO breach is evidence for triage, not a substitute for assessing impact.

Acknowledge a page in the paging system and begin assessment. If no acknowledgment is recorded within the severity target, page the backup; if the backup does not respond within five more minutes, escalate to the on-call lead. Record escalation times so ownership is clear. Acknowledgment means someone has taken responsibility, not that service is restored.

## Establish incident roles and communications

For `SEV1`, open a restricted incident record and assign an incident commander, technical lead, and communications owner. One person may initially hold several roles, but the commander should delegate as responders arrive. For `SEV2`, the primary responder coordinates until additional roles are needed. Track `SEV3` work through the normal engineering queue with an owner.

The commander coordinates decisions and priorities; the technical lead directs investigation and mitigation; the communications owner sends the scheduled updates. Record impact, start time, current hypothesis, actions, and the next update time. Send an update even when the cause remains unknown. Use UTC in the incident timeline to avoid ambiguity across responders' locations.

Keep operational details in the restricted record. Broad status notices describe affected functions, workarounds, and the next update without employee records, exploit details, credentials, or unverified explanations. If ordinary reporting routes are unavailable, use the alternate contact route listed in the rota.

## Investigate and mitigate safely

Check service health, recent releases, dependency status, and error trends. Correlate sanitized logs with `request_id` and the deployed `RELEASE_SHA`; do not paste complete request bodies or authorization headers into the incident record. Separate observed facts from hypotheses, and record each intervention with its time and result.

Prefer the smallest reversible mitigation, such as reducing traffic to a failing component or disabling a nonessential feature through an approved control. Roll back an application artifact only after checking schema and configuration compatibility under [deployment and releases](deployment-and-releases.md). Incident urgency does not bypass the Tuesday-only production migration rule. Escalate recovery options rather than making an unreviewed schema change.

For suspected credential exposure, involve the security owner and follow the [secrets exposure process](secure-coding-and-secrets.md). Preserve relevant evidence in approved restricted storage and avoid copying a suspected secret into additional systems. Authorized platform operators assess any backup restore; recovery point objective (`RPO`) and recovery time objective (`RTO`) discussions must use the service's documented targets and actual recovery evidence, not assume zero data loss.

## Verify recovery and learn from the incident

Confirm affected journeys work, error and latency signals have stabilized, and queued work is recovering. Observe recovery for at least 30 minutes and through a representative affected background-job cycle, whichever takes longer. The commander confirms recovery and the communications owner publishes a safe resolution update. Keep follow-up owners visible during the next on-call handoff.

For `SEV1` and `SEV2`, schedule a blameless postmortem within five business days of recovery. Document impact, timeline, contributing conditions, detection gaps, and what helped. Assign specific prevention or response actions with owners and due dates. Do not declare an uncertain root cause as fact or include sensitive records in the widely shared summary.

## Knowledge check

How do SLA, SLO, and SLI differ? What happens when a primary responder misses the acknowledgment target? Which checks are needed before declaring recovery or rolling back a release?
