# ClinicSync downloads

Offline-first pharmacy, clinic and drug-shop management.
Source code is private; this repo only holds the installers.

## ⬇️ Download here

**➡️ https://github.com/Mubogi/clinicsync-downloads/releases/latest**

| Your device | File to download |
| --- | --- |
| Android phone / tablet | `ClinicSync-1.1.5.apk` |
| Windows PC | `ClinicSync-Setup-1.1.5.exe` |
| Linux PC (portable) | `ClinicSync-1.1.5.AppImage` |
| Linux PC (installer) | `clinicsync_1.1.5_amd64.deb` |
| Check an activation key | `activation.html` (opens offline in any browser) |

Activation keys are issued by JD Hub. The old in-browser key generator is no
longer distributed: it was a vendor tool and had no place in a customer's
download folder.

## Install notes

**Android.** Tap the `.apk`, then allow "Install unknown apps" for your browser
or file manager if Android asks. If you see "Error parsing package", you
downloaded the wrong file — use the release link above, not the source repo.

**Windows.** Run the `.exe` installer.

**Linux.** AppImage: `chmod +x ClinicSync-1.1.5.AppImage` then run it.
Debian/Ubuntu: `sudo apt install ./clinicsync_1.1.5_amd64.deb`.

## What's new in 1.1.5

- **Fixed: creating your clinic when the database is unreadable.** 1.1.4 healed a
  leftover lock file, but a crash or force-stop during a write can leave the
  embedded database in a worse state: the bytes on disk are no longer a valid
  database at all, so the app never finished starting and every screen — including
  "create your clinic (free trial)" — failed with "Something went wrong. Please
  try again." The app now sets that unreadable file aside as
  `clinicsync.db.corrupt-<timestamp>` (kept, never deleted) and builds a fresh
  database, so a new owner can create their clinic and get in. This rebuild
  carries the fix to **both** the phone and the PC builds.

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
