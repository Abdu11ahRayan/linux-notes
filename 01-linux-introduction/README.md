#  Linux Introduction

> **Repository:** DevOps Linux Notes
>
> Structured notes from the "DecodingDevOps" Udemy course (Imran Teli), part of my Linux → Bash → Git → Docker → Kubernetes → Jenkins → Terraform → Ansible → AWS DevOps roadmap.

---

##  What is Linux?

Linux is a free and open-source operating system built around the **Linux Kernel**. It's known for its stability, security, flexibility, and performance.

Unlike Windows and macOS, Linux is open source — anyone can view, modify, and distribute its source code under the appropriate licenses.

Today, Linux powers:

- Web Servers
- Cloud Infrastructure
- DevOps Platforms
- Docker Containers
- Kubernetes Clusters
- Android Devices
- Supercomputers
- IoT Devices

---

##  What is Open Source?

- Open source = software **and** source code available to everyone.
- The **Free Software Foundation** defines four core freedoms:
  1. The freedom to run the program for any purpose.
  2. The freedom to study and modify the source code.
  3. The freedom to redistribute the program.
  4. The freedom to create derivative programs.
- Many open-source licenses exist, each with its own particulars.

---

##  Linux Origins

- **1984** — The GNU Project and the Free Software Foundation
  - Created an open-source version of UNIX utilities.
  - Created the **General Public License (GPL)** — a license enforcing open-source principles.
- **1991** — Linus Torvalds
  - Created an open-source, UNIX-like kernel, released under the GPL.
  - Ported some GNU utilities and solicited help from developers online.
- **Today**
  - Linux kernel + GNU utilities = a complete, open-source, UNIX-like operating system.
  - Packaged for different audiences as **distributions**.

---

##  Why Learn Linux for DevOps?

Most production servers run Linux — it's foundational for any DevOps role.

As a DevOps Engineer, you'll use Linux to:

- Deploy applications
- Configure servers
- Manage users and permissions
- Write Bash scripts
- Install software packages
- Troubleshoot production issues
- Configure web servers
- Automate repetitive tasks
- Work with Docker and Kubernetes

> 💡 Learning Linux is the foundation of a DevOps career.

---

##  Linux Principles

- Everything is a file (including hardware).
- Small, single-purpose programs.
- Ability to chain programs together to perform complex tasks.
- Avoid captive user interfaces.
- Configuration data is stored in plain text.

---

##  Features of Linux

- Open Source
- Secure
- Stable
- Multi-user
- Multitasking
- Portable
- Highly Customizable
- Powerful Command Line Interface (CLI)
- Excellent Networking Support
- Strong Community Support
- Automation-friendly

---

##  Linux Architecture

```
+----------------------+
|        User          |
+----------------------+
           │
           ▼
+----------------------+
|    Applications      |
+----------------------+
           │
           ▼
+----------------------+
|    Shell (Bash)      |
+----------------------+
           │
           ▼
+----------------------+
|    Linux Kernel      |
+----------------------+
           │
           ▼
+----------------------+
|      Hardware        |
+----------------------+
```

| Layer | Description |
|---|---|
| **User** | The person interacting with the operating system. |
| **Applications** | Programs like VS Code, Nginx, Apache, Docker, MySQL. |
| **Shell** | Interface between the user and the kernel (e.g., Bash). Interprets commands typed in the terminal. |
| **Kernel** | The core of the OS. Handles process management, memory management, file system management, device management, and network management. |
| **Hardware** | Physical components — CPU, RAM, Disk, Keyboard, NICs. |

Multiple users can interact with applications like compilers, editors (`vi`), and commands (`cd`, `grep`, `date`) simultaneously — all mediated by the shell → kernel → hardware chain.

---

##  Linux Distributions (Distros)

A **distro** is an OS built using the Linux kernel plus additional software and package management tools.

| Distribution | Common Usage |
|---|---|
| Ubuntu | Development, Cloud |
| Debian | Stable Servers |
| CentOS Stream | Enterprise Testing |
| Rocky Linux | Enterprise Servers |
| AlmaLinux | Enterprise Servers |
| Fedora | Latest Features |
| Red Hat Enterprise Linux (RHEL) | Enterprise Production |
| Kali Linux | Cybersecurity |
| Arch Linux | Advanced Users |

**Popular Desktop Linux OS:** Ubuntu Linux, Linux Mint, Arch Linux, Fedora, Debian, OpenSUSE

**Popular Server Linux OS:** Red Hat Enterprise Linux, Ubuntu Server, CentOS, SUSE Enterprise Linux

> Most used in the IT industry today: **RPM-based** (RHEL, CentOS) and **Debian-based** (Ubuntu Server).

### RPM vs DEB — What's the difference?

From a user's point of view there isn't much difference — both are archive files with metadata attached, both have hardcoded install paths, and they differ mostly in subtle details.

| | **DEB** | **RPM** |
|---|---|---|
| Used by | Debian-based distros (Ubuntu) | Red Hat-based distros (RHEL, CentOS, Fedora) |
| Package manager | APT / DPKG | RPM / YUM / DNF |
| Example file | `google-chrome-stable_current_amd64.deb` | `google-chrome-stable-57.0.2987.133-1.x86_64.rpm` |
| Install command | `dpkg -i google-chrome-stable_current_amd64.deb` | `rpm -ivh google-chrome-stable-57.0.2987.133-1.x86_64.rpm` |

> ⚠️ **Note:** Commands, package names, and service names often differ between RPM-based and Debian-based distros — expect to learn both.

---

##  Command Line Interface (CLI)

Linux can be operated via GUI or CLI. In DevOps, almost all work happens in the **CLI** — it's faster, scriptable, and essential for managing remote servers.

```bash
pwd
ls -la
cd /etc
mkdir DevOps
```

---

##  Linux File System

Linux follows a hierarchical directory structure, starting from `/` (root).

```
/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── opt
├── proc
├── root
├── tmp
├── usr
└── var
```

### Important Directories

| Directory | Purpose |
|---|---|
| `/` | Root directory |
| `/root`, `/home/username` | Home directories |
| `/bin`, `/usr/bin`, `/usr/local/bin` | User executables |
| `/sbin`, `/usr/sbin`, `/usr/local/sbin` | System executables |
| `/etc` | Configuration files |
| `/var`, `/srv` | Logs and server data |
| `/tmp` | Temporary files |
| `/boot` | Kernels and bootloader |
| `/proc`, `/sys` | System / kernel information |
| `/lib`, `/usr/lib`, `/usr/local/lib` | Shared libraries |
| `/media`, `/mnt` | Other mount points |

---

##  Advantages of Linux

- Free to use
- Highly secure
- Stable for production environments
- Excellent performance
- Supports automation & scripting
- Large community support

---

##  Where is Linux Used?

- AWS EC2
- Microsoft Azure
- Google Cloud Platform
- Docker
- Kubernetes
- Jenkins
- GitLab CI/CD
- Nginx / Apache
- MySQL / PostgreSQL

---

##  Linux vs Windows

| Linux | Windows |
|---|---|
| Open Source | Proprietary |
| Mostly Free | Commercial Licensing |
| Bash Shell | PowerShell / CMD |
| Preferred for Servers | Popular for Desktop |
| Highly Customizable | Less Customizable |
| Excellent for Automation | GUI Focused |

---

##  Key Terms

| Term | Description |
|---|---|
| Kernel | Core of the operating system |
| Shell | Command interpreter |
| Terminal | Interface used to access the shell |
| Distribution | Complete Linux operating system |
| CLI | Command Line Interface |
| Package Manager | Installs and manages software |

---

##  Real-World DevOps Example

Imagine a company hosting a web application. A DevOps Engineer may use Linux to:

- SSH into a server
- Check running services
- Monitor CPU and memory
- Restart Apache or Nginx
- Deploy application updates
- Install Docker
- Configure Jenkins
- Manage file permissions
- Write Bash automation scripts

Without Linux knowledge, performing these tasks would be difficult.

---

##  Topics Covered in This Repository

- [x] Linux Introduction
- [ ] Basic Commands
- [ ] Vim Editor
- [ ] Filters & I/O Redirection
- [ ] Users & Groups
- [ ] File Permissions
- [ ] Sudo
- [ ] Software Management (RPM/YUM/DNF, APT/DPKG)
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

##  Key Takeaways

- Linux is an open-source operating system built around the Linux Kernel.
- The kernel is the core, handling process, memory, file system, device, and network management.
- Linux is the preferred OS for servers and cloud infrastructure.
- Most DevOps tools run on Linux.
- Distros split into RPM-based (RHEL, CentOS) and Debian-based (Ubuntu) families — each with different package managers and commands.
- Strong Linux knowledge is essential before moving on to Docker, Kubernetes, Jenkins, Terraform, and Ansible.

---

##  References

- Linux Documentation: https://docs.kernel.org/
- Ubuntu Documentation: https://ubuntu.com/server/docs
- Red Hat Documentation: https://access.redhat.com/documentation

---

*Course: DecodingDevOps by Imran Teli (Udemy) | Status: ✅ Completed*
