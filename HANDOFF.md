# Project Handoff — Horse Course Registration Minisite

## Quick Start
1. Site is live at: https://tsafrirezra.github.io/havab-horse-course/
2. Registrations flow into a Google Sheet automatically
3. To make changes: edit `index.html` → `git commit` → `git push` → live in 30s

## File Structure
```
MiniSite/
├── index.html          # The entire site (HTML + CSS + JS)
├── PROJECT_CONTEXT.md  # Technical architecture & details
└── HANDOFF.md          # This file
```

## Common Tasks

### Change course dates or text
Edit the HTML content in `index.html` (lines 303–323 area).

### Add/remove time slots
Edit the radio buttons in `index.html` (lines 365–377 area). Add a new `<div class="time-option">` block.

### Change payment link
Search for `payboxapp.com` in `index.html` — appears in 2 places (button + text link).

### Update Google Script URL
If you redeploy the Apps Script, update the `SCRIPT_URL` constant (line 411 in `index.html`).

### Add new form fields
1. Add HTML input in the form section
2. Add validation in the JS `submit` handler
3. Add the field to `sendToSheet({...})`
4. Update the Apps Script `doGet` to read and append the new `e.parameter.fieldname`
5. Add column header in Google Sheet

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Data not appearing in sheet | Check Apps Script deployment is "Anyone" (not "Anyone with Google account") |
| Site shows old version | Hard refresh (Ctrl+Shift+R) or open incognito |
| Site 404 | Check GitHub Pages is enabled: repo Settings → Pages → Source: main, / |
| Script URL broken | Redeploy in Apps Script → get new URL → update `SCRIPT_URL` in HTML |

## Contacts
- **נתנאל:** 052-595-0524
- **צפריר:** 052-529-9868
