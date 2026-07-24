#  Login (SSH & Telnet)

> **Repository:** DevOps Linux Notes — Section 10
>
> How to remotely log into another Linux system — the single most-used skill in DevOps for managing servers.

---

##  SSH — Secure Shell

SSH is the secure way to connect to a remote host — all data (including your password) is encrypted in transit.

```bash
$ ssh user@host                    # Connect to host as user (secure data communication)
$ ssh -p port user@host            # Connect to host on a specific port
```

---

##  Telnet

```bash
$ telnet host                      # Connect to a system using the telnet port
```

> ⚠️ Telnet sends everything — including passwords — in **plain text**. It's largely obsolete for anything beyond legacy/internal testing; always prefer SSH for real servers.

---

##  Quick Reference

| Command | Purpose |
|---|---|
| `ssh user@host` | Securely connect to a remote host as `user` |
| `ssh -p <port> user@host` | Connect to a remote host on a non-default SSH port |
| `telnet host` | Connect to a host using telnet (unencrypted) |

---

##  Key Takeaways

- SSH encrypts the entire session — the standard for connecting to any real server.
- The default SSH port is `22`; use `-p` when a server listens on a custom port.
- Telnet is unencrypted and should be avoided for anything sensitive — it's mainly a legacy/debugging tool now.

---

##  Topics Covered in This Repository

- [x] Linux Introduction
- [x] Basic Commands
- [x] Vim Editor
- [x] Filters & I/O Redirection
- [x] Users & Groups
- [x] File Permissions
- [x] Sudo
- [x] Software Management
- [x] Search
- [x] Login (SSH & Telnet)
- [ ] File Transfer
- [ ] Disk Usage
- [ ] Directory Traverse
- [ ] Services
- [ ] Compression & Archiving
- [ ] Process Management
- [ ] System Info
- [ ] Hardware Info
- [ ] Statistics
- [ ] Bash Scripting

---

*Course: DecodingDevOps by Imran Teli (Udemy) | Status: ✅ Completed*
