# Berlim — anonymous FTP, Base64, and CMS enumeration

[← CTFs](../README.md)

> University challenge · VirtualBox lab · Partial reconstruction · Revisit

## Environment

I worked on a university challenge VM in VirtualBox, with FTP and HTTP services on a lab network.

## Recorded observations

- The FTP service was identified as vsFTPd 3.0.5 and allowed anonymous read access.
- A directory contained `mail.txt`, with CMS-related information encoded in Base64.
- The HTTP service was identified as Apache 2.4.58, exposing paths including `/css/`, `/images/`, `/js/`, and `/site/`.
- Decoding the clue pointed toward administrative access to the CMS. The password is omitted.
- I recalled JavaScript under `/site/` consuming a parameter and considered whether it could lead to SSRF.

## Results and uncertainty

The recovered notes support enumeration and discovery of the encoded clue. The JavaScript filename, parameter, request, and response were not retained.

SSRF and a possible chain to remote code execution remain hypotheses. Neither a confirmed SSRF-to-RCE chain nor a recovered flag is claimed here.

## Lessons

Base64 is encoding, not encryption: an anonymously accessible file remains exposed even when its contents are encoded.

Demonstrating SSRF requires evidence of a server-side request to a selected destination. Demonstrating code execution requires separate evidence.

## Next session

Recover the original lab material, record sanitized request/response pairs, and validate each suspected step independently.

Source: personal Notion lab journal, translated and condensed.
