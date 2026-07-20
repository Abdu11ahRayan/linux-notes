#  File Permissions

> **Repository:** DevOps Linux Notes — Section 6
>
> Permissions decide who can read, write, or execute a file — the foundation of Linux security and multi-user access control.

---

##  Viewing Permissions — `ls -l`

```bash
$ ls -l /bin/login
-rwxr-xr-x 1 root root 19080 Apr 1 18:26 /bin/login
```

Four symbols are used when displaying permissions:

| Symbol | Meaning |
|---|---|
| `r` | Permission to read a file, or list a directory's contents |
| `w` | Permission to write to a file, or create/remove files in a directory |
| `x` | Permission to execute a program, or `cd` into a directory and list it |
| `-` | No permission (in place of `r`, `w`, or `x`) |

The permission string breaks down into **3 groups of 3**:

```
-  rwx  r-x  r-x
   |    |    |
 owner group other
```

---

##  Changing File Ownership — `chown` / `chgrp`

- Only **root** can change a file's owner.
- Only **root or the current owner** can change a file's group.

```bash
chown [-R] user_name file|directory ...
chgrp [-R] group_name file|directory ...
```

```bash
abdullah@DevOps:~/linux-practices$ sudo adduser sam
...
abdullah@DevOps:~/linux-practices$ ls -l devopstools
-rw-rw-r-- 1 abdullah abdullah 53 Apr 2 19:09 devopstools

abdullah@DevOps:~/linux-practices$ chown sam.sam devopstools
chown: changing ownership of 'devopstools': Operation not permitted

abdullah@DevOps:~/linux-practices$ sudo chown sam.sam devopstools
abdullah@DevOps:~/linux-practices$ ls -l devopstools
-rw-rw-r-- 1 sam sam 53 Apr 2 19:09 devopstools
```

> ⚠️ Regular users **cannot** `chown` a file to another user without `sudo` — only root can hand ownership away.

**Recursive ownership change on a directory:**

```bash
abdullah@DevOps:~/linux-practices$ chown sam.sam vpdir/ -R
chown: changing ownership of 'vpdir/devopsdir/ansible': Operation not permitted
chown: changing ownership of 'vpdir/devopsdir/aws': Operation not permitted
chown: changing ownership of 'vpdir/devopsdir': Operation not permitted
```
(Again — needs `sudo` to succeed for files you don't own.)

---

##  Changing Permissions — Symbolic Method

```bash
chmod [-OPTION]... mode[,mode] file|directory ...
```

`mode` is made of:

- **who**: `u` (user/owner), `g` (group), `o` (others), `a` (all)
- **operator**: `+` (grant), `-` (deny), `=` (set exactly)
- **permission**: `r`, `w`, `x`

| Option | Meaning |
|---|---|
| `-R` | Recursive |
| `-v` | Verbose |
| `--reference` | Copy mode from another file |

**Examples:**

```bash
chmod ugo+r file      # Grant read access to everyone for `file`
chmod o-wx dir         # Deny write and execute to others for `dir`
```

---

##  Changing Permissions — Numeric Method

Uses a three-digit mode number:

- 1st digit → **owner** permissions
- 2nd digit → **group** permissions
- 3rd digit → **others** permissions

Each digit is a sum of:

| Value | Permission |
|---|---|
| `4` | read |
| `2` | write |
| `1` | execute |

```bash
chmod 640 myfile      # owner: rw-, group: r--, others: ---
```

**Walkthrough:**

```bash
abdullah@DevOps:~/linux-practices$ ls -l
-rw-rw-r-- 1 sam       sam       53 Apr 2 19:09 devopstools
-rw-rw-r-- 1 abdullah  abdullah   0 Apr 2 18:00 file2
lrwxrwxrwx 1 abdullah  abdullah   9 Apr 2 18:41 logdir -> /var/log/
-rw-rw-r-- 1 abdullah  abdullah 612 Apr 2 19:14 newtools.txt
drwxrwxr-x 4 sam       sam     4096 Apr 2 18:21 vpdir

abdullah@DevOps:~/linux-practices$ chmod u+x newtools.txt
abdullah@DevOps:~/linux-practices$ ls -l newtools.txt
-rwxrw-r-- 1 abdullah abdullah 612 Apr 2 19:14 newtools.txt

abdullah@DevOps:~/linux-practices$ chmod o-r newtools.txt
abdullah@DevOps:~/linux-practices$ ls -l newtools.txt
-rwxrw---- 1 abdullah abdullah 612 Apr 2 19:14 newtools.txt

abdullah@DevOps:~/linux-practices$ chmod 700 newtools.txt
abdullah@DevOps:~/linux-practices$ ls -l newtools.txt
-rwx------ 1 abdullah abdullah 612 Apr 2 19:14 newtools.txt

abdullah@DevOps:~/linux-practices$ chmod 755 newtools.txt
abdullah@DevOps:~/linux-practices$ ls -l newtools.txt
-rwxr-xr-x 1 abdullah abdullah 612 Apr 2 19:14 newtools.txt
```

---

##  Common Numeric Modes Cheat Sheet

| Mode | Meaning | Typical Use |
|---|---|---|
| `755` | rwxr-xr-x | Scripts, executables |
| `644` | rw-r--r-- | Regular files, configs |
| `700` | rwx------ | Private scripts/keys, only owner can touch |
| `600` | rw------- | Private files (e.g. SSH private keys) |
| `777` | rwxrwxrwx | Full access to everyone — avoid unless truly needed |

---

## 🧾 Quick Reference

| Command | Purpose |
|---|---|
| `ls -l` | View permissions |
| `chown user file` | Change owner |
| `chown user.group file` | Change owner + group |
| `chown -R user dir` | Change owner recursively |
| `chgrp group file` | Change group |
| `chmod u+x file` | Add execute for owner |
| `chmod o-r file` | Remove read for others |
| `chmod 755 file` | Set permissions numerically |

---

##  Key Takeaways

- `ls -l` shows permissions as 3 sets of `rwx` — owner, group, other.
- Only root can change a file's owner; root or the owner can change its group.
- `chmod` supports two styles: **symbolic** (`u+x`, `o-r`) and **numeric** (`755`, `644`) — numeric is faster once you know the read/write/execute = 4/2/1 math.
- `755` for executables/scripts and `644` for regular files are the most common defaults; `600`/`700` lock things down to the owner only.
- Recursive changes (`-R`) apply to every file/subdirectory — use with care, and remember `sudo` is needed for files you don't own.

---

##  Topics Covered in This Repository

- [x] Linux Introduction
- [x] Basic Commands
- [x] Vim Editor
- [x] Filters & I/O Redirection
- [x] Users & Groups
- [x] File Permissions
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
