### Authentication

The preferred authentication method is HTTP Basic Authentication.

In addition to Basic Authentication there is also an HTTP Cookie based mechanism. Cookie Authentication is more suitable for Web Browser based applications where Basic Authentication may impose Browser specific limitations. 

At Cookie Authentication the user authenticates via the /login URL. This will set a session specific HTTP Cookie in the Browser. This Cookie will be included in all subsequent requests until the user terminates the session via the /logout URL. 

---
__TODO:__ Write a paragraph about cookies, load balancing and token expiry.

