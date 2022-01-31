# Summary

[Administration (CPU, disk usage, memory, ...)](https://github.com/NG3IT/Linux-cli/blob/main/Cheat%20sheet.md#linux-administration-cpu-disk-usage-memory-)
[Packages manipulation (Install, update, ...)[]

---

# Linux administration (CPU, disk usage, memory, ...)

## Disk usage

```bash
# -a -> show files and direcories du in .
# -h -> human readable
# -c -> print total du at the end
# --time -> show the last modification date
$ du -ahc -d <subdirectories numbers (1,2,3,...)> --time .
```

```bash
# Show informations about file (creation, modification, access, ...)
$ stat <file>
```

---

## Find informations...

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

## Strops (STRing OPerationS)

### tr : Find and replace

```bash
$ tr --help
tr [flags] [source]/[find]/[select] [destination]/[replace]/[change]

### Flags examples
# -d -> delete set of characters
# -s -> replace the source set with the destination set

$ cat file.txt | tr -s '[a-z]' '[A-Z]'
```

### Powerful AWK

```bash
$ awk --help
awk [flags] [select pattern/find(sort)/commands] [input file]

```

---

## Download and upload

### cURL

```bash
# Display the source code of an url
$ curl <url>

# -# -> display progress meter
# -o -> get output in file
# -u -> provides user authentication <user>:<password>
# -T -> use to upload
# -x -> proxy specification
# -I -> get headers
# -b -> cookies specification
# -X -> use specific method (GET/POST/TRACE/OPTIONS)
```

---

# Packages manipulation (Install, update, ...)

## apt

```bash

```
