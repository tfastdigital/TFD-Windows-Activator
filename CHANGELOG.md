# Changelog

All notable changes to **TFD Windows Activator** are documented here.
This project follows [Semantic Versioning](https://semver.org/) (`MAJOR.MINOR.PATCH`).

---

## [2.2.1] — 2026-10-08

### Changed
- Publisher and company metadata is now **TFAST Digital Agency** (application
  properties, branding and terms).

---

## [2.2.0] — 2026-10-08

### Security
- **Hardened release pipeline**: the assembly is **obfuscated** (string
  encryption, Obfuscar) before the single-file exe is bundled.
- **SHA-256 published** for each release; the updater verifies the download
  against GitHub's published digest and refuses to install on mismatch.
- Updates are accepted over **HTTPS only**; no debug symbols are shipped.
- Added [SECURITY.md](SECURITY.md) and [OBFUSCATION.md](OBFUSCATION.md).
- Removed the earlier, un-hardened releases.

### Added
- **Sound effects** on success and failure, with a **Sound** on/off toggle in the footer.
- **Toast notifications** that slide in for success (green) and failure (red).
- **Join Us popup** shown when activation succeeds, with Website, Telegram and
  WhatsApp links, plus a **Join Us** button in the footer.
- **Activation tools**: Repair Activation, License Details, Clear Notices.
- **System & branding**: Keep On This PC (install + shortcuts for re-activation),
  TFD Branding (shows TFAST Digital Agency in this PC's activation info),
  Activation Record (who activated this PC and when).
- **Terms & Conditions** in the app and in [TERMS.md](TERMS.md).
- README now includes the app logo and real screenshots of the tool.

### Fixed
- Taskbar / title-bar icon now uses the branded application icon.

---

## [2.1.1] — 2026-10-08

### Fixed
- Window title now shows the correct version (was stuck on v2.0).

### Documentation
- Added the app logo and real screenshots of the tool to the README.

---

## [2.1.0] — 2026-10-08

### Added
- **Check for Updates** — checks the latest release on GitHub and downloads and
  installs the newest build automatically, then restarts.
- **Help & Usage guide** covering the correct steps for Windows 8, 8.1, 10 and 11.
- Version number displayed in the header.

### Changed
- Buttons renamed to clear, professional actions (no internal terminology).
- Log messages rewritten to be user-facing and consistent.
- Window is fully responsive: reflows and fits small screens and laptops.
- Project version aligned across assembly, file and application metadata.

### Fixed
- Button descriptions no longer clip on narrow windows.
- System info panel wraps instead of overflowing.

---

## [2.0.0] — 2026-10-08

### Added
- Complete desktop (WPF) interface to replace the earlier console version.
- System detection: version, edition, build, architecture, activation state.
- Activation verification with a clear verdict.
- Restore-point creation and product-key backup.
- Pro edition upgrade flow with a guided all-in-one mode.
- Five activation profiles with per-version recommendations.
- Branded dark theme with icons and a lightweight, dependency-free build.

---

[2.2.1]: #221--2026-10-08
[2.2.0]: #220--2026-10-08
[2.1.1]: #211--2026-10-08
[2.1.0]: #210--2026-10-08
[2.0.0]: #200--2026-10-08
