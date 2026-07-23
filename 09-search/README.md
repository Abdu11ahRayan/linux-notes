#  Search

> **Repository:** DevOps Linux Notes — Section 9
>
> Quick reference for the core search commands: text search, filename lookups, and finding files by size.

---

##  grep — Search Text Inside Files

```bash
$ grep pattern files          # Search for a pattern in files — you'll use this constantly
$ grep -r pattern dir         # Search recursively for a pattern inside a directory
```

---

##  locate — Find Files by Name (Fast, Indexed)

```bash
$ locate file                 # Find all instances of a file by name
```

> 💡 `locate` searches a pre-built index (updated via `updatedb`), so it's much faster than `find` — but it can be out of date if the index hasn't refreshed since the file was created.

---

##  find — Search the Filesystem Directly

```bash
$ find /home/abdullah -name 'index*'      # Find files whose names start with "index"
$ find /home -size +10000k                # Find files larger than 10000k in /home
```

`find` searches live on disk (no index), so it's always accurate but slower than `locate` on large filesystems.

---

##  Quick Reference

| Command | Purpose |
|---|---|
| `grep pattern file` | Search for text inside a file |
| `grep -r pattern dir` | Recursive text search through a directory |
| `locate file` | Fast, indexed filename search |
| `find /path -name 'pattern'` | Search by filename pattern |
| `find /path -size +Nk` | Search by file size |

---

##  Key Takeaways

- `grep` searches **inside** file content; `find` and `locate` search for files **by name/attributes**.
- `locate` is fast because it queries a pre-built index — but that index can go stale.
- `find` is slower but always reflects the current state of the filesystem, and supports rich filters (name, size, type, owner, and more — see the Filters & I/O Redirection notes for the full option table).

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
