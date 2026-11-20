# BMC Building Safety

A static website prototype for searching and viewing Mumbai building-safety records.

## Project files

- `index.html` — the website.
- `data/c1.psv` and `data/c1.js` — the published BMC C1 building list loaded by the prototype (source list dated 30 April 2026).
- `data/graded.psv` and `data/graded.js` — the data structure for C2A, C2B and C3 entries. The files currently contain instructions/examples only; they are not a verified building-level dataset.
- `data/coords.js` — coordinate data used by the map. It is empty until coordinates are generated.
- `scripts/geocode.mjs` — optional helper to look up approximate/address coordinates for the C1 list.

The prototype may show approximate ward-area locations where verified building-level coordinates are unavailable. A map marker must not be treated as an exact building pin unless its coordinate precision is verified. Absence from the C1 list is not a safety certificate.

## Optional coordinate generation

Requires Node.js 18 or later. Run from the repository root.

**Windows PowerShell**
```powershell
$env:CONTACT = "BMC Building Safety prototype (your-email@example.com)"
node scripts/geocode.mjs
```

**macOS / Linux**
```bash
CONTACT="BMC Building Safety prototype (your-email@example.com)" node scripts/geocode.mjs
```

Use a real contact address in the User-Agent. The script queries the public OpenStreetMap Nominatim service at a cautious rate and writes both `data/coords.json` and `data/coords.js`. Review the resulting locations before publishing them as building-level coordinates.

## Optional Mapillary images

The Mapillary integration is disabled by default. A client token is optional; the site can deploy without one. The token is used by browser-side code, so do not treat it as a secret or put a privileged server token in this public repository.

## Deploy on Vercel

This is a plain static site:

- Framework preset: **Other**
- Root directory: repository root
- Build command: leave blank
- Output directory: `.` (or leave the default for Other)
- Install command: leave blank

Import this GitHub repository into Vercel and deploy. No environment variables are required for the basic site.
