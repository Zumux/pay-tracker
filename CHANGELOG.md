# Changelog

All notable changes to Pay Tracker. Newest first.

When releasing a change, add an entry here and bump the cache version in `sw.js` (noted in brackets below) so phones pick up the update.

**This file is shown inside the app.** The first time someone opens a new version, a "What's new" popup shows every release section newer than the one they last saw. Write entries for the person using the app, use a heading like `## [1.2.0] - 2026-11-01`, and keep the `## [Unreleased]` heading above it for work in progress (it is never shown).

## [Unreleased]

## [1.1.0] - 2026-10-12 (sw cache `pay-tracker-v4`)

### Added
- **What's new popup**: after an update, the app shows what changed, once. You can see it again any time from ⚙ → About → What's new.
- The app version is now shown in ⚙ → About.

## [1.0.0] - 2026-10-12 (sw cache `pay-tracker-v3`)

First release. Replaces the old AppSheet + Google Sheet app.

### Added
- **Timesheet**: add, edit and delete shifts (date, start time, end time). Hours and pay are calculated automatically, overnight shifts are supported, and shifts are grouped by pay period with totals.
- **Pay Rates**: hourly rates with an effective date. Each shift uses the rate in effect on its date, so backdated raises recalculate all pay.
- **Pay Periods**: 1st–15th paid on the last day of the month, 16th–end paid on the 15th of the next month. Shows hours, gross pay and estimated net pay per period, plus a status (in progress, awaiting pay, paid).
- **Payday adjustments**: paydays on a weekend or Canadian stat holiday move to the business day before. Holidays are chosen by province or territory, and you can add your own extra holiday dates.
- **Actual pay**: record the net pay actually received for a period. The app compares it with the estimate and suggests a deductions % based on your last 6 recorded paycheques.
- **Year-to-date totals**: hours, gross and net paid per year, counted by pay date (matching your T4).
- **Backup and restore**: export all data as a `.json` file (via the share sheet on phones) and import it again. A banner reminds you if your last backup is more than 14 days old.
- **CSV export and import**: export timesheet, pay periods and pay rates; import shifts and rates from CSV, including from the old Google Sheet.
- **Settings**: 12-hour or 24-hour time, estimated deductions %, province.
- Installable on Android and iPhone, works offline, light and dark mode.
