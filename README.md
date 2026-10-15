# 📓 Bet Tracker

A small, private bet journal. **No account, no tracking, no backend, no runtime dependencies.** This is a record-keeping tool, not betting advice or a prediction service.

[Live app](https://tekideki.github.io/Bet-Tracker/) · [Apache-2.0](LICENSE) · [Support with a coffee](https://paypal.me/TekiDeki)

## Features

- Record date, sport, competition, event, bet type, stake, decimal odds, result and notes.
- **Edit existing records**, including settling pending bets, or delete them with confirmation.
- **Decimal comma or dot**: `1,5` and `1.5` both mean one and a half, in the form and in imported files. Numbers are displayed in the format of the selected language.
- Net profit, settled-bet ROI, win rate, average odds/stake, cumulative profit, settled stake, pending stake and potential profit.
- **Română, English, Srpski (Latin), Српски (Cyrillic)**. Stable stored values and translated donation labels.
- Light/dark themes, responsive mobile cards, accessible keyboard controls.
- One journal currency: **RON, EUR, USD, RSD or GBP**. Language changes never change the currency. Changing currency only relabels amounts; it does **not** convert them.
- **Field-level validation** with a message under every problem field, instead of browser alert boxes. Confirmations and results use small in-page dialogs and toasts that stay readable on phones.
- **Recovery banner** when stored data cannot be read: the app never overwrites it, and offers a raw copy download, a retry, or a fresh start that keeps the old bytes saved in the browser.
- Accessible history table (screen-reader caption, labelled row actions), a keyboard skip link and visible focus states.
- Local browser storage and JSON export/import, with validation, duplicate detection and a summary of new, duplicate and invalid records before anything is merged.
- Installable PWA and offline app shell after the first successful online visit, with app shortcuts for adding a bet and jumping to the statistics.
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
- Both separators are accepted on input: a comma or a dot, with no thousands separators. Scientific notation and negative values are rejected, and grouping separators typed by hand are ignored.

## Data safety and backups

Data is stored under `tracker_pariuri_v1` in `localStorage`, separately from theme, language and currency preferences. There is no upload, cloud synchronization or encryption. Anyone with access to your browser profile may access it. The hosting provider receives ordinary page requests; following external GitHub/PayPal links involves those services.

**Export backups regularly.** Clearing site data, changing browser/device/origin, or using private browsing can erase or isolate the journal. Data from a local file is not automatically moved to GitHub Pages.

New backups contain `{ "schemaVersion": 2, "currency": "RON", "bets": [...] }`. Legacy array-only backups remain accepted. Old localized sport/type/result values are normalized in memory and persisted after the next successful edit/add/delete/import. Existing storage is not rewritten just by opening the app.

Legacy records have no currency metadata: **RON is the default until you choose the correct journal currency**. Old versions changed the symbol with the UI language without performing conversion. Mixed-currency historical data cannot be reliably reconstructed automatically; reconcile it manually before using aggregate statistics.

Imports are all-or-nothing for validation, appended rather than replacing data, and require confirmation. Records with identical normalized content are skipped as duplicates, regardless of their ID. This avoids re-importing the same backup, but also skips genuinely separate bets with identical fields. Distinguish those records with a note before importing. Backup currencies must match the journal currency. Imported IDs are regenerated to avoid collisions and unsafe markup.

Invalid stored data is handled without losing work:

- **One corrupt record** no longer blocks the journal. Valid records load normally, the broken ones are skipped, a banner says how many were ignored, and the untouched original bytes can be downloaded as a raw copy for manual recovery.
- **Unreadable or partially written storage** opens the app with a warning banner and three choices: download the raw copy, retry reading, or start a new journal. Starting fresh keeps the previous bytes saved in the browser under a `tracker_pariuri_v1_backup_<timestamp>` key, so nothing is destroyed.
- **Blocked storage** (private mode or strict settings) still lets you record bets for the session; a banner explains that they are lost when the tab closes and offers an immediate export.
- Failed writes leave the existing journal and the entered form unchanged.

## Responsible use

Gambling can lead to financial harm and addiction. This app neither recommends bets nor guarantees returns. Do not chase losses. If gambling is causing harm, stop and seek qualified local support.

## Verification

The 2026-10-15 update was tested in Chromium using Playwright against a local copy of exactly these files: 98 checks covering the statistics (including settled and pending stakes and potential profit), decimal comma and dot input, field validation, editing and deletion through the in-page dialogs, four languages with their number formats, corrupt and unreadable storage with raw-copy download and fresh start, blocked storage, JSON import (new, duplicate, invalid and mismatched-currency files), offline navigation through the service worker, escaped user content, the 390 px phone layout and the axe-core scan. Automated axe-core checks reported 0 violations in both themes. This is not a full accessibility certification or a substitute for testing on actual devices.

The 2026-10-14 update was tested the same way for the previous feature set: calculations, four languages, editing, currency persistence, JSON backups, invalid inputs, escaped user content, legacy data, storage failures, offline navigation, isolated service-worker caches, direct-file mode and widths from 320 to 1280 px.

## License and support

Copyright © 2026 Kristian Mario Mišković (**TekiDeki**).

Licensed under the **Apache License, Version 2.0**. See [LICENSE](LICENSE) and [NOTICE](NOTICE).

[GitHub Sponsors](https://github.com/sponsors/TekiDeki) · [PayPal](https://paypal.me/TekiDeki)


## Install app

Use the **Install app** button near the footer. On supported browsers it opens the native installation prompt when available. Otherwise it shows localized instructions for Safari on iPhone/iPad, Android, and desktop browsers. Installation is controlled by the browser; no installation is claimed without its confirmation. The button is hidden in a standalone/minimal-ui app window and after an `appinstalled` event in the current session. A normal browser tab cannot always detect a previous installation.

Installation needs HTTPS or trustworthy localhost. The controls add no dependencies, tracking, network calls or storage keys; existing application data is not modified. On an existing cached version, revisit online and refresh after the service worker has updated to see the button. No automatic reload is forced.
