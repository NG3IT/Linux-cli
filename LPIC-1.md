**LPIC-1**

---

Examples shell types :
- sh : Bourne Shell (historic reference)
- csh : C Shell
- ksh : Korn Shell
- bash : Bourne Again Shell
- zsh : Z Shell

---

How show the shells on the machine ?
```bash
cat /etc/shells
```

---

Useful shell shortcuts :
- [Ctrl] a : jump on the start of the line
- [Ctrl] e : jump at the end of the line
- [Ctrl] l : clear
- [Ctrl] u : delete the line from position to start
- [Ctrl] k : delete the line from position to end

---

Useful specific string to interact with text :
- \n : break line
- \t : tabulation
- \c : remove final line break
- \b : one caracter return
- \\ : print \

--- 

Internal VS external command

Internal commands : this commands are builtin shell. 

External commands : this commands are on the disk. When this command is executed, the file is charged on the memory and is launched as processus.

---

Internal or external command ?

```bash
$ type <command>

$ type pwd
pwd is a shell builtin

$ type df
df is /bin/df
```

--- 

Useful shortcuts
- [Ctrl] c : programm interruption
- [Ctrl] z : programm 

---

