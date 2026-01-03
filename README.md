# Digital Detox App Waitlist

A bold, modern landing page + waitlist for **NFC Social Media Blocker**. Built for GitHub Pages with a single HTML file and a lightweight Google Sheets (Apps Script) backend for email capture.

## Preview
- Hosted on GitHub Pages (static)
- Tailwind via CDN
- Email-only waitlist
- Inspirational toast on successful signup

## Tech
- HTML + Tailwind CSS
- Google Apps Script (optional for form handling)

## Quick Start
1. Open `index.html` in your browser to preview locally.
2. Deploy the repo to GitHub Pages.
3. Create a Google Sheet and connect Apps Script (see below).

## Google Sheets Setup (Free)
1. Create a Google Sheet.
2. Extensions → Apps Script.
3. Paste this script and save:

```javascript
function doGet() {
  return ContentService.createTextOutput("ok");
}

function doPost(e) {
  const sheetName = "Emails";
  const ss = SpreadsheetApp.getActiveSpreadsheet();
  const sheet = ss.getSheetByName(sheetName) || ss.insertSheet(sheetName);

  if (sheet.getLastRow() === 0) {
    sheet.appendRow(["email", "submitted_at"]);
  }

  const email = (e.parameter.email || "").trim();
  if (!email) {
    return ContentService.createTextOutput("missing email");
  }

  sheet.appendRow([email, new Date().toISOString()]);
  return ContentService.createTextOutput("ok");
}
```

4. Deploy → New deployment → Web app
   - Execute as: Me
   - Who has access: Anyone
5. Copy the Web App URL and paste it into `index.html` at:

```javascript
const scriptURL = "YOUR_WEB_APP_URL";
```

## Export CSV
In Google Sheets: File → Download → Comma-separated values (.csv)

## License
MIT
