# Security Policy

This file is the org-wide default security policy for [yey-boats](https://github.com/yey-boats)
repositories. GitHub falls back to the copy in this `.github` repo for any repo (e.g. `midl`)
that doesn't ship its own `SECURITY.md`.

## Supported versions

These are source-available hobby/early-stage projects without a formal LTS policy. Security
fixes are applied to the `main` branch of the affected repo; there are no maintained release
branches at this time.

## Reporting a vulnerability

Please **do not** open a public GitHub issue for security vulnerabilities.

<!-- TODO: confirm reporting address with operator -->
Instead, report it privately by emailing **security@yey.boats** with:

- A description of the vulnerability and its potential impact.
- Steps to reproduce (proof-of-concept code, requests, or configuration if applicable).
- The affected repository and commit/version, if known.

We'll acknowledge your report as soon as we can and follow up with next steps, including an
expected timeline for a fix. Please give us a reasonable amount of time to address the issue
before any public disclosure.

## Scope

This policy applies to all repositories under the `yey-boats` GitHub organization, including
firmware (`instruments`), the dashboard language (`midl`), the SignalK plugin
(`Instruments-manager`), the simulator (`simulator`), and the private automation bot
(`navigator-tg-bot`).
