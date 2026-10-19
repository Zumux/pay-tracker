# Changelog

All notable changes to Pay Tracker. Newest first.

When releasing a change, add an entry here and bump the cache version in `sw.js` (noted in brackets below) so phones pick up the update.

**This file is shown inside the app.** The first time someone opens a new version, a "What's new" popup shows every release section newer than the one they last saw. Write entries for the person using the app, use a heading like `## [1.2.0] - 2026-11-01`, and keep the `## [Unreleased]` heading above it for work in progress (it is never shown).

## [Unreleased]

## [1.5.0] - 2026-10-18 (sw cache `pay-tracker-v11`)

### Added
- **30 extra paid minutes at clock-in.** When you clock in, your shift now starts 30 minutes earlier to include the extra paid time, e.g. clocking in at 7:23 rounds to 7:30 and the shift starts at 7:00. It only applies to your first clock-in of the day.
- Change the amount (none, 15, 30, 45 or 60 minutes) in ⚙ → Clock in / out rounding. Shifts added with **+** are not changed.

## [1.4.0] - 2026-10-18 (sw cache `pay-tracker-v10`)

### Added
- **Clock in / clock out** at the top of the Timesheet. Tap **Clock in** when you start and **Clock out** when you finish, and the shift is saved for you. A timer shows how long you have been working, and what clocking out right now would record.
- Times round to the **nearest 15 minutes** (7:23 becomes 7:30, 7:22 becomes 7:15). You can change this to 5 minutes or no rounding in ⚙ → Clock in / out rounding.
- Clocking in is remembered even if you close the app or restart your phone.
- If you forget to clock out (16+ hours), the shift opens for you to check before it is saved. **Cancel** throws away a clock-in you did not mean to make.

## [1.3.1] - 2026-10-18 (sw cache `pay-tracker-v9`)

### Added
- **Weekly totals** now show the average hours per day worked for each week (e.g. "5 days · 8.75 h/day · $875.00").

## [1.3.0] - 2026-10-18 (sw cache `pay-tracker-v8`)

### Added
- **Reports tab** (📊), with:
  - **Hours worked**: choose a From *and* To date, or tap a quick range (This week, Last week, This month, Last month, Last 30 days, This year). It shows hours, days worked, gross pay and average hours per day worked.
  - **Weekly totals**: every week's hours, days and pay, with a bar for each week and your average week over the last 12 full weeks. Choose whether weeks run Mon–Sun or Sun–Sat.

### Changed
- "Hours since" moved from Pay Periods to the new Reports tab, and now has an end date. Your saved start date carries over.

## [1.2.1] - 2026-10-18 (sw cache `pay-tracker-v7`)

### Fixed
- **CSV import** now understands dates written with month names, like `March 2` or `Mar 2, 2026`. Dates without a year are given the most recent past year, and the import message says so.
- Import messages now separate shifts that were already in the app from rows that couldn't be read, and show an example of a problem row.

## [1.2.0] - 2026-10-18 (sw cache `pay-tracker-v6`)

### Added
- **Hours since**: at the top of Pay Periods, pick a date to see the hours, days worked and gross pay from that date through today. The date is remembered, so you can keep tracking from a start date, your last raise or your last vacation.

## [1.1.1] - 2026-10-12 (sw cache `pay-tracker-v5`)

### Fixed
- Updates could install with leftover copies of old files, so new features (like ⚙ → About) didn't appear. Updates now always download fresh files.
- Updates now apply as soon as they've downloaded. The app reloads itself once, instead of waiting until the next time you open it. It also checks for updates when you switch back to it.

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
