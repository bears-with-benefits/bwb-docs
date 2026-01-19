← [Back to Technical Documentation](/technical-docs/)

# Documentation Style & Implementation Guide

This guide defines the default format for future Docsify technical docs so new topics (e.g., a new cart setup) match the existing style.

## Goals

- Consistent structure across docs
- Easy scanning for non-dev and dev readers
- Minimal fluff, high signal
- Docsify-friendly (plain Markdown, simple links)

## File and link conventions

- File names: `kebab-case.md` (e.g., `new-cart-setup.md`).
- Titles: use Title Case in the first `#` heading.
- Links: use relative links (e.g., `new-cart-setup.md`).
- If a doc is draft, add `(Draft)` in the title line.

## Where to link new docs

Add new docs to the **Technical Documentation** index page (example pattern):

```md
# Technical Documentation

## Current Cart System (July 2025)

- [New Cart Setup](new-cart-setup.md)
- [Rebuy SmartCart Discount System](rebuy-smartcart-discount-system.md)

## Additional Topics

- [BwB Progressive Discount App](bwb-progressive-discount-app/)
```

If you use a Docsify sidebar, ensure the new file is linked there too.

## Standard doc template

Use this skeleton for new technical docs. Remove sections that do not apply.

```md
# <Doc Title>

One or two sentences describing what this doc covers.

## Scope

- In scope: what this doc covers
- Out of scope: what it does not cover

## Audience

- Who should read this (e.g., ops, devs, support)

## Architecture (if needed)

- Key components
- How data flows

## Setup / Implementation

- Step-by-step instructions
- Any required files/paths

## Configuration

- Required settings
- Optional settings
- Defaults

## Ops / Deployment (if needed)

- Env vars
- Release steps

## Troubleshooting

- Common issues and fixes

## References

- Link to related docs or files
```

## Writing style

- Short paragraphs, bullet lists preferred.
- Avoid deep theory; focus on how it behaves in this codebase.
- Prefer specifics over generalities (paths, keys, exact labels).
- Keep language clear and internal (no marketing tone).

## New doc checklist

- File created with the standard template.
- Added to Technical Documentation index page.
- Added to Docsify sidebar (if used).
- Checked links are relative and working.

