# Nikto Platform

Nikto Platform is a web vulnerability scanning platform you run yourself: a web
console, a scan engine, and a database, all in Docker containers on your own
machine. Nothing is sent to us and no scan data leaves your host.

This repository is the **download and support channel**. The product source is
not public — see [Licensing](#licensing).

## Download

Get the launcher for your platform from the
**[latest release](https://github.com/hackllc/nikto-platform-support/releases/latest)**:

| Platform | File |
| --- | --- |
| macOS (Apple silicon) | `nikto-launcher-macos-arm64` |
| macOS (Intel) | `nikto-launcher-macos-amd64` |
| Linux (x86-64) | `nikto-launcher-linux-amd64` |
| Linux (arm64) | `nikto-launcher-linux-arm64` |
| Windows (x86-64) | `nikto-launcher-windows-amd64.exe` |
| Windows (arm64) | `nikto-launcher-windows-arm64.exe` |

The macOS launchers are signed and notarized by Apple. The Windows launchers are
not signed yet, so SmartScreen warns on first run (**More info** → **Run
anyway**).

## Requirements

**Docker Engine 28.0 or later with Compose v2 (2.17+).** The launcher checks both
before starting and tells you what it found. Engine 27 and earlier fail with
`unknown gateway mode isolated`; `docker-compose` 1.x cannot read the compose
file at all.

Give Docker **6 GB** of memory — **8 GB or more** for Headless Browser crawls —
and keep **20 GB** of disk free. The launcher warns when either is short.

- **macOS / Windows**: [Docker Desktop](https://www.docker.com/products/docker-desktop/).
  Raise memory under *Settings → Resources*; the default is usually too low.
- **Kali**: `sudo apt install docker.io docker-compose`
- **Ubuntu 24.04+**: `sudo apt install docker.io docker-compose-v2`
- **Debian, RHEL/Fedora, older Ubuntu**: the distro package is too old — install
  from [docs.docker.com/engine/install](https://docs.docker.com/engine/install/).

On Linux, add yourself to the `docker` group (`sudo usermod -aG docker $USER`,
then log out and back in) or run the launcher with `sudo`.

The per-platform commands are repeated in full on each
[release page](https://github.com/hackllc/nikto-platform-support/releases/latest).

## Install

```bash
chmod +x nikto-launcher-*          # macOS and Linux only
./nikto-launcher-macos-arm64 up
```

`up` creates an install folder, pulls the container images, starts the stack and
opens <http://localhost:3001> when the console is ready. It also prints a
one-time **setup code** — enter it in the console to create your admin account.

Scanning requires a license file. Install it in the console under
*Settings → License*. Until then the console works but new scans are blocked.

Everything the launcher manages — config, database, backups, license — lives in
one folder it names on first run (`--home PATH` or `NIKTO_HOME` puts it
elsewhere; use the same value every time).

## Update

```bash
nikto-launcher update
```

Backs up the database first, then pulls the images pinned in the newer launcher
and recreates what changed. New container images ship with a new launcher, so
download the latest launcher when the console tells you one exists.

`nikto-launcher backup` and `nikto-launcher restore <file>` handle the database
on demand. **Backups contain your scan data and any stored credentials — keep
them private.**

## Documentation

Full documentation ships with the product: open the console and use **Help**.
It covers every command, the scan options, the engines, and troubleshooting.

## Support

Open an issue: **[new issue](https://github.com/hackllc/nikto-platform-support/issues/new/choose)**.
Pick the form that matches (install problem, bug, false positive, missed
finding, feature request); the console's *Report an issue* fills in your version
for you.

**Issues here are public.** Do not paste target hostnames, URLs, IP addresses,
credentials, session tokens or customer data. Describe the shape of the problem
instead ("a 403 on a path that exists"), and redact anything identifying.

`nikto-launcher support-bundle` writes a zip of diagnostics and recent logs with
secrets redacted. Nothing is uploaded — review it, then attach it if you want to.

Found a security issue **in Nikto Platform itself**? See
[SECURITY.md](SECURITY.md) — do not open a public issue.

## What this is for

A collection of scanning tools built to run as automated as possible, and to
carry a confirmed finding further down an automated path:

- **Nikto** — broad web-server vulnerability scanner, a Go port of the Perl
  original. Probes for known misconfigurations, outdated software, interesting
  paths and insecure headers, then turns hits into findings and host context the
  rest of the platform uses.
- **LFIC** (Local File Inclusion Commander) — turns a confirmed LFI or path
  traversal into a bulk file-retrieval engine: configure the vulnerable request,
  pick modules and filesets, then browse and download what came back in a
  host-scoped file tree. Extractors peel real file content out of hostile
  responses.
- **Crawler** — catalogs included JavaScript (with outdated/vulnerable library
  checks) and extracts API and secret keys via
  [Titus](https://github.com/praetorian-inc/titus). Standard and Headless
  Browser engines.
- **MS10-070** — fast scanner and full exploit for the ASP.NET padding oracle,
  replacing PadBuster.
- **Recommendation engine** — surfaces follow-up work, inside the platform or
  out.

Planned: **Bustah** (wordlist content discovery with soft-404 handling, seeded
from crawl and Nikto results), CMS Explorer redux (WordPress first), JWT
analysis, `postMessage()` testing, path indexing checks.

## Legal

Scan only hosts you own or have written permission to test. Running this against
systems you are not authorized to test is illegal in most jurisdictions and is
your responsibility alone.

## Licensing

Nikto Platform is proprietary software. Copyright © 2026 Hack LLC. All rights
reserved. This repository distributes the launcher binary and hosts support
issues; it does not contain the product source. Your use is governed by the
end-user license agreement shipped with the product (console → *Help → EULA*).
