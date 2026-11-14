# CLAUDE.md - cateim.github.io

Single source of truth for agents and humans working on this repository.
`AGENTS.md` only points here.

## Overview

The GitHub Pages user site of the `CaTeIM` account, served at
`https://cateim.github.io/`. It holds two things: a one-page list of projects
(`site/index.html`) and the Google Search Console verification file that
proves `cateim.github.io` belongs to this account. Google Cloud projects need
that proof to list `cateim.github.io` as an authorized domain on their OAuth
consent screen (DriveSync's, first).

Project pages are not here: each project repository publishes its own site
under its own path (`CaTeIM/drivesync` serves `/drivesync/`).

## Stack

Plain HTML with inline CSS, no build and no dependencies. Published by
GitHub Actions (`actions/upload-pages-artifact` and `actions/deploy-pages`);
the repository's Pages source is "GitHub Actions".

## Structure

```text
site/                        everything published: index.html, and google<token>.html once added
.github/workflows/pages.yml  publishes site/ on a push to master that touches it
```

## Deploy

Push to `master`. The workflow publishes `site/`, and the site is live about
a minute later. Check with `curl -sI https://cateim.github.io/`.

## Gotchas

- **Never remove or rename the Search Console file** (`site/google<token>.html`).
  Search Console keeps checking it, and once it is gone the ownership of
  `cateim.github.io` lapses, and with it the authorized domain of every
  Google Cloud project that uses it.
- Never create a folder in `site/` named like a project repository
  (`site/drivesync/`): that path belongs to the project's own Pages site.
- `github.io` is on the public suffix list, so `cateim.github.io` is a top
  private domain: Google accepts it as an authorized domain, and Search
  Console verifies it as a URL-prefix property (`https://cateim.github.io/`),
  never as a domain property, since there is no DNS to edit.
- No em or en dashes anywhere (house rule of the owner).
