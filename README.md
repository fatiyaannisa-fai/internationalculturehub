# RZ Internal Portal (Single-File HTML App)

This project is a single self-contained `index.html` page used as an internal portal (English Hour reporting, leaderboard, forum, and an admin panel for managing accounts/roles). It uses vanilla JavaScript, Tailwind CSS (via CDN), Font Awesome, and browser `localStorage` for storing users and content — no backend server or build step is required.

## Key technologies
- Plain HTML/CSS/JavaScript (no framework, no bundler)
- Tailwind CSS via CDN
- Font Awesome via CDN
- Google Identity Services (optional Google SSO, configured by an Admin)
- Browser `localStorage` for persistence

## Running locally
Just open `index.html` in a browser, or serve it with any static file server, e.g.:

```bash
npx serve .
```

Then visit the printed local URL.

## Admin: bulk-adding users via CSV
In the Admin Control Panel → User & Access Management modal, there is now a "Bulk Import Akun via CSV" section in addition to the single-user form. Upload a `.csv` file with the columns:

```
name,email,password,role
```

- `password` and `role` are optional — defaults are `changeme123` and `visitor`.
- A header row is optional and automatically ignored if present.
- Rows with an email that's already registered are skipped.
