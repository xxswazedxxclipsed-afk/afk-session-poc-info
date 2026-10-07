# AFK Session POC

AFK Session POC is a local proof of concept for a user-controlled Minecraft: Java Edition session manager. Its purpose is to test whether a legitimate account owner can authorize a lightweight headless client, connect it to a server they are permitted to join, and disconnect it automatically at a fixed deadline.

This application is independent and is not an official Mojang Studios, Microsoft, Xbox, Discord, or Minecraft product or service.

## Authentication and account safety

- Users authenticate only on Microsoft's official sign-in page using the OAuth device authorization flow.
- The application never asks for or stores a Microsoft password.
- It uses its own Microsoft Entra public-client application ID.
- It verifies that the signed-in account has a usable Minecraft: Java Edition profile and entitlement before attempting a connection.
- Authentication tokens are encrypted at rest and are never placed in queue jobs, browser storage, URLs, Discord messages, or application logs.
- Users can stop sessions, unlink their accounts, and revoke the application's Microsoft access.

## Intended API access

The application needs delegated Microsoft/Xbox authentication and Minecraft Services access to:

1. authenticate the account owner through Microsoft;
2. obtain the account's Minecraft: Java Edition authentication token;
3. verify the Java profile and entitlement; and
4. authenticate a headless Java protocol client to an online-mode server selected by the account owner.

The proof does not distribute Minecraft game files or provide access to accounts that do not own the required game entitlement.

## Acceptable-use boundaries

The application does not bypass authentication, licensing, multiplayer restrictions, bans, anti-cheat systems, anti-bot systems, anti-AFK protections, CAPTCHAs, or server access controls. A server rejection is treated as a failure. Users must have permission to join and use an idle client on the destination server.

The local proof is intentionally limited to one worker while authentication and a real permitted server connection are tested. Payments and commercial operation are not part of the proof of concept.

## Data used by the local proof

The proof stores only the data required to operate and audit a requested session: an internal user identifier, Minecraft profile UUID and username, encrypted authentication cache, server address and port, session status, fixed expiration time, connection timestamps, retry count, and sanitized failure reason.

Microsoft passwords, raw tokens, cookies, encryption keys, and session secrets are not logged. PostgreSQL and Redis are not exposed publicly by the local Docker configuration.

## Contact

Contact details are supplied privately through Microsoft's official AppID review form rather than published in this repository.
