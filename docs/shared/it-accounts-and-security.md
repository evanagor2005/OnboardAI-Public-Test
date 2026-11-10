# Shared: IT accounts and security

Document type: realistic sample document for the fictional Cedar Works demo company.
Classification: company-wide shared content.
Document owner: IT service desk lead.
Created: 2026-11-06 (simulated source date).
Last updated: 2026-11-09 (simulated source date).
Review status: AI-drafted; pending Evan's review for accuracy and realism.

This is synthetic evaluation content. Account controls, device settings, and support procedures are fictional Cedar Works examples, not adopted company policy or a real system configuration. Dates are simulated source metadata, not Git commit timestamps.

## Activate an employee account

This guide covers the everyday accounts and devices used by both HR and Software employees. IT manages company sign-in, managed laptops, and network access. HR confirms the employee's role and start date; the manager requests the access needed for that role. An approved request does not grant access until the responsible administrator provisions it.

Use the account invitation supplied through the established onboarding process. Verify an unexpected invitation with IT using the contact route in the onboarding packet before opening it. Set up your own account; never sign in as the manager or onboarding buddy. If an existing onboarding account already belongs to you, ask the administrator to add the appropriate team membership rather than creating another identity.

Single sign-on (`SSO`) lets one company identity access participating applications. It does not automatically authorize every application or record. If a private HR tool or engineering repository is unavailable, request the specific permission through the service desk. Do not ask a colleague to share their login or export restricted records as a workaround.

## Set passwords and enroll MFA

For services that use passwords, the sample Cedar Works rule is a unique password of at least 16 characters, generated and stored in the approved password manager. Do not reuse a personal password or store passwords in a shared document. IT does not request a password, a recovery code, or a one-time sign-in code through chat or email.

Enroll multi-factor authentication (`MFA`) during account activation. Use a company-supported passkey or security key where available; otherwise use the authenticator method offered by IT. Register a second approved recovery method when supported and keep recovery codes in the approved protected storage. Do not store the only recovery method on the same device it is intended to recover.

Approve an MFA prompt only when you initiated the sign-in and the displayed details match your action. Deny an unexpected prompt and report it to IT promptly. If a phone or security key is lost, contact the service desk through the alternate route in the onboarding packet. IT verifies identity using its established recovery procedure before replacing a factor; a manager's ordinary email request alone is insufficient.

## Prepare a managed laptop

On receipt, confirm the laptop's asset label with IT and complete device enrollment before accessing company information. IT verifies full-disk encryption, endpoint protection, automatic updates, and a screen lock that activates after five minutes of inactivity. Use a standard user account for routine work and request any approved elevated installation through IT.

Install software from the managed catalog or an IT-approved source. Do not disable endpoint protection or device management to complete a setup task. Keep company records on approved storage, lock the screen when stepping away, and avoid shared family accounts or personal cloud synchronization. Report a missing compliance check to IT rather than assuming the laptop is ready.

## Connect through the VPN

The virtual private network (`VPN`) provides an approved route to designated internal resources when working remotely. Install the managed VPN client, sign in with your own company identity, and complete MFA when prompted. Confirm the client reports an active connection before opening a resource that requires it.

A VPN connection does not grant application permissions. For a connection failure, record the approximate time, client error code, and whether ordinary internet access works. For an application denial after a successful connection, identify the application and requested task so IT can route the access request. Do not send diagnostic bundles containing credentials or private employee records in a shared chat, and do not bypass certificate warnings or change network controls independently.

## Protect credentials and report a problem

Keep passwords, access tokens, and recovery codes out of repository files, screenshots, and chatbot conversations. This applies to HR portal access as well as engineering tools. For application signing keys, environment variables, CI credentials, and a secret committed to Git, follow the Software guide to [secure coding and secrets](../software/secure-coding-and-secrets.md); employee password recovery and lost MFA devices go to IT.

Report a lost laptop, suspected phishing, an unexpected MFA prompt, or a possible account compromise immediately through the security reporting channel. If the company portal is inaccessible, use the alternate contact route supplied during onboarding. Give the affected device or service, approximate time, and a safe description without repeating a suspected secret. IT and the security owner coordinate containment and any session revocation; do not wipe a device or erase evidence independently.

## Knowledge check

Does SSO or an active VPN connection grant access to every application? What should an employee do with an unexpected MFA prompt? Which guide covers an application secret committed to Git, and who handles employee account recovery?
