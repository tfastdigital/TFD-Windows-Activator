# Changelog

All notable changes to **TFD Windows Activator** are documented here.
This project follows [Semantic Versioning](https://semver.org/) (`MAJOR.MINOR.PATCH`).

---

## [2.2.8] — 2026-10-08

### Fixed
- **No console window appears any more.** Console and PowerShell windows used by
  the tool now always run hidden, including the activation step.
- Activation is now applied automatically - no menu has to be answered.
- Restore-point creation used the wrong command; it is now correct.

### Added
- A "Checking This PC" report on startup that confirms everything the tool needs
  is already part of Windows, so **nothing has to be installed**.

---

## [2.2.7] — 2026-10-08

### Added
- **YouTube** and **TikTok** links in the footer, the success popup and the guide.

---

## [2.2.6] — 2026-10-08

### Fixed
- The GitHub link shown in the app now points to the correct project page.

---

## [2.2.5] — 2026-10-08

### Changed
- Internal reliability and quality improvements.
- General maintenance of how the tool stores its configuration values.

---

## [2.2.4] — 2026-10-08

### Changed
- Renamed to **One Click Free Activation**.
- Added **Past Updates** (version history) and a **GitHub** link inside the app.

---

## [2.2.3] — 2026-10-08

### Changed
- Action panel reorganised into clearer groups (Get Started, Safety First,
  Upgrade to Pro, Activate Windows, Tools, Help & Support).
- Presentation artwork added for the project page.

---

## [2.2.2] — 2026-10-08

### Added
- **Single-instance guard**: only one copy of the tool can run at a time;
  launching it again brings the existing window to the front.
- **Global error handling**: unexpected errors are logged to `error.log` and
  shown with a clear message instead of closing silently.
- **Diagnostics & feedback**: Diagnostics, Copy Log, Save Log and Open Log
  Folder actions for technical support.

### Improved
- Command runner now enforces a **timeout**, reports **exit codes**, and
  distinguishes missing executables and timeouts from real failures.
- Timings shown for commands that take longer than a few seconds.

---

## [2.2.1] — 2026-10-08

### Changed
- General maintenance and internal improvements.

---

## [2.2.0] — 2026-10-08

### Packaging
- Improved release packaging and download integrity checks.
- Removed the earlier superseded releases.

### Added
- **Sound effects** on success and failure, with a **Sound** on/off toggle in the footer.
- **Toast notifications** that slide in for success (green) and failure (red).
- **Join Us popup** shown when activation succeeds, with Website, Telegram and
  WhatsApp links, plus a **Join Us** button in the footer.
- **Activation tools**: Repair Activation, License Details, Clear Notices.
- **Keep On This PC** — installs the tool so you can re-activate later.
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

[2.2.8]: #228--2026-10-08
[2.2.7]: #227--2026-10-08
[2.2.6]: #226--2026-10-08
[2.2.5]: #225--2026-10-08
[2.2.4]: #224--2026-10-08
[2.2.3]: #223--2026-10-08
[2.2.2]: #222--2026-10-08
[2.2.1]: #221--2026-10-08
[2.2.0]: #220--2026-10-08
[2.1.1]: #211--2026-10-08
[2.1.0]: #210--2026-10-08
[2.0.0]: #200--2026-10-08
