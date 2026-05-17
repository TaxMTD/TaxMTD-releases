<div align="center">
  <a href="https://taxmtd.uk">
    <img src="https://taxmtd.uk/TaxMTD-LOGO-Full.png" alt="TaxMTD" width="320" />
  </a>

  <h3>Download TaxMTD</h3>

  <p>
    Making Tax Digital, on every device a UK business owner uses.<br/>
    Native, signed, and silently auto-updating.
  </p>

  <p>
    <a href="https://github.com/TaxMTD/TaxMTD-releases/releases/latest">
      <img alt="Latest release" src="https://img.shields.io/github/v/release/TaxMTD/TaxMTD-releases?display_name=tag&label=latest&color=22c55e" />
    </a>
    <a href="https://github.com/TaxMTD/TaxMTD-releases/releases/latest">
      <img alt="Downloads" src="https://img.shields.io/github/downloads/TaxMTD/TaxMTD-releases/total?color=22c55e&label=downloads" />
    </a>
    <img alt="Signed" src="https://img.shields.io/badge/signed-Apple%20Developer%20ID%20%2B%20Azure%20Code%20Signing-22c55e" />
    <img alt="HMRC" src="https://img.shields.io/badge/HMRC-recognised-22c55e" />
  </p>

  <p>
    <a href="https://taxmtd.uk/download"><strong>Auto-detect my OS →</strong></a>
    &nbsp;·&nbsp;
    <a href="https://taxmtd.uk"><strong>Open the web app</strong></a>
    &nbsp;·&nbsp;
    <a href="https://taxmtd.uk/docs"><strong>Docs</strong></a>
    &nbsp;·&nbsp;
    <a href="https://taxmtd.uk/contact"><strong>Support</strong></a>
  </p>

  <br/>

  <img src="https://api.taxmtd.uk/assets/5ab518c2-52f1-4060-aed2-9e9404bbcf42?width=1600&format=avif" alt="TaxMTD on every device" width="100%" />
</div>

---

## Pick your platform

| Platform                  | Download                                                                                          | Notes                                              |
| ------------------------- | ------------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| 🍎 **macOS** Apple Silicon | [Latest .dmg](https://github.com/TaxMTD/TaxMTD-releases/releases/latest)                          | M1 / M2 / M3 / M4 / M5. Signed with Apple Developer ID + notarised. |
| 🍎 **macOS** Intel        | [Latest .dmg](https://github.com/TaxMTD/TaxMTD-releases/releases/latest)                          | Pre-2020 Macs. Same features as Apple Silicon.     |
| 🪟 **Windows** 10 / 11    | [Latest .msi](https://github.com/TaxMTD/TaxMTD-releases/releases/latest)                          | Branded MSI, en-GB locale, Azure-signed. Recommended. |
| 🪟 **Windows** 10 / 11    | [Latest .exe (NSIS)](https://github.com/TaxMTD/TaxMTD-releases/releases/latest)                   | Single-file installer for users who prefer .exe.   |
| 📱 **iOS / iPadOS**       | [Notify me](https://taxmtd.uk/contact?topic=ios-launch)                                            | Coming soon to the App Store.                       |
| 🤖 **Android**            | [Notify me](https://taxmtd.uk/contact?topic=android-launch)                                        | Coming soon to Google Play.                         |
| 🐧 **Linux**              | [Open the web app](https://taxmtd.uk)                                                              | All TaxMTD features work fully in the browser too. |

> Not sure which one? **[taxmtd.uk/download](https://taxmtd.uk/download)** auto-detects your OS and serves the right installer.

---

## What ships in every release

Each version tag (e.g. `v1.0.1`) attaches the following assets:

```
TaxMTD_<v>_aarch64.dmg          macOS Apple Silicon installer
TaxMTD_<v>_aarch64.dmg.sig      Ed25519 signature for the updater
TaxMTD_<v>_x64.dmg              macOS Intel installer
TaxMTD_<v>_x64.dmg.sig          Ed25519 signature for the updater
TaxMTD_<v>_x64_en-GB.msi        Windows MSI (en-GB)
TaxMTD_<v>_x64_en-GB.msi.sig    Ed25519 signature for the updater
TaxMTD_<v>_x64-setup.exe        Windows NSIS installer
TaxMTD_<v>_x64-setup.exe.sig    Ed25519 signature for the updater
latest.json                     Tauri auto-updater manifest
```

The `.sig` files are public Ed25519 minisign signatures. Installed apps verify them against a public key baked in at build time before applying any update — a tampered binary is refused before it touches disk.

---

## Auto-update flow

Once installed, **TaxMTD updates itself**. On every launch the app asks our update endpoint whether a newer version is available. If yes, the app shows the release's changelog inline and offers **Install & restart** — one click and you're on the new version.

```
   App boots
       │
       ▼
   GET https://taxmtd.uk/api/desktop/update
       ?target=darwin|windows
       &arch=aarch64|x86_64
       &current_version=<running>
       │
       ▼
   ─ If a newer version exists:
       200 { version, notes, pub_date, url, signature }
       App shows the changelog, downloads the bundle,
       verifies the signature, swaps the binary, restarts.
   ─ Otherwise:
       204 No Content — no dialog, no interruption.
```

No GitHub login required. No CDN credentials in the app. Everything is HTTPS + minisign.

---

## Security & signing

- 🍎 **macOS** binaries are signed with **Apple Developer ID** (Team `6S87K97Y8M`, Cliqer Ltd) and **notarised** by Apple. Gatekeeper opens them with no warnings.
- 🪟 **Windows** binaries are signed with **Azure Code Signing** (publisher: Cliqer Ltd). SmartScreen will trust them as the cert's reputation builds. If you see "Unknown publisher" on a fresh install, that's a transient SmartScreen heuristic — the cert is valid; click **More info → Run anyway**.
- 🔄 **Update payloads** are verified with **Ed25519 minisign** against a public key baked into every installed app. The key cannot be replaced post-install.

---

## What's inside the app

This is the **same TaxMTD app** you use in the browser — just running natively. Same data, same account, same features. One log-in, every device.

- **Making Tax Digital** for Income Tax, VAT, and Corporation Tax
- **Self Assessment** auto-fill for SA100 / SA102 / SA103 / SA105 / SA106 / SA108
- **Universal Credit** calculator with monthly assessment-period support
- **Bank feeds** via Open Banking (Plaid), Wise, Revolut, Stripe, PayPal, and Amazon Seller
- **AI bookkeeping** — categorisation, receipt OCR, mileage tracking
- **Invoicing** — designer, recurring templates, credit notes, estimates
- **Reports** — P&L, balance sheet, cash flow, fixed assets, project profitability, custom builder
- **Companies House** integration — annual accounts + CT600 + iXBRL export

See [taxmtd.uk](https://taxmtd.uk) for the full feature list and [taxmtd.uk/docs](https://taxmtd.uk/docs) for guides.

---

## Source code

This repo only hosts **signed binaries**. The Tauri shell source lives in [`TaxMTD/UC-tauri`](https://github.com/TaxMTD/UC-tauri) (private). The web app is at [taxmtd.uk](https://taxmtd.uk).

---

<div align="center">

Built by [Cliqer Ltd](https://taxmtd.uk) in the UK.

<sub>Apple Developer ID • Azure Code Signing • HMRC-recognised MTD software</sub>

</div>
