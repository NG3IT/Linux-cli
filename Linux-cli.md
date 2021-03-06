# Linux

## Summary

1. [Help](https://github.com/NG3IT/Linux-cli/edit/main/Linux-cli.md#help)
2. RHEL/CentOS/OPENSuse()
    1. [Package Managment](https://github.com/NG3IT/Linux-cli/edit/main/Linux-cli.md#package-managment)
        1. [RPM]()
        2. [Requests RPM DB]()
        3. [Package verification]()
        4. [Extract package content]()
        5. [Repo Configuration]()
        6. [Repo usage]()
            1. [Metadata cache]()
            2. [List packages]()
            3. [Search package]()
            4. [Install packages]() 
            5. [Delete package]()
            6. [Updates]()
        7. [Kernel update]()
3. [Debian/Ubuntu]()
    1. [Package Managment](https://github.com/NG3IT/Linux-cli/edit/main/Linux-cli.md#package-managment)
        1. [dpkg]()

---

## Help

```bash
# Classical help
$ man <command>
$ <command> --help
$ <command> -h
```

```bash
# Specify man section
# 1. Shell's commands
# 2. Kernel API
# 3. Libraries
# 4. Special files
# 5. File format
# 6. Games, gadgets, etc.
# 7. Miscellaneous
# 8. Administrative commands
# 9. Sub program

# Example
# Get passwd file format
$ man 5 passwd 
```

```bash
# Retrieve command
$ man -k <pattern>
```

---

## Package managment

### RPM

RPM database is here : ```/var/lib/rpm``` **(do not interracte directly with this db)**

Naming rule : ```name-version-edition.arch.rpm```

```bash
# Package installation
$ rpm -i <package_name>.rpm
# Package update (if package is not present on system, it will be installed)
$ rpm -Uvh <package_name>.rpm
# Package update (if package is not present on system, it will not be installed)
$ rpm -Fvh <package_name>.rpm
# Delete package
$ rpm -e <name>
$ rpm -e php
```

#### Requests RPM DB

```bash
# General informations
$ rpm -qi
# List all packages installed
$ rpm -qa
# List files installed
$ rpm -ql
# Find package who contains pattern
$ rpm -qp <pattern>

# Example
$ rpm -qilp <package_name>.rpm
```

#### Package verification

```bash
# Run verification
$ rpm -V <name>
$ rpm -V php
```

#### Extract package content

```bash
$ rpm2cpio <package_name>.rpm > <name>.cpio
$ file <name>.cpio
```

#### Repo Configuration

```bash
# Create or edit file on /etc/yum.repos.d (simple example is following)
# [repo_name]
# name=<repo_name>
# baseurl=<url>
# gpgcheck=0 (if gpgcheck desiabled is necessary)
```

#### yum : repo usage

##### Metadata cache

```bash
# Force metadata cache to refresh
$ yum makecache

# Delete metadata cache 
$ yum clean all

# Configuration on /etc/yum.conf
# metadata_expire=1h
```

##### List packages

```bash
# List all available packages
$ yum list available <pattern>
$ yum list available kernel\*
# Show all versions, not only the last
$ yum list available <pattern> --showduplicates

# Get informations about package
$ yum info <pattern>
$ yum info php
```

##### Search package

```bash
$ yum search <package_name>
$ yum search php
```

##### Install packages

```bash
$ yum install <package_name>
$ yum install -y <package_name>
```

##### Delete package

```bash
$ yum remove <package_name>
$ yum remove php
```

##### Updates

```bash
# Check if updates availables
$ yum check-update

# Update specific package
$ yum update <package_name>
$ yum update php

# Update all packages
$ yum update

# Update with exclusion
$ yum --exclude=<pattern> update
$ yum --exclude=kernel\* update

# Distribution upgrade
$ yum upgrade

# Distribution upgrade with exclusion
$ yum --exclude=<pattern> upgrade
$ yum --exclude=kernel\* upgrade
```

#### zypper : repo usage

##### Repo manipulaton

The configuration directories are on -> /etc/zypp/repos.d 

```bash
# Print active repos in priority order
$ zypper lr -E
# Scan, add and automatic refresh repo
$ zypper addrepo -c -f -n <repo_name> <url>
$ zypper addrepo -c -f -n "Mozilla-repo" http://[...]
# Delete repo
$ zypper removerepo <repo_name>
# Modify repo
$ zypper mr <repo_name>
# Update package db
$ zypper clean
$ zypper refresh
```

##### Search and install package

```bash
# Search
$ zypper se <pattern>
$ zypper se screen
# Install
$ zypper in <pattern>
$ zypper in screen
```

##### Delete package

```bash
$ zypper rm -y <pattern>
$ zypper rm -y screen
```

##### Update packages

```bash
# Update packages with origin repo
$ zypper update
# Update packages with newer version, also in other repos
$ zypper dup 
```

##### Delete package

```bash
$ 
``` 

##### Kernel update

```bash
# 1. New kernel instalation
$ rpm -i <new_kernel>.rpm
# 2. Reboot and test
# 3. Optionnal delete
$ rpm -e <old_kernel>
# 4.1. Grub1 modification : edit /boot/grub/grub.conf and modify the default line
# 4.2. Grub2 modification : execute command 'grub2-mkconfig' for generate new /boot/grub2/grub.cfg file
```

 ##### Download package without install

```bash
# The yumdownloader tool is in yum-utils package. You need to install it before
$ yum install -y yum-utils
$ yumdownloader <package_name>
$ yumdownloader php
```

---

# Debian/Ubuntu

## Patch managment

#### dpkg

dpkg database is here : ```/var/lib/dpkg``` **(do not interracte directly with this db)**

Naming rule : ```name-version-edition.arch.dpkg```

```bash
# Package installation (Update if package is already installed
$ dpkg -i <package_name>.rpm

# Update only if package is already installed
# First check if package is already installed
$ (dpkg -l <package_name> | grep ^ii > /dev/null) && echo INSTALLED || echo NOTINSTALLED
# If package is installed
$ dpkg -l <package_name>.deb

# Example
$ (dpkg -l php | grep ^ii >/dev/null) && dpkg -l php.deb

# Delete package (with delete configuration files)
$ dpkg -r <name>
$ dpkg -r php

# Delete package (and configuration files)
$ dpkg -P <name>
$ dpkg -P php

# Force delete and configuration file deletion
$ dpkg --force-all --purge <package_name>.dpkg
$ dpkg --force-all --purge php.dpkg
```

#### Requests dpkg

```bash
# List all known packages by system
$ dpkg -l
$ dpkg -l "php*"

# List all packages installed
$ COLUMNS=160 dpkg -l | grep ^ii | awk '{print $2}'
$ dpkg --get-selections

# Find package with file
$ dpkg -S <full_path_file>
$ dpkg -S /usr/bin/basename

# List content of package
$ dpkg -L <package_name> | grep <pattern>
$ dpkg -L coreutils | grep bin
```

#### Convert RPM package to dpkg

```bash
$ alien -d <rpm_name>.rpm
$ alien --scripts -d <rpm_name>.rpm
# Example
$ alien -d lgtoclnt-7.4-1.i686.rpm
```

#### Installed Package configuration/reconfiguration

```bash
$ debconf-show <package_name>
$ dpkg-reconfigure <package_name>
```

#### APT

File repos configuration ```/etc/apt/sources.list``` and ```/etc/apt/sources.list.d```

```bash
# List active repos
$ cat /etc/apt/sources.list |egrep -v "^(#|$)"
```

##### Create repo

```bash
$ 
```

##### Repo usage

```bash
# Update db
$ sudo apt -y update

# Upgrade packages
$ sudo apt -y upgrade

# Upgrade distribution
$ sudo apt -y dist-upgrade

# Search package
$ sudo apt-cache search <pattern>
$ sudo apt-cache search screen

# Install package
$ sudo apt install <pattern>
$ sudo apt install screen

# Install simulation
$ sudo apt install -s <pattern>
# Fix-broken
$ sudo apt install -f <pattern>

# Delete package
$ apt remove <package>
# Delete package and dependencies
$ apt autoremove <package>
$ apt autoclean <package>
```

#### snappy

##### Snap package usage

```bash
# Find snap package
$ snap find <pattern>
$ snap find screen
# Install snap package
$ snap install <pattern>
$ snap install screen
# List snap package
$ snap list
# Update snap images
$ snap refresh <pattern>
# Remove snap package
$ snap remove <pattern>
```

#### Install from sources

##### 
