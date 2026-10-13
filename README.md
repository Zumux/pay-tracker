# Pay Tracker

**App:** <https://zumux.github.io/pay-tracker/>

A small app for tracking work shifts, pay rates and pay periods. It runs on Android and iPhone as an installable web app (PWA). All data is stored on the phone, works offline, and can be exported and imported as files.

## Features

- **Timesheet**: date, start time, end time, hours and pay for each shift. Hours and pay are calculated automatically. Overnight shifts (ending after midnight) are handled. Shifts are grouped by pay period.
- **Pay Periods**: period start, period end, pay date, hours, gross pay and estimated net pay. Tap a period to see its shifts and record the pay you actually received.
- **Year to date**: the top card on Pay Periods shows hours, gross and net paid in the year, with ‹ › to view other years. Income is counted by **pay date**, the same way your T4 counts it (so work from Dec 16–31 counts toward the next year). Net uses your recorded pay where you've entered it, and estimates otherwise.
- **Pay Rates**: hourly rates with the date they take effect. Each shift uses the rate in effect on its date, so adding a raise (even backdated) updates all pay automatically.
- **Backup & settings** (⚙ button): export/import a backup, CSV exports, 12/24-hour time, estimated deductions %, province for stat holidays, extra holidays.

## Pay schedule

| Work period | Paid on |
|---|---|
| 1st – 15th | Last day of the same month |
| 16th – end of month | 15th of the next month |

If a pay date falls on a weekend or a stat holiday, it moves back to the business day before (repeating if needed, e.g. a Sunday payday on Easter weekend moves past Good Friday to Thursday). The Pay Periods tab shows when and why a date was moved.

To change the schedule, edit `periodFor()` and `adjustPayDate()` in `app.js`.

### Stat holidays

Choose your province or territory in ⚙ → *Stat holidays*. The app then uses:

- **National**: New Year's Day, Good Friday, Canada Day, Labour Day, Christmas Day.
- **Plus your province's** general holidays (e.g. Family Day, Victoria Day, Thanksgiving, Remembrance Day, Boxing Day, Sept 30, Fête nationale; it varies by province).

Dates are calculated automatically for every year. Expand *Holidays in [year]* in settings to check the list. If your employer observes other days (or the bank is closed on a day not listed), add them under *Extra holidays*. The holiday lists live in `PROVINCE_HOLIDAYS` in `app.js` if they ever need adjusting.

In practice only a few holidays can land on or just before a payday (the 15th or month end): Sept 30, Family Day / Islander Day / Louis Riel Day / Heritage Day when it falls on Feb 15, Yukon's Discovery Day on Aug 15, and Good Friday.

### Net pay

**Estimated net pay** = gross pay × (1 − deductions %). Set the percentage in ⚙ (default 20%).

When a paycheque arrives, open Pay Periods → tap the period → **Record actual pay received** and enter the amount deposited. That period then shows the actual amount, along with what the estimate was. Once you've recorded at least one, ⚙ → *Estimated deductions* suggests a percentage based on your last 6 recorded paycheques, which you can apply with one tap.

## Files

| File | Purpose |
|---|---|
| `index.html` | Page layout |
| `styles.css` | Styling (light and dark mode) |
| `app.js` | All app logic: storage, pay calculations, screens, import/export |
| `sw.js` | Service worker that makes the app work offline |
| `manifest.webmanifest` | App name, colours and icons used when installing |
| `icons/` | App icons |
| `CHANGELOG.md` | History of changes |

## Putting it online

The files must be served over HTTPS for the app to install. Either free option works; the host only serves the app code. Your data never leaves your phone.

**Netlify**
1. Create a free account at netlify.com.
2. Go to <https://app.netlify.com/drop> and drag the whole `PayTrackerPWA` folder onto the page.
3. Optionally rename the site under *Site configuration → Change site name*.

**GitHub Pages**
1. Create a public repository and upload these files to it.
2. *Settings → Pages → Deploy from a branch → main / root*.

## Installing on a phone

- **Android**: open the URL in Chrome → ⋮ → *Install app* (or *Add to Home screen*).
- **iPhone**: open the URL in **Safari** → Share → *Add to Home Screen*. Always open it from the home-screen icon, because Safari tabs have separate storage.

## Your data

- Stored in the browser's on-device database (IndexedDB) for the app's web address. Nothing is sent anywhere.
- **Uninstalling the app or deleting the home-screen icon (iPhone) deletes the data.** Clearing "site data / cookies" for the site in Chrome also deletes it.
- Data is tied to the web address. If the app moves to a new URL, export a backup from the old one and import it into the new one.
- Each device has its own copy; there is no syncing.

### Backups

⚙ → **Export backup** saves a `.json` file with all shifts, rates, recorded pay and settings. On a phone this opens the share sheet so you can save it to Google Drive, iCloud Files, email, etc. The app reminds you on the Timesheet if your last backup is more than 14 days old.

⚙ → **Import file** with a backup `.json` **replaces all data** (you're asked to confirm first).

### CSV export and import

- Export: Timesheet, Pay Periods (including estimated and actual net) and Pay Rates as CSV files for Excel or Google Sheets.
- Import: a CSV with **Date, Start, End** columns adds shifts; one with **Date, Rate** columns adds pay rates. Columns are matched by name, duplicate shifts are skipped, and a rate with the same date as an existing one replaces it.
- Dates like `2026-03-04` work best. A date like `3/4/2026` is read as month/day (March 4), unless the first number is over 12.
- Times like `09:00`, `9:00 AM` or `9:00:00 PM` are all accepted.

**Moving data from the old Google Sheet:** open the Timesheet tab → *File → Download → Comma-separated values (.csv)*, then do the same for the Pay Rates tab, then import both files in the app.

## Updating the app

The app is hosted on GitHub Pages from the `main` branch of <https://github.com/Zumux/pay-tracker>.

1. Edit the files.
2. In `sw.js`, bump the version in `const CACHE = 'pay-tracker-v3'` (e.g. to `v4`). **Without this, phones keep showing the old version.**
3. Add an entry to [CHANGELOG.md](CHANGELOG.md).
4. Commit and push:
   ```
   git add -A
   git commit -m "Describe the change"
   git push
   ```
   GitHub Pages republishes automatically within a minute or two.

Phones pick up the update the next time the app is opened (sometimes it takes a second open). Data is not affected.

## Testing locally

From this folder run a local web server, e.g. `python -m http.server 8000`, and open <http://localhost:8000>. Opening `index.html` directly from disk won't work properly because service workers need a server.
