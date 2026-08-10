# Setup

## Requirements
- Docker Desktop (https://www.docker.com/products/docker-desktop/)

## First-time setup

1. Create a GitHub Personal Access Token (classic) at
   https://github.com/settings/tokens/new with the single scope
   **read:packages**. This is your own token — do not share it.
2. Edit `.env` — set `GHCR_USER` to your GitHub username and
   `GHCR_TOKEN` to the token from step 1.
3. Run: `./update.sh`
4. Open http://localhost:3000

## Getting updates

Run `./update.sh` whenever you want the latest version.

## Reporting issues

File issues (you must be signed in to the GitHub account you were granted access with):
https://github.com/hackllc/nikto-platform-support/issues

## Tools
The Nikto Platform is a collection of tools built to work in the most automated fashion possible, and then take exploits further down an automated path. Nikto currently is two tools:

- Nikto — Broad web-server vulnerability scanner -- port of the Perl program. Probes for known misconfigs, outdated software, interesting paths, and insecure headers, then turns hits into findings and host context for the rest of the platform.

- LFIC (Local File Inclusion Commander) — Once a target has a confirmed LFI/path traversal, LFIC turns that bug into a bulk file-retrieval engine. You configure the vulnerable request, pick modules/filesets to pull, and browse/download what came back in a host-scoped file tree (with extractors peeling real file content out of hostile responses).

- Crawler - currently a limited crawl which will:
  - Catalog Javascript included (with outdated/vuln checking)
  - Do API and secret key extraction (via [Titus](https://github.com/praetorian-inc/titus))
  - Planned: Check for indexing on all paths

More tools and automations are planned.

- Bustah — Content-discovery / directory brute for the platform. Wordlist-driven recursion with soft-404 handling, seeding from crawl/Nikto, and results on a shared host sitemap. The platform's inspection engine will run against new results.

- JWT analysis

[ ] `PostMessage()` testing




