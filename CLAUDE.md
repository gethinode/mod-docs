# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Hugo module (`github.com/gethinode/mod-docs`) that provides reference documentation for [Hinode](https://gethinode.com) blocks and UI components. It is designed to be bundled into Hinode-based Hugo sites as a dependency, not run standalone. It requires **Hugo Extended** (v0.146.0+) for SCSS compilation.

## Common Commands

```bash
# Development server
npm start

# Production build (also used for testing)
npm run build
npm run test

# Linting
npm run lint            # All linters (styles + markdown)
npm run lint:styles     # stylelint on assets/scss/**
npm run lint:markdown   # markdownlint on content/**

# Cleanup
npm run clean           # Remove public/ and resources/

# Hugo module management
npm run mod:update      # Update Hugo module dependencies
npm run mod:vendor      # Vendor Hugo modules into _vendor/
npm run mod:tidy        # Tidy go.sum
```

`npm start` and `npm run build` automatically run `npm run clean` and `npm run mod:vendor` as pre-steps.

## Architecture

### Module Structure

This Hugo module mounts its content into the consuming site via `hugo.toml` module mounts:

- `content/` → site content (blocks + components documentation pages)
- `assets/` → SCSS, images, SVGs
- `data/` → YAML/TOML data files (abbreviations, contacts, timelines, style config)
- `static/` → static assets (animations)

### Content Organization

Documentation lives in `content/` with two sections:

- `content/blocks/` — 18 Hinode block types (hero, cards, faq, cta, etc.)
- `content/components/` — 40+ UI components (button, carousel, modal, etc.)

Each markdown file documents a single block or component with frontmatter and examples.

### Example Site

`exampleSite/` is a standalone Hugo site used to preview and test the module locally. It has its own `go.mod` and `hugo.toml`. The file `mod-docs.work` is a Hugo workspace file enabling local module resolution without publishing.

### Dependency Management

Hugo module dependencies are vendored into `_vendor/` (auto-generated, not committed). The `go.mod` at the root defines this module's identity; `exampleSite/go.mod` defines the example site's dependencies.

## Git & Release Conventions

**Commits must follow [Conventional Commits](https://www.conventionalcommits.org/)** — enforced by a Husky commit-msg hook using `commitlint`. The pre-commit hook runs `npm test` (full build).

Releases are automated via **semantic-release** triggered on pushes to `main`. It generates changelogs, bumps versions in `package.json`, creates GitHub releases, and publishes to npm with OIDC provenance.

## CI/CD

- **test.yml** — Builds on macOS, Windows, Ubuntu × Node 22.x & 24.x on push to `main`, PRs, and version tags.
- **release.yml** — Runs semantic-release on `main` after tests pass.
- **mod-update.yml** — Daily scheduled Hugo module dependency updates.
- **auto-merge.yml** — Auto-merges Dependabot patch/minor updates; flags majors for manual review.
