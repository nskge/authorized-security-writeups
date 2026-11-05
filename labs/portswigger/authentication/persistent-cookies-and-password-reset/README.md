# Persistent cookies and password reset poisoning

[← Authentication](../README.md)

> PortSwigger study notes · Partial reconstruction · Exercises recorded as completed

## Context

I studied account recovery and persistent login mechanisms in authorized PortSwigger exercises. The original lab names, full requests, and exact solutions were not retained, so this is a study record rather than a reproducible walkthrough.

## Recorded work

- Examined a `stay-logged-in` cookie containing password-derived information and an MD5 hash.
- Studied offline password cracking within an authorized exercise.
- Practiced password reset poisoning, looking at how request-controlled data can influence the URL sent for account recovery.

## Lessons

A predictable persistent-login construction can expose password-derived material to offline guessing. Encoding a value does not make it secret, and a fast hash is not an adequate password-storage mechanism.

For password recovery, trusting request headers such as `Host` when constructing reset links can point users toward an untrusted origin.

## Follow-up checklist

These are review recommendations, not additional results from my session:

- Generate reset URLs from a server-controlled canonical origin.
- Check token expiration, account binding, single use, and invalidation after use.
- Review persistent-login token generation and revocation.
- Check whether account-recovery responses reveal registered users.

## Evidence limits

No passwords, cookies, tokens, or reconstructed session captures are published. Individual lab titles and exact solution steps remain unconfirmed.

Source: personal Notion study notes, translated and condensed.
