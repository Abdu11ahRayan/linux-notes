#  Vim Editor

> **Repository:** DevOps Linux Notes — Section 3
>
> `vi`/`vim` is the default command-line text editor on almost every Linux server — essential for editing configs when there's no GUI.

---

##  What is Vim?

- **VI** — Visual display editor
- **VIM** — Visual display editor **Improved**

It's a command-mode editor for files. Other Linux editors exist (`emacs`, `gedit`), but `vi`/`vim` is the most widely used — and often the *only* editor available on minimal server installs.

---

##  Installing Vim

```bash
abdullah@DevOps:~/linux-practices$ sudo apt-get install vim
[sudo] password for abdullah:
Reading package lists... Done
Building dependency tree
Reading state information... Done
```

---

##  The 3 Modes of Vim

| Mode | Purpose |
|---|---|
| **Command Mode** | Default mode on open. Navigate, delete, copy, paste. |
| **Insert Mode (Edit Mode)** | Type/edit text. |
| **Extended Command Mode (Colon Mode)** | Save, quit, search/replace, set options. |

> 💡 When you open Vim, you always start in **Command Mode**.

---

##  Basic Workflow

```bash
abdullah@DevOps:~/linux-practices$ vim firstfile.txt
```

1. Hit `i` to enter **Insert Mode**.
2. Type your content.
3. Hit `Esc` to return to **Command Mode**.
4. Type `:wq` and hit `Enter` to save and quit.

```bash
This is first line in vim editor.
This one's second
So on
and
So forth.
:wq
```

**Read the file back:**

```bash
abdullah@DevOps:~/linux-practices$ cat firstfile.txt
This is first line in vim editor.
This one's second
So on
and
So forth.
```

---

##  Command Mode Shortcuts

| Key | Action |
|---|---|
| `gg` | Go to the beginning of the file |
| `G` | Go to the end of the file |
| `w` | Move cursor forward, word by word |
| `b` | Move cursor backward, word by word |
| `nw` | Move forward *n* words (e.g. `5w`) |
| `nb` | Move backward *n* words (e.g. `5b`) |
| `u` | Undo last change |
| `Ctrl + R` | Redo |
| `yy` | Copy (yank) a line |
| `nyy` | Copy *n* lines (e.g. `4yy`) |
| `p` | Paste below the cursor |
| `P` | Paste above the cursor |
| `dw` | Delete a word |
| `x` | Delete a character (like DEL key) |
| `dd` | Delete the entire line |
| `ndd` | Delete *n* lines from cursor (e.g. `5dd`) |
| `/word` | Search for a word in the file |

---

##  Extended Mode (Colon Mode)

Used to save, quit, or configure — accessed with `:` from Command Mode.

| Command | Action |
|---|---|
| `:w` | Save the changes |
| `:q` | Quit (without saving) |
| `:wq` | Save and quit |
| `:w!` | Save forcefully |
| `:wq!` | Save and quit forcefully |
| `:x` | Save and quit (same as `:wq`) |
| `:X` | Add/remove a password on the file |
| `:20` | Go to line 20 (or any line `n`) |
| `:set nu` | Show line numbers |
| `:set nonu` | Hide line numbers |

---

##  Quick Reference

| Task | Keys |
|---|---|
| Enter Insert Mode | `i` |
| Exit Insert Mode | `Esc` |
| Save & quit | `Esc` → `:wq` → `Enter` |
| Quit without saving | `Esc` → `:q!` → `Enter` |
| Delete a line | `dd` |
| Copy a line | `yy` |
| Undo | `u` |
| Search | `/searchterm` |

---

##  Key Takeaways

- Vim has 3 modes: Command (default), Insert (editing), and Extended/Colon (save, quit, search).
- Always start in Command Mode — press `i` to edit, `Esc` to get back out.
- `:wq` is the single most important shortcut to memorize — save and quit.
- Vim is unavoidable in DevOps: editing configs on remote servers over SSH almost always means using `vi`/`vim`.

---

##  Topics Covered in This Repository

- [x] Linux Introduction
- [x] Basic Commands
- [x] Vim Editor
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
