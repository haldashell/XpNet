# HaldaShell - Operation Manual

**Version:** 2.2

---

## 1. Introduction

HaldaShell is a professional network connection tool for SSH, Telnet, Serial, and SFTP. It provides a tabbed terminal interface with encrypted credential storage, session logging, file transfer, port forwarding, syntax highlighting, and built-in network utilities.

**Key capabilities:**
- SSH, Telnet, and Serial terminal sessions
- SFTP file browser (upload/download files and folders)
- SSH port forwarding (tunnels)
- Ping, Traceroute, Wake-on-LAN
- Encrypted, device-bound connection storage
- Multi-tab sessions with color coding and close (X) button
- Session reconnect (right-click tab)
- Terminal syntax highlighting (MobaXterm-style)
- Bracketed paste mode with line-ending normalization
- Full-screen app support (vim, less, htop, man)
- Session logging (clean, ANSI-free)

---

## 2. Getting Started

### Launching
Double-click **HaldaShell.exe**. No installation required.

On first launch, HaldaShell creates:
- `.haldashell.key` — device identity file (do not delete or share)
- `HDSXXXXXXXXXX.dat` — your saved connections
- `logs/` — folder for session logs

### System Requirements
- Windows 10/11 (64-bit)
- No Python or dependencies needed (self-contained .exe)

---

## 3. Making a Connection

### New Connection (SSH / Telnet / Serial)
1. **File → New Connection**
2. Select **Type**: SSH, Telnet, or Serial
3. Fill in the fields:

**For SSH:**
   - **Host** — server IP or hostname
   - **Port** — SSH port (default 22)
   - **Username** — login name
   - **Password** — password (blank if using key)
   - **Key File** — browse for private key (optional)
   - **Terminal** — terminal type (default xterm-256color)

**For Telnet:**
   - **Host** — device IP or hostname
   - **Port** — Telnet port (default 23)

**For Serial:**
   - **COM Port** — dropdown showing available COM ports (auto-detected)
   - **Baud** — baud rate (default 9600)

4. Click **Connect** — session opens in a new colored tab
5. Or click **Save** — saves the connection for quick access later

### Quick Connect (Saved Connections)
1. Open **View → Toggle Connections Panel** (sidebar appears)
2. **Double-click** any saved connection to connect instantly

---

## 4. Tab Management

### Tab Bar
Each session opens as a colored tab at the top with:
- **Tab name** — click to switch to that session
- **✕ button** — click to disconnect and close the tab

### Right-Click Menu
Right-click any tab to see:
- **Reconnect** — reconnect a disconnected session (uses saved credentials)
- **Disconnect** — close the session

### Tab Colors
Each new session gets a random color for easy visual identification.

---

## 5. Terminal Usage

### Keyboard
Type directly into the terminal — all keystrokes are sent to the server.

| Key | Action |
|-----|--------|
| Ctrl+C | Interrupt (stop running command) |
| Ctrl+D | EOF / logout |
| Ctrl+Z | Suspend process |
| Ctrl+L | Clear screen |
| Ctrl+F | Find text in terminal |
| Tab | Autocomplete |
| Arrow keys | Navigate / command history |
| Esc | Escape (for vi/vim) |
| Ctrl+End | Snap to bottom (return to live prompt) |
| Shift+End | Snap to bottom (alternate) |

### Copy & Paste
- **Select text** with left-click + drag → automatically copied to clipboard
- **Right-click** → pastes clipboard into terminal
- **Ctrl + left-click + drag** → column/block selection

**Paste behavior (v2.2):**
- Line endings normalized: `\r\n` → `\r` (like PuTTY)
- Bracketed Paste Mode: pasted text wrapped in escape sequences so the shell knows it's pasted (like MobaXterm) — prevents accidental command execution

### Zoom
- **Ctrl + Mouse Wheel** — zoom in/out
- **Ctrl + Plus / Minus** — zoom in/out
- **Ctrl + 0** — reset zoom

### Scrolling
- **Mouse wheel** — scroll 5 lines per tick through history (up to 100,000 lines)
- **Ctrl+End** or **Shift+End** — instant jump back to live prompt
- **Any keypress** — auto-scrolls to bottom (you're typing at the prompt)

### Full-Screen Applications (vim, less, htop)
HaldaShell v2.2 properly supports full-screen terminal applications:
- **vim/vi** — works normally (insert, command, visual modes)
- **less/more** — page scrolling works
- **htop/top** — live updates render correctly
- **man pages** — display and navigation works

The terminal detects alternate screen mode automatically and adjusts rendering.

---

## 6. Syntax Highlighting

HaldaShell highlights keywords in the terminal output for quick visual scanning (similar to MobaXterm):

| Color | Keywords |
|-------|----------|
| **Red** | error, failed, denied, refused, timeout, unreachable, fatal, critical |
| **Orange** | warning, deprecated, missing, invalid, retry |
| **Green** | ok, success, pass, done, active, running, enabled, connected, loaded, complete, ready |
| **Blue** | info, note, notice, hint, debug |

- Toggle on/off: **View → Toggle Syntax Highlight**
- Highlighting is disabled during full-screen apps (vim, htop) to avoid interference
- Only visible lines are highlighted (no performance impact on large scrollback)

---

## 7. Managing Saved Connections

### Save a Connection
- In the New Connection dialog, click **Save**
- Enter a **Connection Name** and **Group**, then click **OK**

### Edit a Connection
1. **View → Toggle Connections Panel** to show the sidebar
2. Select a connection
3. **View → Edit Connection**
4. Modify fields, click **Save**

### Delete a Connection
1. Show the sidebar
2. Select a connection
3. Click the **Delete** button in the sidebar

### Connection Groups
Connections are organized into groups (folders) in the sidebar.
Assign a group name when saving. Default group is "Default".

---

## 8. SFTP File Transfer

1. Connect to an SSH server
2. **Tools → SFTP Browser**
3. In the SFTP window:
   - Navigate folders (double-click to enter, "Up" to go back)
   - **Upload Files** — select one or more files to upload
   - **Upload Folder** — upload an entire folder (recursive)
   - **Download** — select file(s), choose destination
   - **New Folder** — create a remote directory
   - **Delete** — remove selected file(s)/folder(s)
   - Multi-select with Ctrl+click or Shift+click

---

## 9. Port Forwarding (Tunnels)

1. Connect to an SSH server
2. **Tools → Port Forwarding**
3. Enter:
   - **Local Port** — port on your machine
   - **Remote Host** — target host (from the server's perspective)
   - **Remote Port** — target port
4. Click **Start** — traffic to localhost:localport is tunneled through SSH
5. Select a tunnel and click **Stop Selected** to close it

Example: Forward local 8080 to a remote web server's 80.

---

## 10. Network Tools

| Tool | Menu | Purpose |
|------|------|---------|
| Ping | Tools → Ping | Test connectivity to a host |
| Traceroute | Tools → Traceroute | Trace network path to a host |
| Wake-on-LAN | Tools → Wake-on-LAN | Wake a device by MAC address |

---

## 11. Security & Encryption

### Enabling Encryption
1. **File → Enable Encryption**
2. Set a **master password** (min 4 characters), confirm it
3. Optionally save a **recovery key** file (store it safely!)

After this, HaldaShell asks for your master password on every startup.
Your connection file becomes an encrypted binary — unreadable without the password.

### Device Binding
Encryption is tied to this specific installation via the `.haldashell.key` file.
Even with the correct password, the connection file **cannot** be decrypted on a
different machine without the `.haldashell.key` file.

### Recovery
- If you forget your master password, use the recovery key file to reset it.
- **If both password and recovery key are lost, connections cannot be recovered** —
  you'll need to re-add your servers.

### Disabling Encryption
- **File → Disable Encryption** — converts back to plain storage (requires current password)

---

## 12. Session Logging

Every session is automatically logged to the `logs/` folder next to HaldaShell.exe.

- Filename format: `user@host_YYYY-MM-DD_HH-MM-SS.log`
- Logs are cleaned of ANSI escape codes (human readable)
- Logs capture all terminal output including commands and responses

---

## 13. Themes

**View → Theme** — choose from:
- Corporate Blue (default)
- Green on Black
- White on Black
- Amber on Black
- Black on White
- Solarized Dark
- Dracula
- Monokai

---

## 14. Command Snippets

Save frequently-used commands for quick execution.

1. **View → Toggle Snippets** (panel appears at bottom)
2. **Add Snippet** — enter a name and command
3. **Double-click** a snippet to send it to the active session
4. **Delete** — remove a selected snippet

Example snippets:
- Disk Usage: `df -h`
- Memory: `free -m`
- Processes: `ps aux --sort=-%mem | head -20`

---

## 15. Importing from PuTTY

**File → Import from PuTTY** — imports saved PuTTY sessions from the Windows
registry (host, port, username, terminal type). Passwords are not imported
(PuTTY doesn't store them) — you'll need to re-enter them.

---

## 16. Files Created by HaldaShell

| File | Location | Purpose |
|------|----------|---------|
| `.haldashell.key` | Next to .exe | Device identity + encryption key |
| `HDSXXXXXXXXXX.dat` | Next to .exe | Saved connections (encrypted or plain) |
| `HDSXXXXXXXXXX.salt` | Next to .exe | Encryption salt (only if encrypted) |
| `logs/*.log` | logs/ folder | Session transcripts |
| `HaldaShell_recovery.key` | Wherever you save it | Password recovery |

**Backup recommendation:** Keep a safe copy of `.haldashell.key` and your
`.dat` file together. Without both, encrypted connections are unrecoverable.

---

## 17. Troubleshooting

| Problem | Solution |
|---------|----------|
| Connection fails | Check host/port/credentials |
| No prompt after login | Try a different Terminal type (vt100, linux) |
| Password auth rejected | Server may require key auth — provide a Key File |
| vim/vi doesn't work | Should work in v2.2. If issues persist, try terminal type "xterm" |
| Mouse selection disappears | Fixed in v2.2 — selection preserved during data arrival |
| Can't scroll back to prompt | Press any key or Ctrl+End to snap back |
| Serial port not showing | Install pyserial: `pip install pyserial` (Pro version only) |
| Forgot master password | Use the recovery key file (File menu) |
| App won't start | Ensure .haldashell.key isn't corrupted; delete it to reset (loses saved connections) |

---

## 18. Keyboard Shortcut Reference

| Shortcut | Action |
|----------|--------|
| Ctrl+C | SIGINT (interrupt) |
| Ctrl+D | EOF (logout) |
| Ctrl+Z | Suspend |
| Ctrl+L | Clear screen |
| Ctrl+A | Start of line |
| Ctrl+E | End of line |
| Ctrl+U | Kill line |
| Ctrl+W | Kill word |
| Ctrl+R | Reverse search |
| Ctrl+F | Find in terminal |
| Ctrl+End | Snap to bottom |
| Shift+End | Snap to bottom |
| Ctrl+Scroll | Zoom in/out |
| Ctrl+0 | Reset zoom |
| Right-click | Paste |
| Select+release | Copy |
| Ctrl+Click+drag | Column select |

---

## 19. Version History

| Version | Changes |
|---------|---------|
| 2.2 | Syntax highlighting, vim/less/htop support, bracketed paste mode, COM port auto-detect for Serial |
| 2.1 | Serial connection support, paste line-ending normalization |
| 2.0 | Tab close (X) button, right-click reconnect, unified New Connection dialog (SSH/Telnet/Serial), Telnet fix, mouse selection fix, scroll-back improvements |
| 1.0 | Initial release — SSH, Telnet, SFTP, tunnels, encryption, themes |

---

*HaldaShell
shellhalda@gmail.com
HaldaShell@outlook.com

*"Have fun with your Daily Connection"*
