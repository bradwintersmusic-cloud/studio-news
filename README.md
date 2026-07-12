# studio-news

# AET News — Belmont AET

**Live URL:** https://bradwintersmusic-cloud.github.io/studio-news/

Announcement and news feed for the Belmont AET program. Supports emergency alerts, pinned carousel posts, category filtering, and automatic archiving by expiration date.

---

## Overview

- Emergency banner with red glow animation (above carousel when active)
- Auto-rotating pinned post carousel with swipe support
- Searchable feed with list and grid views
- Posts auto-archive when expiration date passes
- Collapsible archive section
- Full modal with structured content, event info, CTA button, and contact link
- Category-based visual treatment (color coding per post type)

---

## Post Lifecycle

```
Pending → Published → Archived (automatic on expiration)
```

- **Pending** — submitted via Tally, not visible on page
- **Published** — set manually in sheet, visible on page
- **Archived** — happens automatically when current date exceeds Expiration Date

To publish a post: change `Status` from `Pending` to `Published` in the Google Sheet.

---

## Data Source

**Google Sheet CSV** — URL defined at the top of the script in `index.html`:

```javascript
var SHEET_CSV_URL = "YOUR_GOOGLE_SHEET_CSV_URL_HERE";
```

To publish: Google Sheets → File → Share → Publish to web → select sheet tab → CSV → copy URL.

---

## Google Sheet Column Headers

Must match exactly (case-sensitive):

| Column               | Required | Notes                                                           |
| -------------------- | -------- | --------------------------------------------------------------- |
| Submitted at         | Auto     | Written by Tally                                                |
| Status               | Yes      | Pending or Published                                            |
| Category             | Yes      | News, Announcement, Event, Opportunity, Alert, Emergency, Other |
| Priority             | No       | Normal or High                                                  |
| Headline             | Yes      | One sentence, displayed large                                   |
| Summary              | Yes      | Truncated to 200 chars on card                                  |
| Body                 | No       | Full text, modal only                                           |
| Thumbnail URL        | No       | Dropbox `raw=1` link via Make automation                        |
| Image Alt Text       | No       | Accessibility description for thumbnail                         |
| Event Date           | No       | Relevant for Event category                                     |
| Event Time           | No       | e.g. "7:00 PM – 9:00 PM"                                        |
| Event Location       | No       |                                                                 |
| Expiration Date      | Yes      | Post archives automatically after this date                     |
| Contact Email        | No       | Shown as contact button in modal                                |
| URL                  | No       | External link                                                   |
| Call to Action Label | No       | Button text for URL (default: "Learn More")                     |
| Posted By            | Yes      | Name and department                                             |
| Audience             | No       | Metadata only, not filtered on page                             |
| Pinned               | Manual   | TRUE = appears in carousel                                      |

---

## Category Visual Treatment

| Category     | Color  | Notes                                           |
| ------------ | ------ | ----------------------------------------------- |
| News         | Gold   | Default AET brand color                         |
| Announcement | Gold   | Same as News                                    |
| Event        | Blue   | Shows date/time/location strip in modal         |
| Opportunity  | Green  |                                                 |
| Alert        | Orange |                                                 |
| Emergency    | Red    | Appears in emergency banner only, not main feed |
| Other        | Grey   |                                                 |

---

## Emergency Posts

Posts with `Category = Emergency` and `Status = Published` appear in the red glowing banner above the carousel. They do **not** appear in the main feed. Multiple emergencies stack vertically in the banner. They auto-archive on expiration like all other posts.

---

## Thumbnail Images

Thumbnails are uploaded to Dropbox via a Make automation scenario:

1. Submitter uploads image in Tally form
2. Make downloads file from Tally, uploads to Dropbox `/AET News/Thumbnails/`
3. Make creates a Dropbox shared link and writes it to the `Thumbnail URL` column in the sheet
4. Page fetches and displays the image using the `raw=1` Dropbox URL

If no thumbnail is provided, the card/carousel renders without an image.

---

## Tally Form

Staff-only submission form. Link is shared privately. If the link is leaked, generate a new Tally form URL and update the sheet integration.

---

## Tech Stack

- Static HTML / CSS / JS
- Google Sheets (CSV data source)
- Tally (form submissions)
- Make (Dropbox automation for thumbnails)
- Dropbox (thumbnail image hosting)
- GitHub Pages hosting

---

## Repo

`bradwintersmusic-cloud/studio-news`
Maintained by Brad Winters
