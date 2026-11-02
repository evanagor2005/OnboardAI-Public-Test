# APIs

Document type: realistic sample document for the fictional Cedar Works demo company.
Classification: team-specific; Software.
Created: 2026-10-28 (simulated source date).
Last updated: 2026-11-02 (simulated source date).

This synthetic guide describes Cedar Works application API conventions. It is not a real company's security policy or an externally supported contract. Dates are simulated source metadata, not Git commit timestamps.

## Define an API contract

Before implementing an endpoint, identify the client and workflow it supports, the data it reads or changes, and the expected success and failure cases. Keep the contract in the service's API documentation or schema so clients and server code can be reviewed against the same behavior.

Use resource-oriented URLs and plural nouns for collections. Use HTTP methods consistently: GET reads, POST creates or starts an operation, PUT replaces a resource, PATCH changes selected fields, and DELETE removes a resource when the contract permits it. Return JSON with an explicit content type, and use standard HTTP status codes to describe the result.

## Authenticate and authorize requests

Endpoints that return employee or company information require an access token from the approved identity service. Send it in the `Authorization: Bearer` header over HTTPS. Never put credentials in a URL, commit them in a sample configuration, or include token values in request logs and error reports.

Authentication establishes who made the request; authorization checks whether that identity can perform the operation on the requested resource. Enforce both checks on the server for every protected route. Do not rely on a hidden button or a client-supplied team name as proof of permission. Return a consistent denial response without revealing records the caller cannot access.

## Version changes deliberately

Publish the major API version in the URL, such as `/api/v1/projects`. Keep a version compatible when adding optional response fields or new endpoints. A change that renames or removes a field, changes its meaning, or alters required request data needs a new major version and a migration period for clients.

When retiring an endpoint, document the replacement and the end-of-support date. Give client owners time to upgrade, monitor use of the old version, and remove it only through the announced release process. Do not silently change the meaning of an existing field to fit new behavior.

## Return actionable errors

Use one JSON error envelope across endpoints. Include a stable machine-readable `code`, a brief safe `message`, and a `request_id` that support staff can use to find a sanitized server log entry. For validation failures, include field-level details in a predictable object. Do not return stack traces, SQL text, access tokens, or private record contents.

Choose status codes that distinguish malformed input, missing resources, authentication failure, permission denial, conflict with current state, rate limiting, and unexpected server failure. Clients should branch on the stable code or status, not parse the human-readable message. A retryable response should make its retry behavior clear, including any `Retry-After` value.

## Test API behavior

Write request tests for successful responses, invalid input, missing authentication, insufficient permission, and important boundary cases. Assert the status code, response shape, and side effects so a route cannot pass by returning the right JSON while changing the wrong data. Use isolated test records and credentials generated for the test environment.

Keep contract examples and client fixtures synchronized with the endpoint. Exercise authorization rules with more than one user or team when access depends on ownership or membership. Do not send tests to production or use real employee data as test fixtures.

## Release an API change

Run the service checks and review the API contract with the client owners before release. Announce breaking changes with a migration guide and verify dashboards or sanitized request metrics for old-version usage during the compatibility period. Preserve a request identifier in diagnostics so a failed client call can be investigated without recording its secrets.

## Knowledge check

Which part of an API request proves identity, and which part checks access? How should a client tell a retryable error from a validation error? When does a contract change need a new major version?
