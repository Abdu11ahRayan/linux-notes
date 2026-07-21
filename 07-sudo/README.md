#  Sudo

> **Repository:** DevOps Linux Notes — Section 7
>
> `sudo` lets a normal user run commands with root privileges — the safer alternative to logging in as root directly.

---

##  What is Sudo?

`sudo` ("superuser do") gives a normal user the power to execute commands that are normally owned/restricted to the root user, without permanently switching to the root account.

---

##  Becoming Root — `sudo -i`

If a user already has full sudoers privilege, they can become root anytime with `sudo -i`.

```bash
abdullah@DevOps:~/linux-practices$ id
uid=1000(abdullah) gid=1000(abdullah) groups=1000(abdullah),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),113(lpadmin),128(sambashare),130(docker),1006(dev_dock_gr)

abdullah@DevOps:~/linux-practices$ sudo -i
[sudo] password for abdullah:
root@DevOps:~# id
uid=0(root) gid=0(root) groups=0(root)
```

> 💡 Note that `abdullah` is already in the `sudo` group above — that's what grants sudo privilege in the first place.

---

##  Adding a User to the Sudoers List — `visudo`

**Never edit `/etc/sudoers` directly** — always use `visudo`, which validates syntax before saving and prevents you from locking yourself out.

```bash
abdullah@DevOps:~/linux-practices$ sudo -i
root@DevOps:~# export EDITOR=vim
root@DevOps:~# visudo
```

Inside the file, under **User privilege specification**:

```
# User privilege specification
root    ALL=(ALL:ALL) ALL
sam     ALL=(ALL:ALL) ALL
```

This grants `sam` the same full root access as `root`.

**A group can also be added to the sudoers list:**

```
# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL
```

The `%` prefix indicates a group rather than a single user.

---

##  Skipping the Password Prompt — `NOPASSWD`

By default, `sudo` asks for **your own password** every time. To skip that prompt for a specific user:

```
# User privilege specification
root    ALL=(ALL:ALL) ALL
sam     ALL=(ALL:ALL) NOPASSWD: ALL
```

> ⚠️ `NOPASSWD` is convenient but weakens security — anyone with access to that account gets instant root with no password check. Use sparingly, mainly for automation/service accounts.

---

##  Switching Users — `su -`

```bash
abdullah@DevOps:~/linux-practices$ su - sam
Password:
sam@DevOps:~$
```

`su -` switches to another user's account (with their environment loaded) — you'll need that user's password unless you're already root.

**Become root from the `sam` login:**

```bash
sam@DevOps:~$ sudo -i
root@DevOps:~#
```

---

##  Quick Reference

| Command | Purpose |
|---|---|
| `sudo <command>` | Run a single command as root |
| `sudo -i` | Start an interactive root shell |
| `su - <user>` | Switch to another user's account |
| `visudo` | Safely edit `/etc/sudoers` |
| `ALL=(ALL:ALL) ALL` | Grants full root access in sudoers |
| `NOPASSWD: ALL` | Skips password prompt for sudo commands |
| `%groupname ALL=(ALL) ALL` | Grants sudo to an entire group |

---

##  Key Takeaways

- `sudo` grants temporary root privileges without logging in as root directly — safer and auditable (actions are logged per-user).
- Always edit sudoers permissions with `visudo`, never a plain text editor — it catches syntax errors before they lock you out.
- Users or whole groups (`%groupname`) can be granted sudo access.
- `NOPASSWD` removes the password prompt — useful for automation, but a real security tradeoff.
- `su - username` switches your full shell/environment to another user; `sudo -i` specifically elevates to root.

---

##  Topics Covered in This Repository

- [x] Linux Introduction
- [x] Basic Commands
- [x] Vim Editor
- [x] Filters & I/O Redirection
- [x] Users & Groups
- [x] File Permissions
- [x] Sudo
- [ ] Software Management
- [ ] Search
- [ ] Login (SSH & Telnet)
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
