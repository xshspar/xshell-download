# Xshell 8.0.0120 Download for Windows — SSH Client

Xshell is a Windows SSH client built around a session manager rather than a bare console. Sessions carry their own authentication, terminal type, log settings and startup script, and open in tabs that can be split or grouped. SFTP runs in a side panel, port forwarding is configured per session, and a scripting engine drives repeatable logins and command runs.

The distinction matters on a jump host estate: a session is a file, so a prepared session for a bastion — key, port, terminal type, log folder — can be handed to a colleague or dropped into a build image without retyping anything.

<p align="center">
  <a href="https://www.netsarang.com/en/xshell-download/">
    <img src="https://img.shields.io/badge/DOWNLOAD-Xshell-1B5E9B?style=for-the-badge&logo=windows&logoColor=white" alt="Download Xshell">
  </a>
</p>

| | |
|---|---|
| **Version** | 8.0.0120 |
| **Package** | installer from the download page |
| **Architecture** | x64 / x86 |
| **Platform** | Windows 10, Windows 11, Windows Server 2016+ |
| **License** | Free for home and school, paid for business |

## Download

| Package | Link |
|---|---|
| **Xshell** | [Download](https://www.netsarang.com/en/xshell-download/) |

The link opens the project's download page, where the current build sits at the top — no mirror sits in between.

## Works with

- Windows 11 (x64)
- Windows 10 22H2 and newer
- Windows Server 2016 / 2019 / 2022
- Free licence covers home and school use only

## SHA-256 checksum

The installer is code-signed, and the download page states the current build. After saving the file, hash it before you run it:

```powershell
Get-FileHash -Algorithm SHA256 <path-to-installer>
```

## Install

1. Download the setup from the download page and run it as administrator.
2. During install choose the free **Home and School** licence when prompted.
3. Create a session: protocol SSH, host, port 22, then pick password or public key authentication.
4. The installer accepts `/S` for a silent run; keep the licence file next to it for scripted installs.
5. Sessions are stored as files under the user profile. Export the folder before reinstalling Windows — the uninstaller removes the program, not the session store, but a wiped profile takes both.

## What it does

- SSH2 with key, keyboard-interactive and agent authentication
- Tabbed sessions with split panes and a folder-based session manager
- SFTP panel with a local/remote two-pane transfer view
- Local, remote and dynamic port forwarding per session
- Scripting for login sequences and batch command execution
- Session logging with timestamps, per session or for all tabs
- Terminal types from VT100 to xterm-256color, with per-session encoding

## Compatibility

Xshell speaks SSH2. Beyond SSH it handles telnet, rlogin and raw COM-port connections, so a console cable and a switch on the same desk do not need two programs. Authentication supports passwords, public keys, keyboard-interactive and agent forwarding, and the key manager imports existing keys as well as generating new ones with an optional passphrase.

Port forwarding is configured per session rather than globally, which is convenient until you need the same tunnel from three sessions. Local forwarding exposes a remote service on a local port, remote forwarding does the reverse, and dynamic forwarding opens a SOCKS proxy that any local application can use. The tunnel lives and dies with the session, so a dropped connection closes the listener.

Terminal behaviour is where most of the tuning happens. The session records its terminal type, its character encoding and its backspace handling; a session set to UTF-8 against a host that sends GB2312 shows readable ASCII and mangled everything else. The same applies to line endings and to the terminal size reported to the remote shell, which full-screen tools read at startup.

The licence split is by use, not by feature: home and school use is free, business use needs a paid licence per user. The build itself is the same binary, so an evaluation install behaves exactly like a licensed one until the trial expires.

## Troubleshooting

**"Connection refused" on port 22.** The SSH service is not listening, or a firewall between the client and host drops the packet. Test with `Test-NetConnection -Port 22` before changing client settings; Xshell reports the same message for both causes.

**"The host key has changed" warning.** The server was reinstalled or its key was regenerated. Compare the fingerprint through an out-of-band channel before accepting, then update the stored key for that session.

**Authentication succeeds but the session closes immediately.** The account's shell is invalid, the home directory is missing, or the server enforces a command restriction that exits at once. The server-side log names the reason; the client only shows a closed connection.

**Keyboard-interactive prompts never appear.** The session is set to password authentication only. Switch the method to keyboard-interactive, which is what many hardened servers require for one-time codes.

**Garbage characters in the terminal.** Encoding mismatch between session and host, or a locale that does not match the terminal type. Set both explicitly rather than relying on the default, which follows the Windows code page.

## Alternatives

PuTTY is the smallest option and still the reference implementation for raw SSH on Windows. MobaXterm adds an X server and a local shell alongside SSH. SecureCRT is the closest commercial equivalent, with a similar session model and its own scripting language. Termius syncs sessions across devices through an account. The OpenSSH client built into Windows covers scripting and config files without any installation at all.

## FAQ

**Is Xshell free?** — Free for home and school use; a business seat is paid.

**Does it run on Windows 11?** — Yes. One installer covers 10 and 11, and the server editions are supported from that same build.

**Can it be installed silently?** — Not with a documented switch; the licence page is interactive. Fleet installs need a packaging tool.

**Does it support SFTP and SCP?** — SFTP runs in the side panel of an SSH session. SCP is not a separate protocol here; file transfer goes through SFTP or through ZMODEM on a COM port.

**Can it run a script on connect?** — Yes. A session can carry a login script with expect-style waits, which is how repeated logins to appliances with menu-driven shells get automated.

**Does it store passwords?** — Only if asked to. Passwords saved in a session are protected by the master password, and without one they are stored in a reversible form.

## Disclaimer

This page collects the installer link, version data and SHA-256 checksum for offline installation and archival. Product names and trademarks belong to their respective owners. No affiliation or endorsement is implied.
