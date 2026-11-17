# ClinicSync downloads

Offline-first pharmacy, clinic and drug-shop management.
Source code is private; this repo only holds the installers.

## ⬇️ Download here

**➡️ https://github.com/Mubogi/clinicsync-downloads/releases/latest**

| Your device | File to download |
| --- | --- |
| Android phone / tablet | `ClinicSync-1.1.12.apk` |
| Windows PC | `ClinicSync-Setup-1.1.12.exe` |
| Linux PC (portable) | `ClinicSync-1.1.12.AppImage` |
| Linux PC (installer) | `clinicsync_1.1.12_amd64.deb` |
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

**Linux.** AppImage: `chmod +x ClinicSync-1.1.12.AppImage` then run it.
Debian/Ubuntu: `sudo apt install ./clinicsync_1.1.12_amd64.deb`.

## What's new in 1.1.12

- **Fixed: the phone's "Something went wrong" when you create your clinic —
  the real cause this time.** 1.1.11 made the app report the true error instead
  of the generic sentence, and the phone reported:

  `"fatal" option is not supported in node js compiled without icu (ERR_NO_ICU)`

  The database client the app uses asks the phone's JavaScript engine for
  strict UTF-8 decoding when it starts. The engine built into the Android app
  is a compact one **without** the international text (ICU) component, so it
  refuses that request — and the database client then fails to start at all, so
  **every** action on the phone fails, including creating your clinic. The PC
  was never affected because the engine it ships includes ICU. This build
  teaches the app to work without ICU, so the phone starts the database
  normally. Nothing to do on your phone.

- The app's health check reports the running build (1.1.12), so support can
  confirm which version a phone is on with one request.

Everything from 1.1.11 and earlier is included: a stale lock left by a
force-stop is cleared automatically before a write, and when something fails on
the device itself the app returns the real message instead of the generic
sentence. Older fixes remain too: a database that can be read but not written is
repaired at start-up (a fresh install included), a healthy database is never set
aside, the app opts out of Android backup so a reinstall really starts clean, and
a damaged data page is set aside and kept.

## What's new in 1.1.10

- **Fixed: the phone could still fail after a fresh install.** 1.1.9 checked the
  database for write damage only when a database already existed, so a brand-new
  install skipped the check. A force-stop can leave the app in exactly the state
  that check was meant to catch — a database it can open for reads but not write.
  It boots, the login screen looks fine, and then your first "create clinic"
  fails with the generic **"Something went wrong. Please try again."** The check
  now runs on every start-up, a fresh install included.

- **Fixed: reinstalling the app brought the old data back.** Android was backing
  up the app's private folder, so after an uninstall and reinstall the previous
  database — damage and all — came straight back. That is why reinstalling never
  cleared the error. The app now opts out of Android backup and device-to-device
  transfer, so a fresh install really starts clean.

- **Fixed: an upgrade could refuse to start.** Repairing an older database's
  missing columns rewrote `DEFAULT CURRENT_TIMESTAMP` into an invalid
  `DEFAULT NOT NULLSTAMP`, so an app upgrading from an older build could fail to
  boot with a syntax error. The rewrite is corrected.

- **Fixed: a request the phone mangled now gets a clear answer.** A request body
  the phone's native HTTP bridge mis-serialised used to fall through to the same
  generic "Something went wrong" 500. It now returns a 400 that says the request
  could not be read.

- The app's health check now reports the running build, so support can confirm
  exactly which version a device is on.

Everything from 1.1.9 and earlier is included: a database that can be read but
not written is repaired at start-up, a healthy database is never set aside, a
damaged data page is set aside, and a mis-packaged build without its licence key
refuses to start.

## What's new in 1.1.9

- **Fixed: creating your clinic or signing in on a phone could fail for good.**
  After a force-stop, the app could still open its database for reads but reject
  every write. Boot, health checks and the login screen all looked fine, and then
  the owner's first real action — creating the clinic, opening the dashboard, a
  sale — failed with the generic **"Something went wrong. Please try again."**
  The cause was debris a force-stop leaves beside the database: a
  `<db>-journal` / `<db>-wal` / `<db>-shm` path that is a **directory** rather
  than a file, or a stray `-wal` this rollback-journal build never writes. SQLite
  cannot replace a directory, so every write failed. The desktop build usually
  escaped it because it is quit cleanly, which is why the same code looked fixed
  on PC but kept failing on the phone. The app now probes a real write at
  start-up; if the write is blocked it clears the sidecar debris and retries
  once, and it fails loudly when the cause is something else (a read-only folder,
  a full disk) instead of booting into an error. This rebuild carries the fix to
  **both** the phone and the PC builds.

## What's new in 1.1.8

- **Fixed: a healthy database could be set aside.** 1.1.7 compared the file's
  real size against the size its header describes, and set the file aside when
  the two disagreed. But a database *longer* than its header describes is
  perfectly normal and healthy — SQLite simply ignores the extra bytes — so a
  shop that had such a file saw its data quarantined on start-up. The check now
  treats only a file that is **shorter** than its header describes as damage; a
  longer file is left exactly where it is. Your data stays put.
- **Fixed: a production offline build could run without its licence key.** A
  phone or desktop build packaged without the vendor public key used to fall back
  to a throw-away in-memory key, which silently switched licence checking off.
  Such a build now refuses to start, so a mis-packaged installer fails at the
  factory instead of running unlicensed in the field.

Everything from 1.1.7 is included:

- **Fixed: "Something went wrong" when creating your clinic or signing in, after
  a force-stop.** A force-stop can leave the file a different length from what
  its header describes — the last page written only partly, or a page from an
  interrupted commit appended after the last durable one. The file could still
  pass the page check and open normally, so the fault only appeared later, on the
  first real action (registration, the dashboard, a sale), as the same generic
  **"Something went wrong. Please try again."** with no way past it. The app now
  also compares the file size against the header's page count times the page size
  on start-up. If they disagree it sets the file aside as
  `clinicsync.db.corrupt-<timestamp>` (kept, never deleted) and builds a fresh
  one, so you can create your clinic and get in. This rebuild carries the fix to
  **both** the phone and the PC builds.

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
