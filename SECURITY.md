# Security

## How this project protects you

TFD Windows Activator is built to be safe to run and hard to tamper with.

### 1. Signed, verified releases
- Every release publishes a **SHA-256 hash**.
- The in-app updater verifies the downloaded file against the hash GitHub
  publishes for that asset and **refuses to install if it does not match**.
- Updates are only accepted over **HTTPS** — a non-HTTPS download is blocked.

### 2. Hardened binary
- The released executable is built from source with a self-contained runtime and
  **no debug symbols**.
- The application assembly is **obfuscated** (string encryption), so the released
  binary does not expose URLs, keys or service names in plain text.
  See [OBFUSCATION.md](OBFUSCATION.md) for the tool selection and test evidence.

### 3. No untrusted downloads
- The tool does not download or execute arbitrary code for its normal operation.
- The only network access is: Windows activation, and the update check against
  this repository's Releases page.
- "Keep On This PC" copies the **existing, running** executable to a permanent
  location — it never fetches anything.

### 4. Least privilege
- The tool requests administrator rights only because activation and the
  licensing service require them.
- It does not install services, drivers or background agents.

## Protecting yourself

| Do | Don't |
|---|---|
| Download **only** from the official Releases page. | Don't use re-uploaded copies from other sites. |
| Check the file's SHA-256 against the release hash. | Don't disable your antivirus to run it. |
| Keep a restore point before changing anything. | Don't run it on a PC you don't own. |

### Verifying a download (PowerShell)

```powershell
Get-FileHash .\TFDWindowsActivator.exe -Algorithm SHA256
```

Compare the result with the hash shown on the release page.

## Reporting a vulnerability

If you believe you have found a security issue, please report it through the
support channels listed in the README rather than opening a public issue.

## Scope and honesty

Obfuscation and hashing raise the cost of tampering; they do not make a .NET
binary impossible to reverse engineer. We do not claim otherwise.
