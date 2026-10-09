# HVAC Job Pipeline

**Every install and service call, from first call to paid.**

A lightweight job pipeline for HVAC companies, built entirely on Google Workspace. It gives teams a powerful, tailored tool without an expensive field-service subscription: Google Apps Script runs the app, Google Sheets is the database, and Google Drive stores job files privately.

### 👉 [Try the live demo](https://masystemsolutions.github.io/HVAC-Pipeline/)

Pick a demo role: **Owner / admin**, **Dispatcher**, or **Subcontractor**. No sign-up needed. Everything is fictional sample data, @mention emails are previewed instead of sent, and the demo resets every night.

> Tip: try the **Subcontractor** role. You'll only see Precision Duct Co.'s jobs, with no pricing and no internal notes.

<!-- Add screenshots here, e.g.
![Dashboard](screenshots/dashboard.png)
![Install board](screenshots/install-board.png)
![Job panel](screenshots/job.png)
-->

---

## Features

| | |
|---|---|
| **Two pipelines in one place** | **Installs** move through 11 stages (New Lead → Estimate → Proposal → Contract Signed → Financing → Permit → Equipment Ordered → Installed → Inspection → Invoiced → Closed). **Service calls** move through 8 (New Call → Scheduled → Tech Dispatched → Diagnosing → Waiting on Parts → Work Completed → Invoiced → Paid). |
| **Dispatch-ready dashboard** | Emergency calls first, then the next two days' schedule; install and service pipeline charts; open install value; and unpaid invoices. |
| **Stuck-job alerts** | Every stage has a target time. Jobs that sit too long, like parts that never arrived, are flagged automatically. |
| **Subcontractor views** | Subcontractors only see jobs assigned to their company, and **never see pricing**: estimates, invoices and payment status are removed on the server before anything reaches them. |
| **Team feed with @mentions** | Tag a tech, the office or a sub, and they get an email with a link that opens the job. |
| **Internal notes & files** | Mark a note or file internal (pricing, margins, disputes) and subcontractors never see it and can't be tagged in it. Replies to internal notes stay internal. |
| **Work order PDFs** | One click creates a crew-ready work order (no pricing), or an internal version with pricing, saved to the job's Drive folder. |
| **Private file storage** | Each job gets its own Drive folder automatically for photos, proposals, permits and reports. |

## Security

- Salted, hashed passwords, expiring sessions, and lockout after repeated failed logins
- Optional **domain lock**: staff must use the company email domain (subcontractors are exempt)
- Role, company and internal-note checks on every server request; access changes apply immediately
- All text escaped (no XSS) and protected against spreadsheet formula injection
- Locking to prevent overlapping saves, sequential job IDs, and a full activity log of who changed what

## Tech stack

Google Apps Script · Google Sheets · Google Drive · MailApp · HTML/CSS/JavaScript · Bootstrap 5 · Bootstrap Icons

## Project structure

```
apps-script/
├── Code.gs       # server: auth, roles, pipelines, files, work orders, emails, demo data
└── index.html    # the whole front end (single page)
index.html        # GitHub Pages wrapper that loads the live app
```

## Run your own copy

1. Create a **new, blank** Google Sheet, then open **Extensions → Apps Script**.
2. Paste `apps-script/Code.gs` into `Code.gs`. Add an HTML file named `index` and paste `apps-script/index.html`.
3. Select the `setup` function and click **Run**, then approve the permissions.
4. **Deploy → New deployment → Web app**, with *Execute as: Me* and *Who has access: Anyone*.
5. Paste the `/exec` link into the root `index.html` (the line marked ⬇️) for GitHub Pages.
6. For real use: set `DEMO_MODE: false` (and optionally `STAFF_DOMAINS`) in `Code.gs`, run `setup` again, and create the first admin with `addUserAccount`.

---

Built by **MA System Solutions**.
