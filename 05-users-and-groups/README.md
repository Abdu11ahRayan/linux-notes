#  Users & Groups

> **Repository:** DevOps Linux Notes — Section 5
>
> Every file, process, and resource on Linux is tied to a user and a group — understanding this is core to securing and managing servers.

---

##  Users — Key Points

- Users and groups control access to files and resources.
- Users log in by supplying a username and password.
- Every file on the system is owned by a user and associated with a group.
- Every process has an owner and group affiliation, and can only access resources its owner or group can access.
- Every user is assigned a unique **User ID (UID)**.
- Usernames and UIDs are stored in **`/etc/passwd`**.
- Passwords are stored in **`/etc/shadow`** in encrypted form.
- Users are assigned a home directory and a login shell (usually Bash).
- Users cannot read, write, or execute each other's files without permission.

---

##  Types of Users

| Type | Example | User ID (UID) | Group ID (GID) | Home Dir | Shell |
|---|---|---|---|---|---|
| **Root** | root | 0 | 0 | `/root` | `/bin/bash` |
| **Regular** | abdullah, vagrant | 1000–60000 | 1000–60000 | `/home/username` | `/bin/bash` |
| **Service** | ftp, ssh, apache | 1–999 | 1–999 | `/var/ftp` etc. | `/sbin/nologin` |

In Linux there are three types of users:

1. **Super user / root user** — the most powerful user; the system administrator.
2. **System user** — created automatically by software/applications (e.g. installing Apache creates a `apache` user).
3. **Normal user** — created by root for real people (e.g. Rahul, Musab). Only root can create or remove a user.

**Whenever a user is created, three things happen by default:**

- A home directory is created (`/home/username`).
- A mailbox is created (`/var/spool/mail`).
- A unique UID and GID are assigned.

---

##  The `/etc/passwd` File

```bash
[root@ktlinux ~]# head /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
```

Fields (colon-separated):

| Field | Example | Meaning |
|---|---|---|
| 1 | `root` | Username |
| 2 | `x` | Link to password file (`/etc/shadow`) |
| 3 | `0` | UID (User ID) |
| 4 | `0` | GID (Group ID) |
| 5 | `root` | Comment (brief info about the user) |
| 6 | `/root` | Home directory |
| 7 | `/bin/bash` | Login shell (or `/sbin/nologin`) |

---

##  The `/etc/group` File

Stores group information — one entry per line.

```
Group name : group password : GID : group members
```

```bash
[root@localhost ~]# head /etc/group
root:x:0:
bin:x:1:
daemon:x:2:
```

---

##  The `/etc/shadow` File

Stores users' encrypted passwords and password-aging info. Same one-line-per-entry format as `/etc/passwd`.

1. Username
2. Encrypted password
3. Days since password was last changed
4. Minimum days before password can be changed
5. Maximum days before password must be changed
6. Days before expiry to warn the user
7. Days to disable the account after password expiry
8. Days since the account has been disabled
9. Reserved field

```bash
[root@localhost ~]# cat /etc/shadow
root:$1$m.FEVNiS$OYiaRNHMHzS85/wnDHccI.::0
bin:*:18353:0:99999:7:::
daemon:*:18353:0:99999:7:::
```

---

##  Add User, Set Password & Switch User

```bash
[abdullah@localhost ~]$ sudo useradd sam
[abdullah@localhost ~]$ sudo passwd sam
Changing password for user sam.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
[abdullah@localhost ~]$ su - sam
Password:
[sam@localhost ~]$ pwd
/home/sam
[sam@localhost ~]$ id
uid=1002(sam) gid=1003(sam) groups=1003(sam)
```

---

##  Add User, Group & Add User Into Group

```bash
[root@localhost ~]# useradd devops
[root@localhost ~]# id devops
uid=1001(devops) gid=1001(devops) groups=1001(devops)

[root@localhost ~]# grep devops /etc/passwd
devops:x:1001:1001::/home/devops:/bin/bash

[root@localhost ~]# groupadd opsadmin
[root@localhost ~]# usermod -G opsadmin devops
[root@localhost ~]# grep opsadmin /etc/group
opsadmin:x:1002:devops

[root@localhost ~]# id devops
uid=1001(devops) gid=1001(devops) groups=1001(devops),1002(opsadmin)
```

> 💡 `usermod -G` **replaces** all of a user's secondary groups. Use `usermod -aG` to **append** a group without removing existing ones — a very common gotcha.

---

##  Delete User & Group

```bash
[abdullah@localhost ~]$ sudo userdel -r sam
[abdullah@localhost ~]$ sudo groupdel opsadmin
[abdullah@localhost ~]$ sudo id sam
id: sam: no such user
```

`userdel -r` removes the user **and** their home directory.

---

##  User & Group Cheatsheet

| Command | Description |
|---|---|
| `useradd` | Creates a user (RHEL/CentOS) |
| `adduser` | Creates a user (Ubuntu — interactive) |
| `id` | Shows user info (UID, GID, groups) |
| `groupadd` | Creates a group |
| `usermod -G grpname username` | Adds user to group (replaces secondary groups) |
| `usermod -aG grpname username` | Appends user to a group |
| `passwd` | Set/reset a password |
| `userdel -r` | Removes user along with home directory |
| `groupdel` | Removes a group |
| `last` | Shows last login history |
| `who` | Shows who is currently logged in |
| `whoami` | Shows your current username |
| `lsof -u user` | Lists files opened by a user |

---

##  Key Takeaways

- Every user has a UID, every group has a GID, and both are recorded in `/etc/passwd` and `/etc/group`.
- Passwords never live in `/etc/passwd` — they're encrypted in `/etc/shadow`.
- Root (UID 0) is all-powerful; service users (UID 1–999) run daemons; regular users (UID 1000+) are real people.
- `useradd`/`adduser` + `passwd` gets a user going; `usermod -aG` adds them to extra groups without wiping existing ones.
- `userdel -r` and `groupdel` clean up users/groups — the `-r` flag matters if you want the home directory gone too.

---

##  Topics Covered in This Repository

- [x] Linux Introduction
- [x] Basic Commands
- [x] Vim Editor
- [x] Filters & I/O Redirection
- [x] Users & Groups
- [ ] File Permissions
- [ ] Sudo
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
