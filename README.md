# 📋 New Hire Checklist

A lightweight, interactive onboarding checklist that lives at a real URL, saves progress automatically, and gives managers a live view of where new hires stand — no logins, no apps, no friction.

Built as a single HTML file. Deployed on GitHub Pages. Backed by Supabase.

---

## What It Does

- **Name-based access** — new hires enter their name on first visit, get a welcome screen, and are assigned a unique profile. Returning users pick up exactly where they left off.
- **Auto-saves to the cloud** — progress is written to Supabase on every interaction. Refresh the page, switch devices, come back a week later — it's all there.
- **Admin dashboard** — type `admin` as your name, enter the password, and see every registered user's progress and last active timestamp at a glance.
- **7 onboarding sections** — covers paperwork, equipment, system access, required training, Day 1 meetings, department tools, and future access items.
- **Urgency badges** — time-sensitive items (like the 48hr SAP Concur deadline) are visually flagged so nothing slips through.
- **Google Analytics** — basic page tracking included out of the box.

---

## Tech Stack

| Layer | Tool | Cost |
|---|---|---|
| Hosting | GitHub Pages | Free |
| Database | Supabase | Free tier |
| Analytics | Google Analytics 4 | Free |
| DNS | Cloudflare | Free |

Total monthly cost: **$0**

---

## How It Works

```
User visits URL
  → Enters name
  → New user: welcome screen → UUID created → row inserted in Supabase
  → Returning user: progress loaded from Supabase → checklist unlocked

Admin visits URL
  → Types "admin" → password prompt
  → Dashboard: all users, % complete, last active
```

---

## Project Structure

```
/
└── index.html      # The entire app — HTML, CSS, and JS in one file
└── CNAME           # Custom domain config for GitHub Pages
└── README.md       # You're reading it
```

---

## Configuration

All config lives at the top of the `<script>` block in `index.html`:

```javascript
const SUPABASE_URL   = 'YOUR_SUPABASE_URL';
const SUPABASE_KEY   = 'YOUR_SUPABASE_ANON_KEY';
const ADMIN_NAME     = 'admin';
const ADMIN_PASSWORD = 'YOUR_PASSWORD';
```

---

## Supabase Setup

Table: `checklist_progress`

| Column | Type | Notes |
|---|---|---|
| `id` | uuid | Auto-generated |
| `user_id` | text | Unique — UUID assigned on first visit |
| `display_name` | text | Name entered at gate |
| `state` | jsonb | Full checkbox state |
| `updated_at` | timestamptz | Timestamp of last save |
| `created_at` | timestamptz | Auto-generated |

Required: `user_id` must have a **unique constraint** for upserts to work correctly.

---

## Roadmap

- [ ] Admin drill-down — click a user to view their checklist read-only
- [ ] Per-item timestamps — "checked Mar 18 at 2:34 PM"
- [ ] Export / print view for HR records
- [ ] Multi-org support — white-label per department or location

---

## Background

This started as a personal tool to make an otherwise ignored PDF checklist actually useful. The original? Printed, maybe glanced at, usually forgotten. This version lives at a URL anyone can bookmark, requires zero setup from the new hire, and gives managers visibility without chasing anyone down.

The goal is to eventually make this something any organization can adopt with minimal configuration.

---

*Built with GitHub Pages · Supabase · Google Analytics*
