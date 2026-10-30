# ClinicSync downloads

Offline-first pharmacy, clinic and drug-shop management.
Source code is private; this repo only holds the installers.

## ⬇️ Download here

**➡️ https://github.com/Mubogi/clinicsync-downloads/releases/latest**

| Your device | File to download |
| --- | --- |
| Android phone / tablet | `ClinicSync-1.1.1.apk` |
| Windows PC | `ClinicSync-Setup-1.1.1.exe` |
| Linux PC (portable) | `ClinicSync-1.1.1.AppImage` |
| Linux PC (installer) | `clinicsync_1.1.1_amd64.deb` |
| Check an activation key | `activation.html` (opens offline in any browser) |

Activation keys are issued by JD Hub. The old in-browser key generator is no
longer distributed: it was a vendor tool and had no place in a customer's
download folder.

## Install notes

**Android.** Tap the `.apk`, then allow "Install unknown apps" for your browser
or file manager if Android asks. If you see "Error parsing package", you
downloaded the wrong file — use the release link above, not the source repo.

**Windows.** Run the `.exe` installer.

**Linux.** AppImage: `chmod +x ClinicSync-1.1.1.AppImage` then run it.
Debian/Ubuntu: `sudo apt install ./clinicsync_1.1.1_amd64.deb`.

## Upgrading from 1.1.0

Install straight over 1.1.0 — same signing key, so your data and settings are
kept. 1.1.1 fixes the phone-as-server first-run dead end: a fresh Android
Server no longer jumps to the activation screen asking for an owner sign-in
that cannot exist yet. It now creates the owner account first, then activates.
It also makes a Server run fully standalone with Wi-Fi off, with periodic sync
deferred until there is a network.

