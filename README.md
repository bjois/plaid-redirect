# plaid-redirect

Static OAuth landing page for Plaid Link, used as the registered redirect URI by
the `plaid-balances` skill.

## Registered redirect URI

```
https://bjois.github.io/plaid-redirect/oauth.html
```

Must match exactly: HTTPS, no trailing slash, no query parameters, no fragment.
Subdomain wildcards are allowed by Plaid; path wildcards are not.

## Why this exists

Plaid cannot support OAuth institutions (Capital One, CIT Bank) without a
registered HTTPS redirect URI. Sandbox permits `http://localhost`; a Trial plan
in production does not, which is why this page is hosted here rather than served
locally.

## What it contains

Nothing sensitive. The page holds no credentials, tokens, or account data. It
reads `oauth_state_id` from the query string and, if a link token is present in
this origin's `localStorage`, reinitializes Link to complete the flow.

In the normal desktop flow Plaid uses a popup and returns control to the
originating window, so this page is never loaded. It is a fallback, plus a
requirement that Capital One checks for.

## Deploying changes

Serve from the `main` branch, repository root. GitHub Pages rebuilds on push.
