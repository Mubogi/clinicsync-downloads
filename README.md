# ClinicSync downloads

Offline-first pharmacy, clinic and drug-shop management.
Source code is private; this repo only holds the installers.

## ⬇️ Download here

**➡️ https://github.com/Mubogi/clinicsync-downloads/releases/latest**

| Your device | File to download |
| --- | --- |
| Android phone / tablet | `ClinicSync-1.1.7.apk` |
| Windows PC | `ClinicSync-Setup-1.1.7.exe` |
| Linux PC (portable) | `ClinicSync-1.1.7.AppImage` |
| Linux PC (installer) | `clinicsync_1.1.7_amd64.deb` |
| Check an activation key | `activation.html` (opens offline in any browser) |
| Marketing kit (videos, posters, documents) | `ClinicSync-Marketing-Kit.zip` |

Every file has a SHA-256 checksum in `SHA256SUMS.txt`.

Activation keys are issued by JD Hub. The old in-browser key generator is no
longer distributed: it was a vendor tool and had no place in a customer's
download folder.

## Install notes

**Android.** Tap the `.apk`, then allow "Install unknown apps" for your browser
or file manager if Android asks. If you see "Error parsing package", you
downloaded the wrong file — use the release link above, not the source repo.

**Windows.** Run the `.exe` installer.

**Linux.** AppImage: `chmod +x ClinicSync-1.1.7.AppImage` then run it.
Debian/Ubuntu: `sudo apt install ./clinicsync_1.1.7_amd64.deb`.

## What's new in 1.1.7

- **Fixed: "Something went wrong" when creating your clinic or signing in, after
  a force-stop.** 1.1.6 healed a database with a damaged *data page*, but the
  check only looked inside the pages it could read. A force-stop can instead
  leave the file a different length from what its header describes — the last
  page written only partly, or a page from an interrupted commit appended after
  the last durable one. The file could still pass the page check and open
  normally, so the fault only appeared later, on the first real action
  (registration, the dashboard, a sale), as the same generic **"Something went
  wrong. Please try again."** with no way past it. The app now also compares the
  file size against the header's page count times the page size on start-up. If
  they disagree it sets the file aside as `clinicsync.db.corrupt-<timestamp>`
  (kept, never deleted) and builds a fresh one, so you can create your clinic and
  get in. This rebuild carries the fix to **both** the phone and the PC builds.

Everything from 1.1.6 is included:

- **Fixed: a damaged data page.** The app checks the whole database on start-up,
  and if any page is damaged it sets the file aside
  (kept as `clinicsync.db.corrupt-<timestamp>`) and builds a fresh one.

Everything from 1.1.4 is included:

- **Fixed: creating your clinic offline.** On a phone or PC, "create your clinic
  (free trial)" could fail permanently with "Something went wrong. Please try
  again." A crash or force-stop during a write left the database's lock file
  behind, after which the app could never open its own database again — so no
  account could be created and the app was unusable. The app now clears a
  leftover lock from a previous crash on start-up. Your data is kept.

Everything from 1.1.3 is included:

- **Fixed: creating your clinic after an upgrade.** On a device that already had
  an older version installed, the app now repairs its offline database on
  start-up, so an upgrade keeps working and keeps your data.

## What's new in 1.1.3

- **Fixed: creating your clinic on Android.** On a phone that already had an
  older version installed, tapping "create clinic (free trial)" could stop with
  "Something went wrong. Please try again." The app now repairs its offline
  database on start-up, so an upgrade keeps working and keeps your data.

Everything from 1.1.2 is included:

- **Sell by strip, tablet or box.** Pick the unit at the till and each unit
  carries its own price. Selling single tablets now works.
- **Stock shows its breakdown** — pack sizes and unit-by-unit counts.
- **Who bought what** — sales record a customer name and phone, and Reports has
  a per-customer view plus printable report sheets.
- **Invite QR works offline** — the staff-invite code is drawn on the device.

## Upgrading

Install straight over any 1.0.7 or later build — same signing key, so your data
and settings are kept.
