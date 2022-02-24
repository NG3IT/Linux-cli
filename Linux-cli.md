# Linux

## Summary

1. [Help](https://github.com/NG3IT/Linux-cli/edit/main/Linux-cli.md#help)
2. RHEL/CentOS/OPENSuse
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
    1. [DPKG]()

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

#### Repo usage

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

 ##### Download package without install it

```bash
# The yumdownloader tool is in yum-utils package. You need to install it before
$ yum install -y yum-utils
$ yumdownloader <package_name>
$ yumdownloader php
```

---

# Debian/Ubuntu

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
