# ⚠️💾 NETWORK VIRUS IDENTIFIER PORTABLE

This project helps identify and detect malicious software on your machine. To contribute to the community, it was ported to an executable, making it more accessible to technicians and people with good computer knowledge to use in their daily work.

The monitor shows, in real time, which programs on your computer are communicating with the internet, to which IP, and from which folder the program is running.

> [README Portuguese Version](README.pt-BR.md)


---

# Terminal

<img width="1674" height="989" alt="Screenshot 2026-03-13 112215" src="https://github.com/user-attachments/assets/2c4cb8d1-4846-4bd9-bd26-267bac2842a1" />

---

# How to install?

1. Go to the **Releases** tab of this repository.
2. Download the **`NetworkVirusIdentifier.exe`** file.
3. Save it in any folder (or on a USB drive, since it is portable).
4. Double-click to open it and accept the administrator prompt (UAC).

That's it, the monitor starts showing connections right away.

> To close it, just close the window or press `Ctrl + C`.

---

# Requirements

- Windows 10 or higher (64-bit)
- **Administrator** permission

> The program uses `netstat` and PowerShell, which already come with Windows. A Linux version is planned for a future update.

---

# Understanding the screen

### `[ CONNECTIONS ESTABLISHED ]`

| Column | Meaning |
|---|---|
| `PROCESS` | Name of the program that opened the connection |
| `PID` | Process identifier in Windows |
| `REMOTE_IP` | Destination IP |
| `STATUS` | Connection state (`ESTABLISHED`) |
| `PATH` | Folder where the executable is saved |

### `[ LATEST DISCONNECTIONS ]`

History of connections that were closed (keeps the last 200), with the process, the IP and the time (`CLOSED_AT`).

### 🚩 Warning signs

When analyzing the list, watch out for:

- Programs running from unusual folders, such as `AppData\Local\Temp`, `Downloads` or `ProgramData`
- Names similar to Windows processes, but in the wrong location (for example, a `svchost.exe` outside `C:\Windows\System32`)
- Constant connections to unknown IPs
- Processes with `PATH` equal to `RESTRICTED ACCESS` (run as administrator to see the path)

> A suspicious connection does not necessarily mean there is a virus. Research the IP and the program before making any decision.

---

# Antivirus warning

Since it is an executable that calls PowerShell and `netstat`, Windows Defender and other antivirus software may flag it as a false positive. The source code is open and available in this repository, so you can review it or build your own executable (see below).

---

# How to build the executable (for developers)

The project uses **Node SEA** (Single Executable Applications) to package the code.

### Prerequisites

- [Node.js 20 or higher](https://nodejs.org)

### Step by step

```bash
# 1. Clone the repository
git clone https://github.com/Shazanxz/Network-Virus-Identifier-Portable.git
cd Network-Virus-Identifier-Portable

# 2. Install the dependencies
npm install

# 3. Build the executable
node run build
```

The result is saved at `build/NetworkVirusIdentifier.exe`.

### Running without building the executable

```bash
node index.js
```

### Project structure

```
Network-Virus-Identifier/
├── assets/
│   └── logo.ico        # executable icon
├── build/              # final executable (generated)
├── dist/               # intermediate files (generated)
├── index.js            # monitor code
├── build-sea.js        # script that builds the executable
├── sea-config.json     # Node SEA configuration
└── package.json
```

# Credits

- **devbluen** - Project creator
- **Shazanxz** - Executable port

If this project helped you, leave a ⭐ on the repository and keep the credits when redistributing.