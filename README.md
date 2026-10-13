# SRM Prime, Ramapuram — MedFlow

Real-time operations gateway for hospital managers and on-duty physicians at **SRM Prime, Ramapuram**.

| Page | Purpose |
|------|---------|
| `index.html`   | Landing / portal selector |
| `manager.html` | Manager's Tab (beds, shifts, alerts, appointments) |
| `doctor.html`  | Doctor App (Code Red attend lock, EMR consults, discharge) |

Each page is a single self-contained HTML file (inline CSS + JS). Only the logo images live in `assets/img/`.

## Run locally
Open `index.html` in a browser, or serve the folder: `python3 -m http.server 8080`.
To see cross-window sync, open `manager.html` and `doctor.html` in two tabs.

## Deploy (GitHub Pages)
Settings → Pages → Deploy from branch → `main` / root. Keep `assets/` next to the HTML files.

## Doctor login (demo)
`doctor.html` opens on a sign-in screen. Pick department, then doctor. Password = **first name + `07`**
(e.g. `Rajesh07`, `Arvind07`; not case-sensitive). The doctor list lives in `DOCTOR_DIRECTORY`
at the top of the script in `doctor.html` and mirrors `medicalSpecialties` / `dynamicIndianStaff` in `manager.html`;
if you add a doctor, add them in both files. Each doctor only sees their own appointments.
This is client-side demo authentication only, not real security.

## Prescriptions
When a doctor taps **Save & Sync Custom Plan to EMR**, the plan (notes, risk, follow-up, orders) is saved and sent to the manager.
In `manager.html` → **5. Appointments**, attended rows get a **Prescription** button: printer animation, preview, then **Download (PDF)**.
The PDF is generated in the browser with no libraries (works offline); the logo is embedded as base64 inside `manager.html`.

## Digital signature & zoom lock
- Saving a plan in `doctor.html` signs it as the logged-in doctor: a SHA-256 checksum over the prescription fields plus the signer and time. `manager.html` re-checks it when opening or downloading and shows **Digitally signed**, **Signature invalid** (content changed) or **Not digitally signed** (older records). This is an electronic signature with tamper detection, not a certificate-based (DSC/PKI) signature.
- Zoom is locked on all pages (viewport meta + pinch / double-tap / ctrl+wheel / keyboard shortcut blockers). Browser-menu zoom can't be disabled by a web page.
