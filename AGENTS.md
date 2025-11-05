# Repository Guidelines

## Project Structure & Module Organization
The docs are authored in the repository root as numbered Markdown files (for example, `1introduction-and-overview.md` through `11project-management-and-reporting.md`). Numbers control sidebar order within Docsify, so keep two-digit prefixes when adding sections. `_sidebar.md` defines navigation labels, while `assets/` stores screenshots and PDFs referenced across topics. `index.html` contains the Docsify bootstrap configuration; edit it only when adjusting global theming or scripts.

## Build, Test, and Development Commands
- `npx docsify-cli@latest serve .` — Local preview at http://localhost:3000 with live reload. Use this before opening a PR to verify navigation and links.
- `npx markdownlint-cli "**/*.md"` — Lint Markdown formatting; install once globally (`npm install -g markdownlint-cli`) if you contribute regularly.
If installing npm tooling is impractical, open `index.html` directly in a browser for a quick spot-check, but rely on Docsify serve for production parity.

## Coding Style & Naming Conventions
Write in Markdown with ATX headings (`#`, `##`, etc.) and sentence-case titles. Favor short paragraphs and ordered lists for stepwise procedures. Use fenced code blocks with language tags for commands. Images belong in `assets/` and are referenced with relative paths including descriptive alt text. Preserve the numeric filename prefixes (e.g., `12new-topic.md`) and keep file names lowercase with hyphens.

## Testing Guidelines
There is no automated test suite, so contributors must self-review. During preview, confirm sidebar links resolve, heading anchors generate correctly, and assets load from `assets/`. For larger updates, request a second reviewer to sanity-check factual accuracy and broken links. Document any manual validation in the PR description.

## Commit & Pull Request Guidelines
Commits in this repo are concise and descriptive (e.g., "Adding images, tidying links sidebar"). Use imperative mood when possible, limit to 70 characters, and group related edits per commit. Pull requests should include a short summary, screenshots for visual changes, links to related tickets, and a checklist of manual verification steps. Ensure PR titles mirror the main change and request review from the documentation maintainer group.

Commits to this repo will automatically redeploy to Github Pages.
