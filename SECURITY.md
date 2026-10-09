# Security

## Reporting a vulnerability in Nikto Platform

Report it privately, not as a public issue:
**[Report a vulnerability](https://github.com/hackllc/nikto-platform-support/security/advisories/new)**
(GitHub private vulnerability reporting — only you and Hack LLC can see it).

Useful to include: affected version (console → *Settings → License → Platform
version*), which component (console/UI, API, launcher, a scan engine), what an
attacker gains, and the smallest reproduction you have. A support bundle
(`nikto-launcher support-bundle`) helps if the issue shows up in logs.

We will acknowledge the report, tell you whether we can reproduce it, and let
you know when a fix ships. Please give us a chance to release a fix before
disclosing publicly.

## In scope

The product itself: the console and its API, authentication and the operator
login, the license check, the launcher, and the container images published for
this product. Anything that lets one operator's data, credentials or host be
reached by someone who should not reach it.

## Not in scope

- **Findings a scan reported about your own target.** Those are the output of
  the tool, not a flaw in it. A wrong one is a
  [false positive](https://github.com/hackllc/nikto-platform-support/issues/new/choose).
- The platform scans hosts you point it at, by design, and the operator console
  is trusted-by-design for the operator — "the tool can send attack traffic" is
  not a vulnerability.
- Exposing your own install to an untrusted network. It is meant to run on a
  machine you control; operator login (`AUTH=on`) is the only access control.
- Reports from automated scanners with no demonstrated impact.

## Vulnerabilities in other people's software

If you found a bug in a *target* while using Nikto Platform, that is between you
and that vendor. We cannot report it for you.
