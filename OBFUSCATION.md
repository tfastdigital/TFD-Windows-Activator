# Obfuscation & Protection — Tool Research and Selection

This document records the protection tooling that was researched for TFD Windows
Activator, what was actually integrated, and the evidence from testing.

**Project profile:** C# / WPF desktop app, `net8.0-windows`, Windows-only,
shipped as a single self-contained `.exe`.

---

## Constraints discovered first

These constraints decided which tools are even possible:

| Constraint | Impact |
|---|---|
| **WPF** uses BAML: XAML `x:Name` fields and event handlers are resolved **by name through reflection** at runtime. | Aggressive renaming breaks the app. Renaming must be limited; string protection is safe. |
| The UI has **no** public API surface, but it is heavily reflection-driven internally. | `KeepPublicApi` + no method/property/event renaming. |
| **Native AOT requires trimming** and forbids reflection/dynamic loading; the official docs list "requires trimming" as a limitation. **WPF is not trim/AOT compatible.** | Native AOT is **not possible** for this app. |
| The artifact is a **single-file self-contained exe**. | The assembly must be protected *before* bundling. |

---

## Comparison matrix

Score = weighted total (Runtime compatibility 25, Protection effectiveness 25,
Stability 20, Maintenance/security 15, Build automation 10, Performance 5).

| # | Tool | Repo | Latest verified | Maintenance | .NET support | Protections | Compatibility risk | Integration | Test result | Recommendation |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | **Obfuscar** | github.com/obfuscar/obfuscar | **v3.0.0-beta.22** | Active (commit ~3 weeks ago, MIT, 3.2k★) | **.NET 8–11** | Symbol renaming, **string hiding**, metadata | Low when renaming is limited (WPF) | **Yes — MSBuild/CLI, integrated** | **PASS** (see below) | ✅ **PRIMARY** |
| 2 | Neo-ConfuserEx | github.com/XenocodeRCE/neo-ConfuserEx | v1.0.0-rc2 | Active-ish (3 months, 872★) | **.NET Framework 2.0–4.7.2 only** | Control-flow, string, anti-tamper, anti-debug | **Incompatible with .NET 8** | No | Not tested (incompatible) | ❌ Rejected |
| 3 | ConfuserEx | github.com/yck1509/ConfuserEx | legacy | Unmaintained | .NET Framework only | Historical reference | Incompatible + abandoned | No | Not tested | ❌ Rejected |
| 4 | Babel Obfuscator | babelfor.net | current | Commercial, active | .NET 8 supported | Strong (control-flow, virtualization) | Low (vendor supports WPF) | Not used | N/A | 💰 Commercial fallback |
| 5 | Eazfuscator.NET | gapotchenko.com | current | Commercial, active | .NET 8 supported | Strong (string/control-flow, WPF-aware) | Low | Not used | N/A | 💰 Commercial fallback |
| 6 | .NET Native AOT | github.com/dotnet/runtime | .NET 8 | Official | .NET 8 | Native code, no IL | **WPF incompatible** | No | Not possible | ❌ Rejected |
| 7 | UPX | github.com/upx/upx | current | Active | Native only | Compression only (not obfuscation) | N/A for .NET | No | Not used | ❌ Rejected |
| 8 | Sigstore Cosign | github.com/sigstore/cosign | current | Active | Artifact signing | Release signing / verification | Low | Recommended (CI) | N/A here | ➕ Recommended |
| 9 | OWASP Dependency-Check | github.com/dependency-check/DependencyCheck | current | Active | Dependency CVE scan | Vulnerability report | Low | Recommended (CI) | N/A here | ➕ Recommended |
| 10 | CodeQL | github.com/github/codeql | current | Active | Static analysis | Vulnerability discovery | Low | Recommended (CI) | N/A here | ➕ Recommended |

**Selection:** **Obfuscar** is the primary solution (only open-source option that
supports .NET 8 **and** builds reproducibly from source).
**Fallback:** a commercial WPF-aware protector (Babel or Eazfuscator.NET).
Per the guidance, **only one obfuscator is applied** — transformations are never
stacked.

---

## What was integrated

`publish.ps1` now runs a hardened pipeline:

```
1. dotnet publish --self-contained -p:PublishSingleFile=false   → bin\Stage
2. obfuscate.ps1  (Obfuscar, HideStrings=true)                  → bin\StageObf
3. copy obfuscated TFDWindowsActivator.dll back into bin\Stage
4. dotnet publish -p:PublishSingleFile=true --no-build          → dist\v<x>\...exe
```

Settings (`Obfuscar.xml`) are deliberately conservative for WPF:

- **`HideStrings = true`** — the main protection. The URLs, KMS server, product
  keys and messages are encrypted in the binary.
- **`RenameTypes/Methods/Properties/Events/Fields = false`** — nothing WPF
  resolves by name is renamed, so the app cannot break.
- **`KeepPublicApi = true`** — the public surface is unchanged.

---

## Evidence (validation tests run)

| Test | Method | Result |
|---|---|---|
| Obfuscar runs on the WPF assembly | `obfuscate.ps1` on a self-contained publish | ✅ "Completed in 1.39 seconds", output DLL produced |
| Secret strings are hidden | ASCII scan of the DLL for `kms8.msguides.com` | ✅ **Not found** in the obfuscated DLL |
| App still starts and renders | Non-elevated obfuscated build launched, window measured | ✅ **1400×945** window rendered |
| Hardened single-file exe works | Full pipeline, bundled exe launched | ✅ **1400×945** window rendered |

Screenshots: `docs/images/screenshot-obfuscated.png` (obfuscated assembly) and
`docs/images/screenshot-hardened.png` (obfuscated single-file exe).

---

## Anti-tamper & integrity (release level)

- **SHA-256 published** for every release; the in-app updater verifies the
  downloaded file against GitHub's published digest and **refuses to install on
  mismatch**.
- Updates are only accepted over **HTTPS**.
- **No debug symbols** (`.pdb`) are shipped.
- **Recommended next step for releases:** sign the `.exe` with an Authenticode
  code-signing certificate and add Cosign release attestation in CI. This is the
  only way to give users cryptographic proof of publisher identity; the token
  holder for the repo does not have a signing certificate available here.

## Honest limitations

- Obfuscation **raises the bar**; it does not make a .NET binary unreadable.
  A determined analyst can still reverse engineer it.
- Because WPF forbids renaming the XAML-bound members, protection here is
  **string encryption first**, not heavy control-flow obfuscation.
- Native AOT (the strongest practical protection) is **impossible** with WPF.
