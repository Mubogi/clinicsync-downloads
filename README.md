# ClinicSync downloads

Offline-first pharmacy, clinic and drug-shop management.
Source code is private; this repo only holds the installers.

## ⬇️ Download here

**➡️ https://github.com/Mubogi/clinicsync-downloads/releases/latest**

| Your device | File to download |
| --- | --- |
| Android phone / tablet | `ClinicSync-1.0.9.apk` |
| Windows PC | `ClinicSync-Setup-1.0.9.exe` |
| Linux PC (portable) | `ClinicSync-1.0.9.AppImage` |
| Linux PC (installer) | `clinicsync_1.0.9_amd64.deb` |
| Check an activation key | `activation.html` (opens offline in any browser) |

Activation keys are issued by JD Hub. The old in-browser key generator is no
longer distributed: it was a vendor tool and had no place in a customer's
download folder.

## Install notes

**Android.** Tap the `.apk`, then allow "Install unknown apps" for your browser
or file manager if Android asks. If you see "Error parsing package", you
downloaded the wrong file — use the release link above, not the source repo.

**Windows.** Run the `.exe` installer.

**Linux.** AppImage: `chmod +x ClinicSync-1.0.9.AppImage` then run it.
Debian/Ubuntu: `sudo apt install ./clinicsync_1.0.9_amd64.deb`.

## Server or Client

On first launch the app asks whether this machine is the **Server** (it keeps
the data and other devices connect to it) or a **Client** (it connects to the
Server). It remembers the choice.

- **On a phone:** pick **Server** to run everything on that one phone — no PC
  and no paid hosting. It shows an address like `http://192.168.1.5:41999`.
  On your other phones and PCs pick **Client**, then tap **Find servers on
  this Wi-Fi** and select this one — no need to type the address. They must be
  on the same Wi-Fi.
- **On a PC:** the Server shows an address like `http://192.168.1.5:5000`.
  Clients can tap **Find servers on this Wi-Fi** or type it in.

## Activation

First launch shows a **Device ID**. Pay to Airtel Money merchant/till **7216334**
(name: JD Hub), then WhatsApp the Device ID, plan and duration to
**+256 754 687 597**. You get back a device-bound activation key.

Licensing runs on trust: unactivated copies keep working, so please pay to keep
ClinicSync maintained and supported.

## Contact

WhatsApp **+256 754 687 597**