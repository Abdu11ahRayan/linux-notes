#  Software Management

> **Repository:** DevOps Linux Notes — Section 8
>
> How to install, update, and remove software on both RPM-based (CentOS/RHEL) and Debian-based (Ubuntu) systems — a must-know split for any DevOps engineer managing mixed environments.

---

##  Downloading Packages from the Internet

### CentOS — Installing `tree` with `curl` + `rpm`

```bash
[root@Abdullah ~]# curl https://rpmfind.net/linux/centos/7.9.2009/os/x86_64/Packages/tree-1.6.0-10.el7.x86_64.rpm -o tree-1.6.0-10.el7.x86_64.rpm

[root@Abdullah ~]# rpm -ivh tree-1.6.0-10.el7.x86_64.rpm
Preparing...                          ################ [100%]
Updating / installing...
   1:tree-1.6.0-10.el7               ################ [100%]
```

### CentOS — Installing `httpd` (fails on dependencies)

```bash
[root@Abdullah ~]# curl https://rpmfind.net/linux/centos/7.9.2009/os/x86_64/Packages/httpd-2.4.6-95.el7.centos.x86_64.rpm -o httpd-2.4.6-95.el7.centos.x86_64.rpm

[root@Abdullah ~]# rpm -ivh httpd-2.4.6-95.el7.centos.x86_64.rpm
error: Failed dependencies:
    /etc/mime.types is needed by httpd-2.4.6-95.el7.centos.x86_64
    system-logos >= 7.92.1-1 is needed by httpd-2.4.6-95.el7.centos.x86_64
    http-tools = 2.4.6-95.el7.centos is needed by httpd-2.4.6-95.el7.centos.x86_64
    libapr-1.so.0()(64bit) is needed by httpd-2.4.6-95.el7.centos.x86_64
    libaprutil-1.so.0()(64bit) is needed by httpd-2.4.6-95.el7.centos.x86_64
```

> ⚠️ `rpm` alone doesn't resolve dependencies — installing one package can fail because of missing dependencies, and with hundreds of dependencies this becomes unmanageable. That's exactly what **YUM/DNF** solve.

---

##  CentOS/RHEL — YUM & DNF

YUM reads repository configuration files from `/etc/yum.repos.d/` to know **where** to download packages and their dependencies from.

```bash
[root@Abdullah ~]# ls /etc/yum.repos.d/
CentOS-Base.repo  CentOS-CR.repo  CentOS-Debuginfo.repo  CentOS-fasttrack.repo  CentOS-Media.repo  CentOS-Sources.repo  CentOS-Vault.repo
```

**Install a package (resolves dependencies automatically):**

```bash
[root@Abdullah ~]# yum install httpd -y
...
Installed:
  httpd.x86_64 0:2.4.6-97.el7.centos

Dependency Installed:
  apr.x86_64 0:1.4.8-7.el7   apr-util.x86_64 0:1.5.2-6.el7   centos-logos.noarch 0:70.0.0.6-3.el7.centos   httpd-tools.x86_64 0:2.4.6-97.el7.centos
  mailcap.noarch 0:2.1.41-2.el7
Complete!
```

**Remove a package:**

```bash
[root@Abdullah ~]# yum remove httpd -y
Removing:
  httpd    x86_64    2.4.6-97.el7.centos    @updates    9.4 M
...
Removed:
  httpd.x86_64 0:2.4.6-97.el7.centos
Complete!
```

**Update all packages:**

```bash
[root@Abdullah ~]# yum update
```

### YUM Commands Cheatsheet

| Command | Purpose |
|---|---|
| `yum --help` | Show help |
| `yum search PACKAGE` | Search available repositories |
| `yum install PACKAGE -y` | Install a package |
| `yum reinstall PACKAGE` | Reinstall a package |
| `yum remove PACKAGE` | Remove a package |
| `yum update` | Update all packages |
| `yum update PACKAGE` | Update a specific package |
| `yum grouplist` | List available package groups |
| `yum groupinstall "Group Name"` | Install all packages in a group |
| `yum repolist` | List enabled repositories |
| `yum install epel-release` | Add the EPEL extra-packages repository |
| `yum clean all` | Clean the YUM cache |
| `yum history` | View install/update history |
| `yum info PACKAGE` | Show version, size, source, repo info |

### DNF Commands Cheatsheet (CentOS 8+)

DNF is the modern successor to YUM (CentOS 8+, Fedora) — commands are nearly identical.

| Command | Purpose |
|---|---|
| `dnf --help` | Show help |
| `dnf search PACKAGE` | Search available repositories |
| `dnf install PACKAGE -y` | Install a package |
| `dnf reinstall PACKAGE` | Reinstall a package |
| `dnf remove PACKAGE` | Remove a package |
| `dnf update` | Update all packages |
| `dnf update PACKAGE` | Update a specific package |
| `dnf grouplist` | List available package groups |
| `dnf groupinstall "GROUPNAME"` | Install all packages in a group |
| `dnf repolist` | List enabled repositories |
| `dnf install epel-release` | Add the EPEL repository |
| `dnf clean all` | Clean the DNF cache |
| `dnf history` | View history |
| `dnf info PACKAGE` | Show package info |

---

##  Ubuntu — DPKG & APT

### Installing `tree` with `wget` + `dpkg`

```bash
root@Abdullah:~# wget http://archive.ubuntu.com/ubuntu/pool/universe/t/tree/tree_1.7.0-3_amd64.deb -o tree_1.7.0-3_amd64.deb
root@Abdullah:~# dpkg -i tree_1.7.0-3_amd64.deb
Selecting previously unselected package tree.
Unpacking tree (1.7.0-3) ...
Setting up tree (1.7.0-3) ...
```

Like YUM for CentOS, Ubuntu uses **APT** to resolve dependencies automatically. Its repository roadmap lives in `/etc/apt/sources.list` — this file tells the system where to download programs for installation or upgrade.

```bash
root@Abdullah:/etc/apt# cat /etc/apt/sources.list
deb http://us-east-1.ec2.archive.ubuntu.com/ubuntu/ focal main restricted
deb http://us-east-1.ec2.archive.ubuntu.com/ubuntu/ focal-updates main restricted
deb http://us-east-1.ec2.archive.ubuntu.com/ubuntu/ focal universe
...
```

**Update the package list:**

```bash
root@Abdullah:~# apt update
Hit:1 http://us-east-1.ec2.archive.ubuntu.com/ubuntu focal InRelease
...
27 packages can be upgraded. Run 'apt list --upgradable' to see them.
```

**Search for a package:**

```bash
root@Abdullah:~# apt search apache2
apache2/focal-updates,now 2.4.41-4ubuntu3.4 amd64 [installed]
  Apache HTTP Server
```

**Install a package:**

```bash
root@Abdullah:~# apt install apache2 -y
...
Setting up apache2 (2.4.41-4ubuntu3.4) ...
```

**Remove a package:**

```bash
root@Abdullah:~# apt remove apache2 -y
...
Removing apache2 (2.4.41-4ubuntu3.4) ...
```

### APT Commands Cheatsheet

| Command | Purpose |
|---|---|
| `apt search PACKAGE` | Search available repositories |
| `apt install PACKAGE -y` | Install a package |
| `apt reinstall PACKAGE` | Reinstall a package |
| `apt remove PACKAGE` | Remove a package |
| `apt update` | Refresh package lists |
| `apt update PACKAGE` | Update a specific package |
| `apt repolist` | List enabled repositories |
| `apt clean all` | Clean the APT cache |
| `apt history` | View history |
| `apt show PACKAGE` | Show version, size, source, repo info |

### RPM Commands Cheatsheet

| Command | Purpose | Example |
|---|---|---|
| `rpm -ivh {file}` | Install a package | `rpm -ivh mozilla-mail-1.7.5-17.i586.rpm` |
| `rpm -Uvh {file}` | Upgrade a package | `rpm -Uvh mozilla-mail-1.7.6-12.i586.rpm` |
| `rpm -ev {package}` | Remove a package | `rpm -ev mozilla-mail` |
| `rpm -ev --nodeps {package}` | Remove without dependency check | `rpm -ev --nodeps mozilla-mail` |
| `rpm -qa` | List all installed packages | `rpm -qa \| less` |
| `rpm -qi {package}` | Show package info | `rpm -qi mozilla-mail` |
| `rpm -qf {/path}` | Find which package owns a file | `rpm -qf /etc/passwd` |
| `rpm -qc {package}` | List config files for a package | `rpm -qc httpd` |
| `rpm -qa --last` | List recently installed RPMs | `rpm -qa --last \| less` |
| `rpm -qpR {file}` / `rpm -qR {package}` | Show a package's dependencies | `rpm -qR bash` |

---

##  General Download Helpers

| Command | Purpose |
|---|---|
| `wget <link>` | Download a file from a link |
| `curl <link>` | Fetch a file from a link |
| `curl <link> -o <outputfile>` | Fetch a file and save it under a specific name |

---

##  Quick Comparison — RPM vs DEB Ecosystems

| | RPM-based (RHEL, CentOS, Fedora) | Debian-based (Ubuntu) |
|---|---|---|
| Low-level tool | `rpm` | `dpkg` |
| Dependency-resolving manager | `yum` (legacy) / `dnf` (modern) | `apt` |
| Repo config location | `/etc/yum.repos.d/` | `/etc/apt/sources.list` |
| Install | `yum install pkg -y` | `apt install pkg -y` |
| Remove | `yum remove pkg -y` | `apt remove pkg -y` |
| Update all | `yum update` | `apt update && apt upgrade` |

---

##  Key Takeaways

- `rpm`/`dpkg` install individual packages but **don't** resolve dependencies — that's why they fail on real-world packages like `httpd`.
- `yum`/`dnf` (CentOS/RHEL) and `apt` (Ubuntu) wrap those low-level tools and automatically pull in dependencies from configured repositories.
- Repository locations differ: `/etc/yum.repos.d/` on RPM systems, `/etc/apt/sources.list` on Debian systems.
- `dnf` is the modern replacement for `yum` on CentOS 8+/Fedora — command syntax is almost identical.
- Always run `apt update` / `yum update` (refresh package lists) before installing something new, especially on a fresh server.

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
