# TransitionZero · Claude Analytics

A private dashboard of Claude usage across the organisation, hosted on GitHub Pages at
`https://transition-zero.github.io/tzcl-analytics/`. The site is served from the
`published` branch; `main` holds the same files under review.

## Files

| File | What it is |
|---|---|
| `index.html` | The dashboard. Changes only when the design changes. |
| `data.enc` | All the figures, encrypted. Useless without the password. Replaced monthly. |
| `fonts/` | Webfonts the page links to. |

## Why the data is encrypted

This repository is public, because GitHub Pages on this plan cannot publish from a private
repository. The dashboard contains named staff usage and spend, so the data file is
encrypted before it is ever committed.

`data.enc` contains nothing but a salt, an IV and ciphertext. Anyone who downloads it sees
noise. The dashboard asks for a password, derives a key from it in the browser
(PBKDF2-SHA256, 250,000 iterations) and decrypts with AES-256-GCM. The password is never
transmitted and is not stored anywhere.

## Refreshing it each month

An owner harvests the figures from claude.ai with a console script, builds the new
`data.enc` inside the dashboard itself (the **Refresh the data** link in the footer,
behind the password), and uploads the file to the `published` branch. The instructions and
the scripts live in the private `tzcl-analytics-source` repository.

## Two different time windows, on purpose

- **Monthly adoption** and **Cost** are calendar months (March 2026 onward). Per-user chat,
  Cowork and Claude Code figures exist as a real monthly series, so these restate cleanly
  for any month you pick.
- **Usage detail** is a rolling 30-day snapshot, labelled as such on the page.
