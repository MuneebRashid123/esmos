# ESMOS - School Management System (Supabase edition)

Static site (index.html, style.css, script.js). Open `index.html` or host on GitHub Pages / any static host.

Backend: Supabase project **esmos** (ap-south-1). URL and anon key are set at the top of `script.js` (`const SB=`).

- **Data**: one row per school in `school_data`, saved automatically a moment after every change. Green badge bottom-left shows "Saved to Supabase <time>".
- **Logins**: school admin, owner, teachers, parents and students are all Supabase Auth users. Passwords are never stored in school data (the server strips them). Portal accounts are created by the `esmos-users` Edge Function when the admin sets a password in Portal Logins.
- **Images**: logo and background are uploaded to the public Storage bucket `esmos-images/<school-code>/...`; only the link is saved in school data.
- **Backups**: automatic copy while working (every 6 h), daily copy (cron 21:30 UTC), safety copy before a big delete. Settings > Backup: Back up now, Download JSON, Restore.
- **Demo**: "Try live demo" and demo schools run in the browser only. The server never saves or backs up demo data.

First time: open `index.html?setup=YOUR-ONE-TIME-CODE#owner-login`, press "Create owner account" with graphicdynamix.co@gmail.com, then Add school (enter the school admin's email). The admin opens the school's login page, chooses Admin, and creates a password.

The owner account can only be created with the one-time setup code (stored hashed in the `setup_codes` table, single use, expires). Never commit the code to GitHub. Passwords must be at least 8 characters.
