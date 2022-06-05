# Users and groups
 
---

## UID

User IDentifier

0 -> root

0 - 100 -> static system

< 1000 -> dynamic system

> 1000 -> other

<br> 

```bash
$ useradd -s <shell> -c <comm> -d <home> -m -g <group> -G <additional_group> -K <skeleton>
```

List user

```bash
$ cat /etc/passwd
$ getent passwd
```

Create user

```bash
$ sudo useradd testuser
```

```bash
# Configuration file of useradd
$ cat /etc/default/useradd
```

---

## Groups

<br>

### GID

0 -> root's group

100 -> default group "users"

> 1000 -> user groups

<br>

List group

```bash
$ getent group
$ cat /etc/group
```

Add group

```bash
# Spécify id group
$ groupadd <group_name> -g <id_num>
$ groupadd grouptest -g 1100
```

```bash
# Configuration file of groupadd
$ cat /etc/login.defs
```

Change gid (use with caution)

```bash
$ groupmod -g <new_gid> <group_name>
$ groupmod -g 1002 grouptest
```

<br>

---

## 

