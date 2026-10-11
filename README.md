<div align="center">

<img src="img/coaltrack-mark.png" alt="CoalTrack" width="150">

# CoalTrack

### Anti-fraud attendance + automatic payroll for coal-mining operations

<p>
<a href="https://coaltrack.id"><img alt="Showcase" src="https://img.shields.io/badge/showcase-coaltrack.id-F5A524?style=for-the-badge&labelColor=0B1220"></a>
</p>

<p>
<img alt="Flutter" src="https://img.shields.io/badge/Flutter-0B1220?style=flat-square&logo=flutter&logoColor=F5A524">
<img alt="Laravel 12" src="https://img.shields.io/badge/Laravel%2012-0B1220?style=flat-square&logo=laravel&logoColor=F5A524">
<img alt="PostgreSQL 16" src="https://img.shields.io/badge/PostgreSQL%2016-0B1220?style=flat-square&logo=postgresql&logoColor=F5A524">
<img alt="Filament 5" src="https://img.shields.io/badge/Filament%205-0B1220?style=flat-square&logo=laravel&logoColor=F5A524">
<img alt="Docker" src="https://img.shields.io/badge/Docker-0B1220?style=flat-square&logo=docker&logoColor=F5A524">
</p>
<p>
<img alt="Tests" src="https://img.shields.io/badge/tests-486%20app%20%2B%20520%20API-F5A524?style=flat-square&labelColor=13213A">
<img alt="Languages" src="https://img.shields.io/badge/languages-7-F5A524?style=flat-square&labelColor=13213A">
<img alt="Login" src="https://img.shields.io/badge/unlock-Face%20ID%20%2F%20Fingerprint-F5A524?style=flat-square&labelColor=13213A">
<img alt="Tenancy" src="https://img.shields.io/badge/multi--tenant-licensed-F5A524?style=flat-square&labelColor=13213A">
<img alt="Status" src="https://img.shields.io/badge/status-v1.8.0%20%C2%B7%20in%20pilot-F5A524?style=flat-square&labelColor=13213A">
</p>

**A product of Ksatria Bintang Samudra**

<img src="img/emp-home.en.webp" alt="CoalTrack employee app — Home" width="280">

</div>

> **This is the public showcase / portfolio repository.** It contains the marketing deck at
> [coaltrack.id](https://coaltrack.id) and its screenshots. **The application source code is private.**

---

## What CoalTrack does

Attendance recaps in a mining operation are usually a spreadsheet problem: the phone clock can be
changed, a friend can clock in for you, and by the time payroll is assembled nobody can prove what
really happened. CoalTrack closes that loop end to end.

A worker clocks in with **real GPS + server time** in one tap — with or without signal. The
**server** decides, using its own clock, and writes an **append-only** event that nobody can edit
later. Verified hours roll into **work sessions**, work sessions into a **payroll engine** that
computes overtime, BPJS and **PPh21 TER**, and HR finalises the period in a **web panel** that
emails every **PDF payslip** and shows the same slip inside the employee's app.

One Flutter app for iOS and Android (the employee app), a Laravel 12 API, and a Filament 5 web
panel for HR.

---

## Key features

### Anti-fraud attendance — six layers

| | Layer | What it closes |
|---|---|---|
| 1 | **Server time** | Decisions use the server clock. Changing the phone clock does nothing. |
| 2 | **Device binding** | One approved device per employee. Buddy-punching from a colleague's phone is blocked. |
| 3 | **Immutable log** | Attendance events and reviews are append-only (enforced by a DB trigger). History cannot be rewritten. |
| 4 | **Trusted clock + work-hour windows** | The server stamps each check-in with its own trusted clock and enforces the work-hour window — even for check-ins captured offline, using the satellite time. |
| 5 | **Real GPS + work-site radius** | Real device location with mock-location detection. Work sites carry a radius: HR sees the distance to the nearest site and can reject check-ins outside it. |
| 6 | **Decision engine** | Accept / reject / flag on the evidence — and it fails safe. |

Attendance also works with **no signal**: the check-in is recorded on the phone with the real GPS
fix and the GPS-satellite time, kept in a local queue, and uploaded by itself the moment signal
returns — on app resume, every two minutes, and right after sign-in. Offline check-ins arrive
flagged with their reason; HR accepts, voids or restores them in the panel — never edits.

### HR web panel

HR works from a laptop, in Bahasa Indonesia, light or dark:

- **Dashboard** — who is on site now, present and late today, attendance trend, contracts about to
  expire.
- **Attendance review** — every event with its risk signals; void or restore with a reason, never edit.
  Monthly recap per division with Excel export.
- **Leave approvals** — annual leave, permit, sick, business trip and work-from-home; an approved request
  gets a numbered official letter on company letterhead (PDF).
- **Work schedules & work sites** — check-in window, late threshold, work days, sites with a radius —
  saved as dated versions.
- **Devices** — approve or revoke the one phone each employee may use; a replacement phone waits for HR.
- **Employees & divisions** — directory, CSV import, contract-expiry reminders for fixed-term employees.
- **Payroll** — payroll settings (BPJS contributions and caps, PPh21 TER tables, overtime divisor),
  salary grades per position, a what-if simulator, then run → review → finalise → email the PDF
  payslips (password-locked). PPh 21 export in Coretax format.

### Payroll

- Payslips computed from verified attendance — **BPJS**, **PPh21 TER**, overtime tiers per
  Kepmenaker 102/2004, allowances, night-shift, production incentives, cut-off — configurable per company.
- Base salary is never cut for lateness; lateness and absence reduce the attendance allowance (or, if the
  company rules say so, a daily rate per PP 36/2021). Monthly, daily and hourly pay schemes.
- The engine is written twice on purpose — PHP on the server, Dart in the app — and cross-tested so
  both produce identical figures.
- **Real payslips in the app** once HR finalises the period; **PDF payslip** by email,
  password-locked; **PPh 21 export** in Coretax format.
- **Company rules are versioned, never retroactive**: payroll settings and work schedules are dated
  versions; a change applies from its effective date onward.
- Money never passes through CoalTrack. Funds leave the company's own bank account only after the
  company's own approver releases them.

### Payslip delivery — email from an authenticated sending domain

Payslips go out from CoalTrack's own **fully authenticated sending domain** (SPF, DKIM, DMARC), so
they land in the inbox rather than the spam folder and cannot be forged. There is no mail server for
the customer to run; sending from the **customer's own domain is available on request**. Each
employee receives a clean letter with the official **PDF payslip attached**, password-locked. Sending is queued per employee; anyone without an email address is listed back to HR so
they get a printed slip instead of silence. Email runs alongside the in-app payslip and print.

### Roles, teams and tenancy

- **Employee** — attendance (online and offline), history, leave & permits with official letters,
  payslip, profile & security.
- **Division head** — approves the exceptions for their own team.
- **HR** — the web panel: visibility across divisions, attendance review, payroll runs.
- **Super-admin** — full control of the organisation and its settings.
- **Multi-tenant, licensed** — one deployment serves several companies with isolated data, each on
  its own licence and its own configuration.

### Everywhere, in 7 languages

The employee app and this showcase speak English, Indonesian, Malay, Chinese, Arabic (full RTL),
Thai and Filipino — switchable at any time. Every screen is designed for both light and dark mode.
The HR panel is in Bahasa Indonesia.

---

## Screens

**Employee app**

| Home | Attend | History | Payslip |
|:---:|:---:|:---:|:---:|
| <img src="img/emp-home.en.webp" width="190"> | <img src="img/emp-absen.en.webp" width="190"> | <img src="img/emp-riwayat.en.webp" width="190"> | <img src="img/emp-slip.en.webp" width="190"> |

| Dark mode | Leave & permits | Edit profile | Pay tab |
|:---:|:---:|:---:|:---:|
| <img src="img/home-dark.en.webp" width="190"> | <img src="img/leave.en.webp" width="190"> | <img src="img/edit-profile.en.png" width="190"> | <img src="img/emp-gaji.en.png" width="190"> |

**HR web panel**

| Dashboard | Attendance review | Devices |
|:---:|:---:|:---:|
| <img src="img/panel-dash.webp" width="300"> | <img src="img/panel-absensi.webp" width="300"> | <img src="img/panel-perangkat.webp" width="300"> |

| Salary grades | Payroll runs & email slips | Run detail: cost summary & payslips |
|:---:|:---:|:---:|
| <img src="img/panel-skala.webp" width="300"> | <img src="img/panel-gaji-run.webp" width="300"> | <img src="img/panel-gaji-detail.webp" width="300"> |

**Sign in once, then tap to unlock**

| First sign-in | Face ID / fingerprint | One-tap enable |
|:---:|:---:|:---:|
| <img src="img/sec-login.en.png" width="190"> | <img src="img/sec-lock.en.png" width="190"> | <img src="img/sec-setup.en.png" width="190"> |

**Licensing &amp; payslip**

| Sign-in & company activation | Work schedules | Payslip PDF |
| :---: | :---: | :---: |
| <img src="img/activate.en.webp" width="190"> | <img src="img/panel-jamkerja.webp" width="300"> | <img src="img/slip-pdf.png" width="190"> |
| One app for every company: a fresh install is neutral CoalTrack. Employees sign in with the phone number and password HR gives them; the company is activated once per device and remembered afterwards. | Company rules are edited by the client's own HR in the panel; statutory rates stay locked. | Official payslip PDF, in the app and by email from an authenticated sending domain. |

First login uses a password on the device; after that one tap unlocks with Face ID / Touch ID (iOS)
or fingerprint (Android), adapted to each phone. Sessions are encrypted and device-bound, re-lock
when the app is backgrounded, and screenshots are blocked on sensitive screens.

---

## Manual / Excel vs CoalTrack

| Aspect | Manual / Excel | CoalTrack |
|---|---|---|
| Attendance time | ✕ Phone clock, manipulable | ✓ **Server time, tamper-proof** |
| Buddy-punching | ✕ Undetected | ✓ **One approved phone per employee + real GPS** |
| No signal on site | ✕ Written on paper, typed in later | ✓ **Captured offline, uploads itself** |
| Payroll recap | ✕ Days of manual work, error-prone | ✓ **Automatic from attendance** |
| Reporting | ✕ Monthly, late | ✓ **Real-time** |
| Tax & BPJS | ✕ Manual, error-prone | ✓ **PPh21 TER + BPJS automatic** |
| Payslip delivery | ✕ Printed and handed out | ✓ **In the app + PDF by email from an authenticated domain** |

---

## Pipeline

```
Attendance    ─▶  Server decision  ─▶  Work session   ─▶  Payroll engine   ─▶  Payslip
real GPS + time   server time,         verified hours     overtime, BPJS,      in-app + PDF
online/offline    immutable log        per day            PPh21 TER            by email
```

## Architecture

```
Flutter (employee app)     ─┐
                            ├─▶  Laravel 12 API (Sanctum)  ─▶  PostgreSQL 16 (append-only)
Filament 5 (HR web panel)  ─┘

Attendance (authoritative, immutable) → Work sessions → Payroll engine → Payslip
```

**Backend** PHP 8.3 · Laravel 12 · PostgreSQL 16 · Sanctum · Filament 5 · Pest (520 tests) · Docker · Caddy
**Mobile** Flutter (iOS / Android) · Riverpod · go_router · dio · geolocator · local_auth · flutter_secure_storage · 486 tests

---

## Status

| Area | Status |
|---|---|
| Backend + anti-fraud API (520 Pest tests) | ✅ done |
| HR web panel — dashboard, attendance review, work schedules, devices, employees, import | ✅ done |
| Mobile employee — attend online & offline, history, pay, profile, security, verified badge | ✅ done |
| Tap-to-unlock biometrics + app-wide screenshot protection | ✅ done |
| Payroll engine (BPJS, PPh21 TER, overtime) — same engine on server and app | ✅ done |
| Payroll in the panel — settings, salary grades, simulator, run → finalise → email PDF slips | ✅ done |
| Offline queue that uploads itself when signal returns | ✅ done |
| Leave & permits in the app — leave, permit, sick, business trip, WFH, with numbered official letters (PDF) | ✅ done |
| Work sites with a radius, contract-expiry reminders, PPh 21 export in Coretax format | ✅ done |

> **Honest note:** the pilot customer runs on CoalTrack's hosted backend (Singapore region).
> There is no public demo build. Demo access is granted on request: fill in the form at
> [coaltrack.id/#demo-request](https://coaltrack.id/#demo-request) and we set up a 14-day demo account.

---

## About this repository

| File | What it is |
|---|---|
| `index.html` | The showcase deck — 22 scroll-snap slides, 7 languages, no build step, no dependencies |
| `privacy.html`, `terms.html`, `support.html` | Legal & support pages (ID / EN) |
| `img/` | Product screenshots per language, HR panel captures (`panel-*.webp`), brand marks, OG image |
| `CNAME` | GitHub Pages custom domain (`coaltrack.id`) |

The deck reads a few constants near the top of the inline script in `index.html`:

```js
const SALES_WA = '6285264402640';            // WhatsApp, international format, digits only
const SALES_EMAIL = 'support@coaltrack.id';  // fallback when SALES_WA is empty
const DEMO_REQUEST_ENDPOINT = 'https://app.coaltrack.id/api/v1/demo-requests'; // "Request demo access" form (POST JSON)
const STORE_ANDROID_URL = '';                // Google Play link — badge renders without a link while empty
const STORE_IOS_URL = '';                    // App Store link — badge says "coming soon" while empty
```

While `SALES_WA` is empty the primary button falls back to email, and while a store URL is empty its
badge renders without a link, so nothing breaks.

---

## Talk to us

- **Showcase** — [coaltrack.id](https://coaltrack.id)
- **Demo access** — on request, via the form at [coaltrack.id/#demo-request](https://coaltrack.id/#demo-request)
- **WhatsApp** — [+62 852-6440-2640](https://wa.me/6285264402640)
- **Email** — [support@coaltrack.id](mailto:support@coaltrack.id)

<div align="center"><sub>CoalTrack — a product of <a href="https://coaltrack.id">Ksatria Bintang Samudra</a> · application source code is private</sub></div>
