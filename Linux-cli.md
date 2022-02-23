# Linux

## Summary

- [Help](https://github.com/NG3IT/Linux-cli/edit/main/Linux-cli.md#help)
- [Package Managment](https://github.com/NG3IT/Linux-cli/edit/main/Linux-cli.md#package-managment)

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

Requests RPM DB :

```bash
# General informations
$ rpm -qi
# List all packages installed
$ rpm -qa
# List all packages installed
$ rpm -qa
```

Kernel update :

```bash
# 1. New kernel instalation
$ rpm -i <new_kernel>.rpm
# 2. Reboot and test
# 3. Optionnal delete
$ rpm -e <old_kernel>
# 4.1. Grub1 modification : edit /boot/grub/grub.conf and modify the default line
# 4.2. Grub2 modification : execute command 'grub2-mkconfig' for generate new /boot/grub2/grub.cfg file
```


