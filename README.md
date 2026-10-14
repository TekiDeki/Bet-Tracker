# 📓 Bet Tracker

A small, private bet journal. **No account, no tracking, no backend, no runtime dependencies.** This is a record-keeping tool, not betting advice or a prediction service.

[Live app](https://tekideki.github.io/Bet-Tracker/) · [Apache-2.0](LICENSE) · [Support with a coffee](https://paypal.me/TekiDeki)

## Features

- Record date, sport, competition, event, bet type, stake, decimal odds, result and notes.
- **Edit existing records**, including settling pending bets, or delete them with confirmation.
- Net profit, settled-bet ROI, win rate, average odds/stake and cumulative profit.
- **Română, English, Srpski (Latin), Српски (Cyrillic)**. Stable stored values and translated donation labels.
- Light/dark themes, responsive mobile cards, accessible keyboard controls.
- One journal currency: **RON, EUR, USD, RSD or GBP**. Language changes never change the currency. Changing currency only relabels amounts; it does **not** convert them.
- Local browser storage and JSON export/import, with validation and duplicate detection.
- Installable PWA and offline app shell after the first successful online visit.
- Application CSS and JavaScript live in a single `index.html`; no framework, CDN, package manager or build step is needed to use it. The accompanying files provide PWA installation, icons and metadata.

## Open or install

Use the [hosted app](https://tekideki.github.io/Bet-Tracker/), or download the repository and open `index.html` directly. Direct file opening does not support service workers; browser storage behavior for `file:` URLs varies.

For local PWA testing:

```sh
python3 -m http.server 8000
```

Open `http://localhost:8000`. A production deployment needs HTTPS. Android/desktop browsers may offer **Install app**. On iPhone/iPad, open in Safari and use **Share → Add to Home Screen**. Installation availability depends on browser support and policy.

### Language links

- [RO](https://tekideki.github.io/Bet-Tracker/?lang=ro)
- [EN](https://tekideki.github.io/Bet-Tracker/?lang=en)
- [SR Latin](https://tekideki.github.io/Bet-Tracker/?lang=sr-Latn)
- [SR Cyrillic](https://tekideki.github.io/Bet-Tracker/?lang=sr-Cyrl)

A valid URL language overrides the saved preference. Otherwise, the app uses the saved preference or browser language. Search/social metadata, canonical/hreflang links, a sitemap and structured data are included; these do not guarantee indexing or ranking.

## Calculations and limits

- **Won:** profit = stake × decimal odds − stake, rounded to two decimal places.
- **Lost:** profit = −stake.
- **Void / Pending:** profit = 0. Pending stakes are not treated as losses.
- **ROI:** net profit ÷ the stakes of won and lost bets. Void and pending stakes are excluded from its denominator.
- **Win rate:** won ÷ (won + lost).
- **Total staked / averages:** include all records, including pending and void bets.
- **Cumulative profit:** chronological running profit, **not** an account balance or starting bankroll.
- Taxes, commissions, cash-outs, partial wins/losses and bookmaker-specific settlement rules are not modeled. Figures may differ from the bookmaker's account.
- Stakes must be positive, at most 1,000,000,000 and have at most two decimal places. Decimal odds must be between 1 and 100,000. Maximum 10,000 records and 5 MB per imported file. Browser storage may fill before these limits.

## Data safety and backups

Data is stored under `tracker_pariuri_v1` in `localStorage`, separately from theme, language and currency preferences. There is no upload, cloud synchronization or encryption. Anyone with access to your browser profile may access it. The hosting provider receives ordinary page requests; following external GitHub/PayPal links involves those services.

**Export backups regularly.** Clearing site data, changing browser/device/origin, or using private browsing can erase or isolate the journal. Data from a local file is not automatically moved to GitHub Pages.

New backups contain `{ "schemaVersion": 2, "currency": "RON", "bets": [...] }`. Legacy array-only backups remain accepted. Old localized sport/type/result values are normalized in memory and persisted after the next successful edit/add/delete/import. Existing storage is not rewritten just by opening the app.

Legacy records have no currency metadata: **RON is the default until you choose the correct journal currency**. Old versions changed the symbol with the UI language without performing conversion. Mixed-currency historical data cannot be reliably reconstructed automatically; reconcile it manually before using aggregate statistics.

Imports are all-or-nothing for validation, appended rather than replacing data, and require confirmation. Records with identical normalized content are skipped as duplicates, regardless of their ID. This avoids re-importing the same backup, but also skips genuinely separate bets with identical fields. Distinguish those records with a note before importing. Backup currencies must match the journal currency. Imported IDs are regenerated to avoid collisions and unsafe markup.

If stored data is invalid/unreadable, editing is blocked instead of silently overwriting it. The Export button can download the raw stored value when readable, for manual recovery. Failed writes leave the existing journal and the entered form unchanged.

## Responsible use

Gambling can lead to financial harm and addiction. This app neither recommends bets nor guarantees returns. Do not chase losses. If gambling is causing harm, stop and seek qualified local support.

## Verification

The 2026-10-14 update was tested in Chromium using Playwright: calculations, four languages, editing, currency persistence, JSON backups, invalid inputs, escaped user content, legacy data, storage failures, offline navigation, isolated service-worker caches, direct-file mode and widths from 320 to 1280 px. Automated axe-core checks reported no tested WCAG A/AA violations in either theme across all four languages; this is not a full accessibility certification or a substitute for testing on actual devices.

## License and support

Copyright © 2026 Kristian Mario Mišković (**TekiDeki**).

Licensed under the **Apache License, Version 2.0**. See [LICENSE](LICENSE) and [NOTICE](NOTICE).

[GitHub Sponsors](https://github.com/sponsors/TekiDeki) · [PayPal](https://paypal.me/TekiDeki)
