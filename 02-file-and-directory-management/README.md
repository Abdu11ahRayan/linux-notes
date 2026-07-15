# 💻 Basic Commands

> **Repository:** DevOps Linux Notes — Section 2
>
> Core navigation and file-handling commands every DevOps engineer uses daily.

---

## 📌 Open Terminal

The terminal is where all the action happens. On Ubuntu: `Ctrl + Alt + T`, or search "Terminal" in the app menu.

---

## 📍 Know Where You Are — `pwd`

`pwd` (Print Working Directory) shows your current location in the filesystem.

```bash
abdullah@DevOps:~$ pwd
/home/abdullah
```

---

## 📁 Create a Directory — `mkdir`

```bash
abdullah@DevOps:~$ mkdir linux-practices
```

---

## 🚶 Change Directory — `cd`

```bash
abdullah@DevOps:~$ cd linux-practices/
abdullah@DevOps:~/linux-practices$
```

---

## 📃 List Files — `ls`

```bash
abdullah@DevOps:~/linux-practices$ mkdir vpdir
abdullah@DevOps:~/linux-practices$ mkdir testdir
abdullah@DevOps:~/linux-practices$ mkdir devopsdir
abdullah@DevOps:~/linux-practices$ ls
devopsdir  testdir  vpdir
```

### `ls` Command Options

| Option | Description |
|---|---|
| `-l` | Long listing format — one file/directory per line |
| `-a` | List all hidden files/directories (those starting with `.`) |
| `-F` | Adds a `/` at the end of each directory name |
| `-g` | List files with group name |
| `-i` | Print index (inode) number of each file |
| `-m` | List files separated by commas |
| `-n` | List numeric UID and GID of owner/group |
| `-r` | List in reverse order |
| `-R` | Recursively list all directories |
| `-t` | Sort by modified time, newest first |

---

## 📄 Create Empty Files — `touch`

```bash
abdullah@DevOps:~/linux-practices$ touch file2 file3 file4
abdullah@DevOps:~/linux-practices$ ls
devopsdir  file1  file2  file3  file4  testdir  vpdir
```

---

## 🧭 Absolute Path vs Relative Path

**What is a path?**
A unique location of a file or folder in the filesystem — a combination of `/` and alphanumeric characters.

**Absolute path** — the full path starting from the root directory `/`.

```
/home/abdullah/linux-practices/
/var/ftp/pub
/etc/samba.smb.conf
/boot/grub/grub.conf
```

**Relative path** — a path relative to your current working directory (`pwd`). If you're in `/home/abdullah` and want to reach `/home/abdullah/linux-practices`, you can just type `linux-practices` — no leading `/`.

```bash
abdullah@DevOps:~$ pwd
/home/abdullah
abdullah@DevOps:~$ cd linux-practices/
abdullah@DevOps:~/linux-practices$ cd devopsdir/
abdullah@DevOps:~/.../devopsdir$ pwd
/home/abdullah/linux-practices/devopsdir
```

> 💡 If the path starts with `/`, it's absolute. If it doesn't, it's relative to `pwd`.

**Creating directories with both path types:**

```bash
abdullah@DevOps:~/linux-practices$ mkdir devopsdir/ansible                              # relative
abdullah@DevOps:~/linux-practices$ mkdir /home/abdullah/linux-practices/devopsdir/aws      # absolute
abdullah@DevOps:~/linux-practices$ ls devopsdir/
ansible  aws
```

---

## 📋 Copying Files & Directories — `cp`

**Copy a file into a directory:**

```bash
abdullah@DevOps:~/linux-practices$ cp file1 testdir/
abdullah@DevOps:~/linux-practices$ cd testdir/
abdullah@DevOps:~/.../testdir$ ls
file1
```

**Copy a directory recursively (`-r`) with verbose, force, and preserved attributes:**

```bash
abdullah@DevOps:~/linux-practices$ cp -rvfp testdir/ vpdir/
'testdir/' -> 'vpdir/testdir'
'testdir/file1' -> 'vpdir/testdir/file1'
```

| Flag | Meaning |
|---|---|
| `-r` | Recursive (needed for directories) |
| `-v` | Verbose — shows what's being copied |
| `-f` | Force overwrite |
| `-p` | Preserve file attributes (permissions, timestamps) |

---

## 🚚 Moving / Renaming — `mv`

`mv` moves files or directories, and is also used to rename them.

```bash
abdullah@DevOps:~/linux-practices$ mv devopsdir/ vpdir/
abdullah@DevOps:~/linux-practices$ mv file3 file4 vpdir/
```

---

## 🗑 Removing Files & Directories — `rm`

```bash
abdullah@DevOps:~/linux-practices$ rm file1
abdullah@DevOps:~/linux-practices$ rm -rf testdir/
```

| Flag | Meaning |
|---|---|
| `-r` | Recursive — needed to remove directories |
| `-f` | Force — no confirmation prompts |

> ⚠️ `rm -rf` is permanent and does **not** go to a trash bin. Double-check your path before running it.

---

## 🔗 Types of Files in Linux

| File Type | First Char in Listing | Description |
|---|---|---|
| Regular file | `-` | Normal files — text, data, or executables |
| Directory | `d` | Files that are lists of other files |
| Link | `l` | A shortcut pointing to the actual file's location |
| Special file | `c` | Used for input/output, e.g. files in `/dev` |
| Socket | `s` | Special file for inter-process networking |
| Pipe | `p` | Special file allowing processes to communicate without network sockets |

### Symbolic Links

Symbolic links are like desktop shortcuts in Windows. Create one with `ln -s`:

```bash
abdullah@DevOps:~/linux-practices$ ln -s /var/log/ logdir
abdullah@DevOps:~/linux-practices$ ls -l
lrwxrwxrwx 1 abdullah abdullah 9 Apr 2 18:41 logdir -> /var/log/
```

---

## 🧾 Quick Reference

| Command | Purpose |
|---|---|
| `pwd` | Show current directory |
| `mkdir <dir>` | Create a directory |
| `cd <dir>` | Change directory |
| `cd -` | Go to the previous directory |
| `ls` / `ls -la` | List files/directories |
| `touch <file>` | Create an empty file |
| `cp <src> <dst>` | Copy a file |
| `cp -rvfp <src> <dst>` | Copy a directory recursively |
| `mv <src> <dst>` | Move or rename |
| `rm <file>` | Remove a file |
| `rm -rf <dir>` | Remove a directory forcefully |
| `ln -s <target> <link>` | Create a symbolic link |

---

## 📌 Key Takeaways

- `pwd`, `cd`, `ls`, `mkdir`, `touch` are the daily-driver navigation/creation commands.
- Absolute paths always start with `/`; relative paths are resolved from `pwd`.
- `cp`, `mv`, and `rm` all support recursive operation on directories via `-r`.
- Linux distinguishes several file types (regular, directory, link, special, socket, pipe) — visible as the first character in `ls -l` output.
- Symbolic links (`ln -s`) work like Windows shortcuts and are heavily used for versioning and configuration management in DevOps.

---

## 📚 Topics Covered in This Repository

- [x] Linux Introduction
- [x] Basic Commands
- [ ] Vim Editor
- [ ] Filters & I/O Redirection
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
