### Authentication

The preferred authentication method is HTTP Basic Authentication.

In addition to Basic Authentication there is also an HTTP Cookie based mechanism. Cookie Authentication is more suitable for Web Browser based applications where Basic Authentication may impose Browser specific limitations. 

At Cookie Authentication the user authenticates via the /login URL. This will set a session specific HTTP Cookie in the Browser. This Cookie will be included in all subsequent requests until the user terminates the session via the /logout URL. 

A Cookie is created by the specific server instance serving the session. The session does also have a limited validity in time. A failed server or a session expiry will require a new authentication of the user. This is not a big problem for a Web Browser based application where the user simply logs in again. 

Unattended (M2M) communication should use Basic Authentication to avoid the scenario above.

