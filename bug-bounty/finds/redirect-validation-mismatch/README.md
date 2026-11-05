# Redirect validation mismatch — anonymized report

[← Findings](../README.md)

> Authorized bug bounty assessment · Anonymized summary · Historical status: triaged / open

## Summary

I reported an open redirect in an authorized bug bounty program. The application validated one destination input while the eventual navigation used another, allowing the intended destination restriction to be bypassed.

This public summary omits the organization, industry, domains, endpoints, original parameter names, report identifier, exact dates, and reproduction payload.

## Root cause

Validation and navigation did not use the same effective destination. A check on one input therefore did not protect a separate input used later in the flow. The handling of relative destinations also required more precise URL validation.

## Reported result

My private notes record the report as triaged / open, with a Low rating and CWE-610 mapping at the time of that observation. These are historical report details, not confirmation of the current status, a fix, final acceptance, or a bounty payment.

The observed issue was an unintended redirect after an authentication flow. No credential theft, account takeover, or additional impact chain is claimed.

## Lessons and remediation

Validate the actual destination used for navigation after parsing and normalization. Prefer server-controlled destinations or a strict allowlist, and avoid divergent sources of truth across validation and redirect handling.

External redirects in authentication flows can support misleading navigation, but any stronger impact claim requires separate evidence.

## Evidence and publication limits

This is an anonymized narrative based on private notes, not a public reproduction guide. No vendor-approved disclosure or remediation status is established by the source record. Original evidence and report references remain private.
