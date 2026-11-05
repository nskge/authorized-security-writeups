# Orion — Craft CMS and privilege-escalation notes

[← Hack The Box](../README.md)

> Linux lab · Partial reconstruction · Revisit

## Environment

My notes describe work on the Hack The Box machine Orion, with a Craft CMS application.

## Recorded progression

1. Identified Craft CMS and investigated a pre-authentication remote-code-execution issue. The notes associate this investigation with CVE-2025-32432.
2. A module reported the target as vulnerable, but an initial attempt did not automatically establish a session.
3. Later notes record shell access and inspection of application configuration, including an `.env` file and references to MySQL credentials.
4. The notes also mention studying `inetutils telnetd` 2.7 and CVE-2026-24061, with an earlier report of reaching root.

The CVE associations and version above are preserved as claims from my notes, not independently verified identification of the machine's exploit chain.

## What the record supports

The journal reports shell access and root completion, but the exact requests, commands, output, and transition between foothold and privilege escalation have not been recovered. I cannot present this as a verified end-to-end walkthrough.

## Lessons

A positive vulnerability check is distinct from successful exploitation. Delivery, connectivity, shell establishment, and effective privileges each need evidence.

Application configuration can reveal sensitive information after a foothold; credentials should remain outside published notes.

## To revisit

Recover the exact software versions, module output, initial-shell evidence, escalation mechanism, and privilege verification. No flags, credentials, or invented commands are included.

Source: personal Notion lab journal, translated and condensed.
