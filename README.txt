ESMOS - multi-school platform (Supabase version)
==================================================
FILES
- index.html    page shell (landing page, ESMOS Admin, school portals load into it)
- style.css     all styles
- script.js     all logic (set Supabase url/key in const SB at the top of the main code)
- supabase.sql  database + security (run in Supabase SQL Editor; safe to run again after updates)

SETUP (about 10 minutes)
1. supabase.com > New project (use Pro for real schools: daily backups, no pausing).
2. Supabase > SQL Editor > New query > paste all of supabase.sql > Run.
3. Supabase > Authentication > Providers > Email > turn OFF "Confirm email".
4. Supabase > Project Settings > API: copy "Project URL" and the "anon public" key.
   In script.js find   const SB={url:'',key:''}   and fill it in. (anon key only, never service_role)
5. Upload index.html, style.css and script.js together to your domain (same folder).
6. IMMEDIATELY open  https://yoursite/#owner-login  > "First time? Create owner account".
   The first account becomes the ESMOS Admin. Nobody else can become admin afterwards.

ESMOS ADMIN (#owner-login)
- Cards: revenue this month, monthly recurring revenue (MRR), outstanding, schools.
- Schools tab: add school (name, city, contact, fee, paid-until, school admin EMAIL), activate/deactivate, edit, delete,
  Open (enter the school's admin panel), Link, student/staff counts, days left / days overdue.
- Payment: record amount, months and method. Access extends by 30 days per month paid, notice is cleared.
- Notice: sends a custom popup message to that school's admin.
- Remind: opens WhatsApp with a ready payment reminder.
- Revenue tab: 6-month chart + list of schools with payment due.
- Payments tab: full ledger + Export CSV (history stays even if a school is deleted).
- Notice to all / Clear notices: broadcast a popup message to every school admin.
- Revenue tab also shows Top schools by revenue; Payments tab has a printable Receipt per payment.
- Schools tab shows last active date. Website nav has an "Admin login" button.
- Requests tab: website enquiries; Create demo for a lead.

PAYMENT RULES
- Due within 5 days: school admin sees a "Payment reminder" popup.
- Past the paid-until date: "Payment overdue" popup with days left. Access continues for 5 grace days.
- After 5 grace days: the whole school (admin, employees, parents, students) is blocked until you record a payment.
- Deactivate blocks instantly.

SCHOOL FLOW
- Give the school its link  https://yoursite/#s-SCHOOLCODE  (button "Link").
- School admin: Admin Portal > "First time? Create my password" using the registered email.
- Admin adds students/staff and shares logins (Admin > Portal Logins) with employees, parents and students.
  All data is saved to Supabase and visible to you via "Open".

SECURITY NOTES
- Browser can only call the functions in supabase.sql; tables are locked.
- Parents/students receive only their own records (passwords removed). Employees get school data without passwords.
- Employee/parent/student portals are read-only in this version.
- Employee/parent/student passwords are still text inside the school's data (set by the school admin). Next step: Supabase Auth per user.
- School data is saved as one record: fine for a few thousand students; if two admins edit at once the last save wins.

UPDATE: PAYMENT POPUP, SCREENSHOT PROOF AND SUSPENSION (local mode, no Supabase keys)
- Owner > Account > "Edit payment details and grace days": bank, account title, IBAN, JazzCash/Easypaisa, note, grace days (minimum 1, default 5).
- School admin popup: shown when payment is due within 5 days, and again every 5 seconds until paid or confirmed.
  Overdue = no close button (locked). It shows the bank details and a "Send payment screenshot" form (screenshot + transaction ID).
- Owner > Proofs tab: view screenshot, Approve (records payment, +30 days per month, unlocks school) or Reject (notice sent to school).
- After the grace days the whole school is suspended; the suspended page shows the bank details and a screenshot form.
- Owner "Open" shows the popup once with a "Close (owner preview)" button.
- NOTE: in local mode data lives in one browser only. For schools on their own devices, Supabase must be connected
  (screenshots and bank details are not yet in supabase.sql).

UPDATE 2: PAYMENT DETAILS, OWNER REVIEW, PASSWORD RESET, BACKUP (local mode)
- School popup form: payment method, amount, months, transaction ID and screenshot. Owner sees them in Proofs and a "waiting" banner.
- Owner > Schools > Edit: change a school's admin username/password. School data (students, fees, etc.) is never touched.
- Owner > Account > Download backup / Restore from backup file (use on your own domain; backs up all schools).
- #owner-login always opens the owner login, even if a school session is open. The popup has a "Back to ESMOS website" link.
- Data is deleted only by Delete school, Remove all demos, the school's Reset demo data, or clearing browser data.
- Local mode keeps data in one browser. For schools on other devices connect Supabase (not yet extended for screenshots/bank details).


REBRAND: ESMOS logo, green theme. Default local owner login for a fresh install is owner / esmos123 (old installs keep their existing password and data).


UPDATE 3: SCROLL FIX (mobile / Inspect device mode)
- The website and ESMOS Admin pages now scroll as a normal page (before, they scrolled inside a hidden full-screen layer).
  Wheel, touch drag, window.scrollTo(), Back to top, Lighthouse and "Capture full size screenshot" now all work.

UPDATE: SCHOOL BRANDING (per-school look)
- School admin: Setup > "School look and branding" > Customize. Choose a ready theme or own main/dark colours, a font (Poppins, Inter, Nunito, Montserrat, Lato, Roboto, Playfair Display, Merriweather) and an optional login background image.
- The look applies to the admin, employee, parent and student portals of that school. "Reset" restores the default.
- ESMOS Admin can set it for any school: Owner > Open (enter the school) > Setup > Customize.
- Saved inside the school's own data (S.set.theme), so each school keeps its own style.
- Cloud mode: the look is applied once the school data loads (after login); the very first login screen uses the default look.
- Owner > Schools > "Look" button (next to Edit): set colours, font and login background for any school directly, without opening it (local mode). The school's admin, employee, parent and student portals then use that look.
- School logo: in Customize (school admin) or Owner > Schools > Look, upload a square logo. It replaces the cap icon in the sidebar and on the portal login pages of that school (admin, employee, parent, student). "Remove logo" brings back the default.
- Background image: shown on the portal login pages (blurred, tinted with the school colours, with glass-style cards) and on the admin dashboard welcome banner. "Image darkness" slider and "Soften image" option in Customize.


UPDATE: MOBILE BOTTOM BAR FOR ALL PORTALS AND PORTAL LOGINS
- Parent and Student portals now have a bottom icon bar on mobile: Home, Fees, Attendance, Results, Timetable. Employee portal bar shows "Home" first.
- Admin > Portal Logins (also a button on the dashboard banner): tabs for Students, Parents, Employees. Per person: Set password, Generate, Send on WhatsApp, Copy.
- Add/Edit student: Parent portal password and Student portal password (empty = auto-generate).
- Add/Edit staff: Portal username and Portal password (empty = auto-create / auto-generate).


UPDATE: PORTAL LOGINS (many users, daily batches) AND CLASS-WISE RESULTS
- Admin > Portal Logins: tabs Students / Parents / Teachers. Table with search, class filter, status filter (Needs password, Set but not sent, Sent), 25 per page.
- "Generate passwords for next N who need one" (batch size editable) gives each person a unique random password. Default passwords (stud123, parent123, emp123) count as "needs password" and cannot be sent.
- Save a typed password, Generate for one person, WhatsApp (marks as sent), Copy, Export CSV, Print login slips. Two people cannot share a password. Parents with the same WhatsApp number share one row.
- Examinations & Results: teacher picks class, subject, test and total marks, then enters Roll no and Marks for every child and presses Save. Saving again updates, no duplicates. Roll no must be unique in a class.
- Each child's marks appear only in that child's Student portal and Parent portal. Parent sessions now match guardian name AND WhatsApp number.
- Students form has a new optional field: Class roll no.
- Note: teacher saving marks works in local mode. Cloud (Supabase) employee portals are still read-only.


DEFAULT LOGINS (when Supabase is not set up yet, data is saved only in that browser)
- ESMOS Admin (#owner-login): username owner / password esmos123
- Demo school: school code demo > Admin Portal > admin / admin123
- Schools you add in the ESMOS Admin only exist in the browser where you added them. For real use on all devices, add Supabase.
