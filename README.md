# Example angular-oauth2-oidc and IBM AppID with AuthGuard


## ⚠ Third-party Cookies

**TLDR 👉 See [my "SPA Necromancy" blogpost for all options and workarounds known to me](https://infi.nl/nieuws/spa-necromancy/).**

Browser vendors are implementing increasingly strict rules around cookies.
This is increasingly problematic for SPA's with their Identity Server on a third-party domain.
Most notably **problems occur if the "silent refresh via an iframe" technique is used**.

This repository uses that technique currently.
This will fire up an iframe to load an IDS page with `noprompt`, hoping cookies get sent along to so the IDS can see if a user is logged in.

[Safari will block cookies from being sent](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/), prompting a leading OAuth/OpenID community member to write "[SPAs are dead!?](https://leastprivilege.com/2020/03/31/spas-are-dead/)".
In fact, if you fire up this sample repository on `localhost`, which talks to `demo.duendesoftware.com` (another domain!), and use it in Safari: you will notice that the silent refresh technique already fails!

## Features


This demonstrates:

- Use of **the Code+PKCE Flow** (so no JWKS validation)
- Async but mandatory bootstrapping (via an `APP_INITIALIZER`) before the rest of the app can run
- Modules (core, shared, and two feature modules)
- An auth guard that forces you to login when navigating to protected routes
- An auth guard that just prevents you from navigating to protected routes
- Asynchronous loading of login information (and thus async auth guards)
- Using `localStorage` for storing tokens (use at your own risk!)
- Loading IDS details from its discovery document
- Trying refresh on app startup before potientially starting a login flow
- OpenID's external logout features
