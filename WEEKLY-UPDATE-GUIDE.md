# Kooner Adoption Dashboard — Weekly Update Guide

**Dashboard URL:** `https://[your-github-username].github.io/kooner-adoption-dashboard/`

You are responsible for two weekly updates:

1. **Survey data** — automatically synced from Jotform via Google Sheets (no action needed unless the connection breaks)
2. **Events calendar** — manually updated in GitHub when new events are scheduled or past events need notes added

---

## Setup (One-Time)

### 1. Create the GitHub Repository

1. Go to [github.com](https://github.com) and sign in
2. Click the **+** button (top right) → **New repository**
3. Name it `kooner-adoption-dashboard`
4. Set to **Public** (required for free GitHub Pages)
5. Click **Create repository**
6. Upload the two files Brooke provides:
   - `index.html`
   - `events-data.json`
7. Click **Commit changes**

### 2. Enable GitHub Pages

1. In your repository, go to **Settings** → **Pages** (left sidebar)
2. Under "Source," select **Deploy from a branch**
3. Choose **main** branch and **/ (root)** folder
4. Click **Save**
5. Wait 2-3 minutes — your dashboard will be live at:
   `https://[your-username].github.io/kooner-adoption-dashboard/`

### 3. Connect Google Sheets (Survey Auto-Sync)

The dashboard pulls survey data from your Jotform-synced Google Sheet. To set this up:

1. Open the Google Sheet that receives Jotform responses
2. Go to **File** → **Share** → **Publish to web**
3. Select the sheet/tab with survey responses
4. Choose **Comma-separated values (.csv)** as the format
5. Click **Publish** and copy the URL
6. In GitHub, open `index.html` and find this line near the top of the `<script>` section:
   ```
   SURVEY_SHEET_URL: 'YOUR_GOOGLE_SHEETS_PUBLISHED_CSV_URL_HERE',
   ```
7. Replace `YOUR_GOOGLE_SHEETS_PUBLISHED_CSV_URL_HERE` with your published CSV URL
8. Also verify the column names in `SURVEY_COLUMNS` match your Google Sheet headers. If your columns have different names, update them here:
   ```
   SURVEY_COLUMNS: {
       date: 'Submission Date',
       dsp: 'DSP Code',
       station: 'Station',
       satisfaction: 'Satisfaction',
       timeliness: 'Timeliness',
       quality: 'Quality',
       issue: 'Issues',
       suggestion: 'Feedback'
   }
   ```
9. Commit the changes

Once connected, new Jotform submissions will appear on the dashboard automatically — no weekly action needed for surveys.

---

## Weekly Task: Update the Events Calendar

When new events are scheduled or past events need notes/summaries added, edit the `events-data.json` file.

### How to Edit events-data.json in GitHub

1. Go to your repository: `github.com/[your-username]/kooner-adoption-dashboard`
2. Click on `events-data.json`
3. Click the **pencil icon** (Edit this file) in the top right
4. Make your changes (see examples below)
5. Click **Commit changes**
6. The dashboard updates automatically within 2-3 minutes

### Adding a New Event

Find the `"events": [` section and add a new entry. Copy this template and fill in the details:

```json
{
  "date": "2026-03-15",
  "title": "HLA2 Roundtable",
  "type": "roundtable",
  "station": "HLA2",
  "time": "2:00 PM",
  "notes": "",
  "actionItems": []
}
```

**Important:** Place a comma after the previous event's closing `}` before your new entry.

**Event types available:** `roundtable`, `site-visit`, `training`, `deadline`, `review`, `newsletter`

### Adding Notes to a Past Event

Find the event in the JSON and update the `"notes"` field. You can use basic HTML for formatting:

```json
"notes": "<strong>Key Issues:</strong> Description of issues discussed.<br><br><strong>Solutions:</strong> What was agreed upon.<br><br><strong>Next Steps:</strong> Follow-up items."
```

**Formatting quick reference:**
- `<strong>Bold text</strong>` — for section headers
- `<br>` — line break
- `<br><br>` — paragraph break

### Adding Action Items to an Event

Update the `"actionItems"` array:

```json
"actionItems": [
  {"owner": "Brooke", "action": "Send escalation contacts by EOD", "status": "pending"},
  {"owner": "Ash", "action": "Share tech contact info with DSPs", "status": "done"},
  {"owner": "Team", "action": "Schedule follow-up meeting", "status": "pending"}
]
```

**Status options:** `"pending"` or `"done"`

### Updating Action Item Status

When an action is completed, change `"status": "pending"` to `"status": "done"`.

---

## Troubleshooting

**Dashboard shows "Could not load events-data.json"**
- Make sure the file is named exactly `events-data.json` (lowercase, with hyphens)
- Check for JSON syntax errors — a missing comma or quote will break the file
- Use [jsonlint.com](https://jsonlint.com) to validate your JSON before committing

**Survey data not showing / showing old data**
- Google Sheets published CSV can take up to 5 minutes to refresh
- Check that the Google Sheet is still published (File → Share → Publish to web)
- Verify the column names still match the CONFIG in index.html

**Dashboard not updating after commit**
- GitHub Pages can take 2-5 minutes to deploy
- Hard refresh your browser: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)

**JSON syntax tips**
- Every string value must be in double quotes: `"like this"`
- Items in a list are separated by commas — but NO comma after the last item
- Use `<br>` for line breaks in notes (not actual line breaks in the JSON string)

---

## Quick Reference: Full Event Template

```json
{
  "date": "YYYY-MM-DD",
  "title": "Event Title",
  "type": "roundtable",
  "station": "STATION_CODE",
  "time": "2:00 PM",
  "notes": "<strong>Summary:</strong> Key discussion points here.<br><br><strong>Decisions:</strong> What was decided.",
  "actionItems": [
    {"owner": "Person Name", "action": "What they need to do", "status": "pending"}
  ]
}
```
