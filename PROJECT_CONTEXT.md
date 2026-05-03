# Project Context — חווה בחבל Registration Minisite

## Overview
Registration minisite for a beginner horse riding course at "חווה בחבל" (Farm in the Region). Single-page HTML app, hosted on GitHub Pages, with Google Sheets as the backend for form submissions.

## Live URLs
- **Site:** https://tsafrirezra.github.io/havab-horse-course/
- **Repo:** https://github.com/tsafrirezra/havab-horse-course
- **Payment (PayBox):** https://links.payboxapp.com/2vYnIA5ZO2b

## Architecture
```
[User submits form] → [GET request via Image ping] → [Google Apps Script] → [Google Sheet]
         ↓
[Success screen with PayBox payment link]
```

- **Frontend:** Single `index.html` (HTML + CSS + JS, no dependencies)
- **Backend:** Google Apps Script (doGet) → appends rows to Google Sheet
- **Hosting:** GitHub Pages (legacy mode, deploys from `main` branch)
- **Payment:** External PayBox link (not integrated, user clicks after registration)

## Google Apps Script
- **URL:** `https://script.google.com/macros/s/AKfycbwDFspn9pcI3U52-zULyLigHh6RvhkmBX6yweutkzzaWMZTYl303Vpm70RreV67cMOCJg/exec`
- **Method:** `doGet(e)` — reads `e.parameter.*` fields
- **Access:** Anyone (no login required)
- **Sheet columns:** שם מלא | טלפון | גיל | שעה | תאריך הרשמה

### Apps Script Code
```javascript
function doGet(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  sheet.appendRow([
    e.parameter.name,
    e.parameter.phone,
    e.parameter.age,
    e.parameter.time,
    new Date().toLocaleString('he-IL')
  ]);
  return ContentService.createTextOutput('ok');
}
```

## Form Fields
| Field | Type | Values |
|-------|------|--------|
| שם מלא | text input | free text |
| טלפון | tel input | min 9 digits |
| גיל | dropdown | 6–16 |
| שעה מועדפת | radio buttons | 16:00 / 17:00 / 18:00 |

## Course Details
- **Name:** קורס הכרות למתחילים
- **Start date:** 06.05
- **Location:** חווה בחבל
- **3 Sessions:**
  1. שפת הסוסים — תקשורת וטיפול ראשוני
  2. הדרכה מעשית — איכוף נכון והכרת הציוד
  3. רכיבה בסיסית — יציבות ושליטה במגרש
- **Contacts:** נתנאל 052-595-0524 | צפריר 052-529-9868

## Design
- RTL Hebrew layout
- Earthy green/brown color palette (matches original flyer)
- Mobile responsive
- No external dependencies (zero JS/CSS libraries)

## Deployment Flow
```bash
# Edit index.html
git add . && git commit -m "message" && git push
# GitHub Pages auto-deploys within ~30 seconds
```

## Known Decisions
- Image-ping (GET) used instead of POST/fetch for maximum mobile compatibility
- `mode: 'no-cors'` and iframe approaches failed on mobile — GET works universally
- Payment is a separate step (not integrated into form flow) — user clicks PayBox link after registration
- If Google Script URL changes (new deployment), update the `SCRIPT_URL` constant in `index.html`
