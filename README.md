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
