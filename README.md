<div align="center">

<img src="img/og.png" alt="CoalTrack" width="820">

<h1>⛏️ CoalTrack</h1>

<h3>Anti-fraud attendance + automatic payroll for coal-mining operations</h3>

<p>
<img alt="Flutter" src="https://img.shields.io/badge/Flutter-02569B?style=flat-square&logo=flutter&logoColor=white">
<img alt="Laravel 12" src="https://img.shields.io/badge/Laravel%2012-FF2D20?style=flat-square&logo=laravel&logoColor=white">
<img alt="PostgreSQL 16" src="https://img.shields.io/badge/PostgreSQL%2016-4169E1?style=flat-square&logo=postgresql&logoColor=white">
<img alt="Vue 3" src="https://img.shields.io/badge/Vue%203-4FC08D?style=flat-square&logo=vuedotjs&logoColor=white">
<img alt="Docker" src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white">
</p>
<p>
<img alt="Tests" src="https://img.shields.io/badge/tests-207%20passing-3C8A12?style=flat-square&logo=checkmarx&logoColor=white">
<img alt="Languages" src="https://img.shields.io/badge/languages-5%20(EN%C2%B7ID%C2%B7MS%C2%B7ZH%C2%B7AR)-6BBE33?style=flat-square">
<img alt="Biometric" src="https://img.shields.io/badge/login-Face%20ID%20%2F%20Fingerprint-124C08?style=flat-square">
<img alt="Status" src="https://img.shields.io/badge/status-pilot--ready-2F7009?style=flat-square">
</p>

<p><b>Built for <a href="https://ksatriabintangsamudra.my.id">Qubah Group</a></b></p>

<h3><a href="https://ksatriabintangsamudra.my.id/coaltrack-showcase/">▶ Open the live showcase</a></h3>

<p><em>Per-slide presentation · flag switcher for <b>5 languages</b> (top-right) · English default · full RTL</em></p>

<br>

<img src="img/demo.gif" alt="CoalTrack employee app demo" width="300">

</div>

> ℹ️ This is the **public showcase / portfolio** repository. **The full source code is private** to keep it easy to evolve.

---

## ✨ What it does

**CoalTrack turns honest attendance into accurate payroll — automatically.** Employees clock in with **face + real GPS** in two taps; the server decides on **immutable, tamper-proof** rules; verified hours flow straight into a **compliant payroll engine** (BPJS, PPh21 TER, overtime) that produces a **PDF payslip**. One Flutter app for **iOS & Android**, a **Laravel** API, and a **Vue** HR portal.

| 🛡️ Anti-fraud | 🙂 Face + liveness | 📍 Real GPS | 🔐 Biometric login | 🌐 5 languages | ✅ 207 tests |
|:---:|:---:|:---:|:---:|:---:|:---:|

---

## 👥 Two roles, one app

The app opens the right surface automatically from the signed-in role — no separate apps.

| 👤 **Employee** — *records their own attendance* | 🛡️ **Admin / HR** — *controls & monitors everything* |
|:---|:---|
| ✓ Face + GPS attendance (2-tap, server time) | ✓ Operations dashboard (on-site headcount, cost) |
| ✓ Attendance history + decision status | ✓ Real-time monitor (present/late, mock-GPS flags) |
| ✓ Payslip (breakdown + PDF) | ✓ Leave approvals (approve / reject + reason) |
| ✓ Leave & permits (+ remaining quota) | ✓ Device management (1 phone / employee) |
| ✓ Notifications | ✓ Employee directory (search, filter) |
| ✓ Profile & theme (5 languages) | ✓ Payroll run → pay → PDF slip → Telegram/Email |

---

## 🔐 Security — sign in once, then just your face or finger

| First sign-in | Face ID / fingerprint | One-tap enable |
|:---:|:---:|:---:|
| <img src="img/sec-login.en.png" width="210"> | <img src="img/sec-lock.en.png" width="210"> | <img src="img/sec-setup.en.png" width="210"> |

First login uses a **password** on the device; after that **Face ID / Touch ID (iOS)** or **fingerprint / face-unlock (Android)** — adapting to each phone via `local_auth`. Sessions are **encrypted** (`flutter_secure_storage`), **device-bound** (1 phone per employee), and re-lock automatically when the app is backgrounded. **Screenshots are blocked** on sensitive screens (Android `FLAG_SECURE` + iOS app-switcher blur).

### The six layers that close the fraud gaps

**Server time** · **Device binding** · **Immutable append-only log** · **Face + liveness** · **Real GPS + mock detection** · **Evidence-based decision engine** *(fails safe)*.

---

## 🆚 Manual / Excel vs CoalTrack

| Aspect | Manual / Excel | CoalTrack |
|---|---|---|
| Attendance time | ✕ Phone clock, manipulable | ✓ **Server time, tamper-proof** |
| Buddy-punching | ✕ Undetected | ✓ **Face + 1 phone/employee** |
| Payroll recap | ✕ Days of manual work, error-prone | ✓ **Automatic from attendance** |
| Reporting | ✕ Monthly, late | ✓ **Real-time** |
| Tax & BPJS | ✕ Manual, error-prone | ✓ **PPh21 TER + BPJS automatic** |
| Cost leakage | ✕ ~Rp 7.47 B / year | ✓ **Closed** |

---

## 📱 The app

| Home | Attend ⭐ | History | Payslip |
|:---:|:---:|:---:|:---:|
| <img src="img/emp-home.en.png" width="200"> | <img src="img/emp-absen.en.png" width="200"> | <img src="img/emp-riwayat.en.png" width="200"> | <img src="img/emp-slip.en.png" width="200"> |

| Leave & permits | Notifications | Edit profile | Beautiful dark mode |
|:---:|:---:|:---:|:---:|
| <img src="img/leave.en.png" width="200"> | <img src="img/notif.en.png" width="200"> | <img src="img/edit-profile.en.png" width="200"> | <img src="img/home-dark.en.png" width="200"> |

### 🖥️ The control room — Admin / HR

| Dashboard | Live monitor | Devices | Employees |
|:---:|:---:|:---:|:---:|
| <img src="img/dash.en.png" width="200"> | <img src="img/monitor.en.png" width="200"> | <img src="img/devices.en.png" width="200"> | <img src="img/employees.en.png" width="200"> |

---

## 🔄 From clock-in to payslip — one pipeline

```
📲 Attendance  ─▶  🖥️ Server decision  ─▶  ⏱️ Work session  ─▶  🧮 Payroll engine  ─▶  🧾 Payslip
 face + GPS         server time,            verified hours       overtime, BPJS,        PDF + Telegram
 2 taps             immutable log           per day              PPh21 TER              / Email
```

Honest attendance feeds accurate payroll — **no manual recaps, no gaps**.

---

## 🏗️ Architecture

```
📱 Flutter (employee + admin)  ─┐
                                ├─▶  🔌 Laravel 12 API (Sanctum)  ─▶  🗄️ PostgreSQL 16 (append-only)
🖥️ Vue 3 (HR portal)          ─┘

Attendance (authoritative, immutable) → Work sessions → Shift/Roster → Payroll engine → Payslip
```

**Backend** PHP 8.3 · Laravel 12 · PostgreSQL 16 · Sanctum · Pest (**207 tests**) · Docker
**Web** Vue 3 · Vite · Tailwind · Pinia
**Mobile** Flutter · Riverpod · go_router · dio · local_auth · flutter_secure_storage

---

## 🚦 Status

| Area | Status |
|---|---|
| Backend + anti-fraud API (207 tests) | ✅ done |
| Web portal (employee + admin/HR) | ✅ done |
| Mobile employee (attend, history, pay, leave, notifications, profile) + **real GPS** | ✅ done |
| **Biometric login** (Face ID / fingerprint) + app-wide screenshot protection | ✅ done |
| Payroll engine (BPJS, PPh21 TER, overtime) + PDF payslip · **20 tests** | ✅ done |
| Admin (dashboard, live monitor, devices, employees) | ✅ done |
| Payroll run → pay + PDF slip · Telegram/Email delivery | ✅ done |
| Leave approvals (HR) | ✅ done |
| FCM push & face-ML liveness | → next |

---

<div align="center"><sub>Technical showcase by <a href="https://ksatriabintangsamudra.my.id">Ksatria Bintang Samudra</a> · source code is private</sub></div>
