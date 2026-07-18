#  Filters & I/O Redirection

> **Repository:** DevOps Linux Notes — Section 4
>
> Filters let you search and transform text; redirection and piping let you control where input comes from and output goes — the backbone of Linux scripting and log analysis.

---

##  grep

`grep` searches for a text pattern inside a file (or any text input).

The `/etc/passwd` file stores information about all users on the system — a common target for `grep` practice.

```bash
abdullah@DevOps:~/linux-practices$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
...
```

**Find lines containing "root":**

```bash
abdullah@DevOps:~/linux-practices$ grep root /etc/passwd
root:x:0:0:root:/root:/bin/bash
```

**Linux is case-sensitive** — `Root` and `root` are different. Ignore case with `-i`:

```bash
abdullah@DevOps:~/linux-practices$ grep Root /etc/passwd     # no match
abdullah@DevOps:~/linux-practices$ grep -i Root /etc/passwd
root:x:0:0:root:/root:/bin/bash
```

**Invert the match** — show everything *except* the given word — with `-v`:

```bash
grep -v root /etc/passwd
```

| Flag | Meaning |
|---|---|
| `-i` | Ignore case |
| `-v` | Invert match (exclude matching lines) |
| `-r` | Search recursively through a directory |
| `-n` | Show line numbers of matches |

---

##  Filter Commands

### `less` — page through a file

```bash
less /etc/passwd
```

| Key | Action |
|---|---|
| `Enter` | Scroll down line by line |
| `d` | Next page |
| `b` | Previous page |
| `/word` | Search for a word in the file |
| `v` | Open in `vi` mode to edit — saving returns you to `less` |

### `more` — same idea as `less`

```bash
more /etc/passwd
```

Same key bindings as `less` (`Enter`, `d`, `/`, `v`).

### `head` — first 10 lines of a file

```bash
[root@ktlinux ~]# head /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
...
```

### `tail` — last 10 lines of a file

```bash
[root@ktlinux ~]# tail /etc/passwd
apache:x:48:48:Apache:/var/www:/sbin/nologin
...
ktuser:x:501:501::/home/ktuser:/bin/bash
```

> 💡 `tail -f logfile` is one of the most-used DevOps commands — it "follows" a log file live as new lines are appended.

---

##  cut — extract fields from text

```bash
# cut -d <delimiter> -f <field> filename
[root@ktlinux ~]# cut -d: -f1 /etc/passwd
root
bin
daemon
adm
lp
sync
shutdown
halt
mail
uucp
```

`-d` sets the delimiter (`:`, `,`, space, etc.), `-f` picks which field to print.

```bash
# To delimit on spaces and print the first field
cut -d " " -f1 filename
```

---

##  sed — stream editor (search & replace)

`sed` searches for a word in a file and replaces it in the **output** — it does **not** modify the original file unless told to.

```bash
# sed 's/searchfor/replacewith/g' filename

[root@ktlinux ~]# cat ktfile
Welcome to Kernel Tech
[root@ktlinux ~]# sed 's/Tech/Technologies/g' ktfile
Welcome to Kernel Technologies
[root@ktlinux ~]# cat ktfile
Welcome to Kernel Tech
```

Note the original file is unchanged after `sed` — the replaced output only appears on screen unless redirected (see below) or run with `-i` to edit in place.

---

##  I/O Redirection

Redirection copies the **output** of a command into a file instead of printing it to the screen.

```bash
abdullah@DevOps:~/linux-practices$ cat devopstools
chef tech
ansible tech
git tech
docker tech
aws tech
```

**Search & replace, then redirect output to a new file with `>`:**

```bash
abdullah@DevOps:~/linux-practices$ sed 's/tech/tools/g' devopstools > newtools.txt
abdullah@DevOps:~/linux-practices$ cat newtools.txt
chef tools
ansible tools
git tools
docker tools
aws tools
```

> ⚠️ **Note:** If the target file doesn't exist, `>` creates it. If it already exists, `>` **overwrites** its entire contents.

**Append output to the same file with `>>`** (doesn't overwrite — adds to the end):

```bash
abdullah@DevOps:~/linux-practices$ tail /etc/passwd >> newtools.txt
```

**Redirect only errors to a file with `2>`:**

```bash
[root@localhost ~]# uptimer 2>> /tmp/error.log
```

**Redirect all output (stdout + stderr) to a file with `&>`:**

```bash
[root@localhost ~]# uptimer &>> /tmp/error.log
[root@localhost ~]# uptime &>> /tmp/error.log
```

| Operator | Meaning |
|---|---|
| `>` | Redirect stdout, overwrite file |
| `>>` | Redirect stdout, append to file |
| `2>` / `2>>` | Redirect stderr only (overwrite / append) |
| `&>` / `&>>` | Redirect stdout + stderr together (overwrite / append) |

---

##  Piping

Piping (`|`) feeds the **output of the command on the left** as **input to the command on the right** — chaining programs together instead of writing to intermediate files.

```bash
abdullah@DevOps:~/linux-practices$ ls | head -3
chefdk_1.2.22-1_amd64.deb
devopstools
file2

abdullah@DevOps:~/linux-practices$ ls | grep logdir
logdir

abdullah@DevOps:~/linux-practices$ cat /etc/passwd | grep root
root:x:0:0:root:/root:/bin/bash
```

---

##  find

`find` locates files or directories by name, type, owner, group, and more — similar to Windows Search.

```bash
abdullah@DevOps:~/linux-practices$ find /home/abdullah/ -name newtools.txt
/home/abdullah/linux-practices/newtools.txt
```

### Options for `find`

| Option | Usage |
|---|---|
| `-name` | Search by filename |
| `-inum` | Search by a particular inode number |
| `-type` | Search by file type (`f` = file, `d` = directory, `l` = link) |
| `-user` | Files owned by a particular user |
| `-group` | Files belonging to a particular group |

---

##  Quick Reference

| Command | Purpose |
|---|---|
| `grep pattern file` | Search for a pattern in a file |
| `grep -i` | Case-insensitive search |
| `grep -v` | Show non-matching lines |
| `less` / `more` | Page through a file |
| `head` | First 10 lines |
| `tail` | Last 10 lines |
| `tail -f` | Live-follow a growing file (logs) |
| `cut -d: -f1` | Extract a field by delimiter |
| `sed 's/old/new/g'` | Search & replace text |
| `>` | Redirect output, overwrite |
| `>>` | Redirect output, append |
| `2>>` | Redirect errors only, append |
| `&>>` | Redirect all output, append |
| `\|` | Pipe output of one command into another |
| `find /path -name` | Search for files by name |

---

##  Key Takeaways

- `grep` is the workhorse for searching text — combine with `-i` and `-v` for flexible matching.
- `head`/`tail` give you quick peeks at big files; `tail -f` is essential for live log monitoring.
- `cut` pulls specific fields out of structured text (like `/etc/passwd`); `sed` does search-and-replace on output.
- Redirection (`>`, `>>`, `2>`, `&>`) controls where a command's output and errors go — critical for scripting and logging.
- Piping (`|`) chains commands together, letting you build powerful one-liners without temp files.
- `find` searches the filesystem itself, not file contents — pair it with `grep` for full-text + filename searches.

---

##  Topics Covered in This Repository

- [x] Linux Introduction
- [x] Basic Commands
- [x] Vim Editor
- [x] Filters & I/O Redirection
- [ ] Users & Groups
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
