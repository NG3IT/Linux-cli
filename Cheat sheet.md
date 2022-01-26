# Linux administration (CPU, disk usage, memory, ...)

## Disk usage

```bash
# -a -> show files and direcories du in .
# -h -> human readable
# -c -> print total du in the end
# --time -> show the last modification date
$ du -ahc -d <subdirectories numbers (1,2,3,...)> --time .
```

```bash
# Show informations about file (creation, modification, access, ...)
$ stat <file>
```

---

# Find informations...

```bash
# grep -E -> regex
# grep -F -> fixes string
```

```bash
# -R -> recursive
# -i -> no case
# -n -> show line(s) which correspond with pattern
$ grep -Rin <file>
```

---
