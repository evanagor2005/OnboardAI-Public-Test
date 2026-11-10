# Software: secure coding and secrets

Document type: realistic sample document for the fictional Cedar Works demo company.
Classification: team-specific; Software.
Document owner: Software security coordinator.
Created: 2026-11-06 (simulated source date).
Last updated: 2026-11-09 (simulated source date).
Review status: AI-drafted; pending Evan's review for accuracy and realism.

This is synthetic evaluation content. Controls and configuration names are fictional Cedar Works examples, not a complete security standard or a real deployment configuration. No credential values are included. Dates are simulated source metadata, not Git commit timestamps.

## Validate inputs and enforce authorization

Treat request bodies, URL parameters, uploaded files, and external service responses as untrusted input. Validate structure, types, length, and permitted values at the server boundary. Use framework-supported parameterized queries rather than composing SQL from input, and apply output escaping appropriate to the destination. A validation success does not establish that the caller has permission to act.

Authentication identifies the caller; authorization checks the requested operation and resource. Follow the [API conventions](apis.md) on every protected route. Verify ownership and membership on the server rather than trusting a client-supplied employee ID or team name. Include tests for a second synthetic user who must not access the first user's records.

Cookie-authenticated browser workflows need the framework's cross-site request forgery (`CSRF`) protections. Review cross-origin resource sharing (`CORS`) settings against the intended frontend origins; a permissive CORS response does not grant authorization. Use maintained framework controls rather than custom cryptography or a new token format.

## Keep configuration separate from credentials

The following environment variable names are examples for recognizing configuration in source material. Confirm the actual names and supported values in the relevant service's configuration documentation before making a change.

| Example name | Purpose and handling |
| --- | --- |
| `APP_ENV` | Identifies the intended environment; it does not grant permissions |
| `DEBUG` | Controls diagnostic behavior; public production responses must not expose debug output |
| `DATABASE_URL` | Database connection configuration that may contain credentials; treat its full value as a secret |
| `DJANGO_SECRET_KEY` | Application signing secret; restrict access and plan rotation with the service owner |
| `ALLOWED_HOSTS` | Expected application hostnames; configure explicitly for the deployment |
| `TEST_DATABASE_URL` | Disposable test database destination; never point it at a shared or production database |

Variable names alone are not secret values. A configuration example may document names and safe nonsecret defaults, but must not contain usable credentials. Production configuration must fail clearly when a required secret is missing rather than falling back to a shared sample secret or enabling debug output.

## Store and deliver secrets safely

Local developers use the safe example environment file and keep generated local credentials in an ignored `.env` file, as described in [backend development](backend-development.md). An ignore rule prevents accidental tracking of new files; it does not remove a file or secret already committed. Inspect staged changes and review scanner findings before pushing.

Shared and production secrets are stored in the approved secret manager and delivered only to the workload or deployment job that needs them. CI/CD means continuous integration and continuous delivery in this sample workflow; production promotion still requires approval. Use short-lived workload identities where supported, restrict job permissions, and keep untrusted PR jobs away from production credentials. Log masking is a secondary control, not permission to print a secret.

Never put private credentials in frontend bundles, container layers, build arguments, committed fixtures, or chatbot messages. Frontend build-time variables are visible to users of the delivered application; a name that sounds private does not make a browser-delivered value secret. Use the server for operations that require private service credentials.

## Review dependencies and diagnostic output

Change dependency manifests and lockfiles together. Review package provenance, maintenance status, and vulnerability findings before merging an update. A software bill of materials (`SBOM`) identifies included components; it does not by itself prove that an artifact is safe. Security findings that block a release need a fix or a documented decision by the security owner before the gate can pass.

Logs can include stable event codes, a sanitized `request_id`, and nonsecret release identifiers. Do not log access-token values, complete `Authorization` headers, full database connection strings, private employee records, or request bodies by default. Apply redaction before output reaches logs or CI artifacts. Return safe API errors without stack traces or SQL text, and retain detailed diagnostics only in authorized operational systems.

## Respond to a possible secret exposure

If a usable secret may have reached Git, a log, an artifact, or an unauthorized recipient, notify the security owner through the restricted reporting route immediately. Treat it as potentially compromised while the owner assesses impact. Provide the affected system, location, and approximate time without repeating the value.

The authorized owner revokes or rotates the affected credential, updates dependent workloads, and verifies that the old credential no longer works where revocation is supported. Signing-key rotation requires a service-specific plan for existing sessions or signatures; do not replace it blindly. Assess access logs and coordinate the [incident response process](incident-response-and-on-call.md) for suspected misuse or sensitive-data exposure.

Removing a value from the current file is insufficient because earlier commits, cached artifacts, or logs may retain it. After containment, coordinate repository-history cleanup and artifact removal with the security owner and maintainers. History rewriting can disrupt collaborators and cannot guarantee deletion from existing copies. Verify the replacement is delivered securely and record follow-up prevention work without storing either secret value in the report.

## Knowledge check

Why does successful input validation not prove authorization? Which environment variable examples may carry credentials? What should happen before repository-history cleanup when a usable secret is exposed?
