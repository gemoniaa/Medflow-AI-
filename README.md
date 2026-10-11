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
