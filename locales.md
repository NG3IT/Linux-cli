# Locales
 
---

## List locales

```bash
$ cat /etc/default/locale
$ locale
$ localectl
```

<br>

---

## Locales details

``` bash
$ locale - <locale_key>
$ locale -k LC_TIME
```

<br>

---

## Update locale

```bash
$ sudo update-locale <locale_key>=<value>
$ sudo update-locale LC_PAPER=en_US.UTF-8
```

<br>

---

## Change keyboard settings

```bash
$ setxkbmap fr
$ setxkbmap us

$ sudo loadkeys fr
```
