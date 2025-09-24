# Linux Fundamentals — Study Guide & Bandit Walkthrough

Clean, copy‑pasteable notes with correct commands and brief explanations. Built from real troubleshooting you’ve done (nmap `-sV`, `openssl s_client -quiet`, strict SSH key perms, SUID/SGID).

---

## 📌 Contents
- [1. CLI essentials](#1-cli-essentials)
- [2. Files, permissions, ownership](#2-files-permissions-ownership)
- [3. Root & sudo](#3-root--sudo)
- [4. Streams & redirection](#4-streams--redirection)
- [5. Env vars & aliases](#5-env-vars--aliases)
- [6. Vim quickref](#6-vim-quickref)
- [7. Networking cheats (ssh, nc, openssl, nmap)](#7-networking-cheats-ssh-nc-openssl-nmap)
- [8. Archives & compression](#8-archives--compression)
- [9. Text tools (grep, diff, tr)](#9-text-tools-grep-diff-tr)
- [10. mktemp](#10-mktemp)
- [11. OverTheWire — Bandit 0→20](#11-overthewire--bandit-020)
- [12. Troubleshooting](#12-troubleshooting)

---

## 1) CLI essentials
- Navigation: `pwd`, `ls -la`, `cd -` (previous dir)
- View files: `cat`, `less`, `head`, `tail -f`
- Create/Remove/Move: `mkdir -p`, `rm -rf`, `cp -r`, `mv`
- Locate programs: `which <cmd>`, `whereis <cmd>`
- Help: `man <cmd>`, `<cmd> --help`
- Anatomy: **command** + **options** + **arguments** → e.g. `ls -a /home`

## 2) Files, permissions, ownership
- `ls -l` → `rwx` for **user | group | other**; `d`=dir, `-`=file.
- Octal: r=4, w=2, x=1 → `chmod 755 file` → `-rwxr-xr-x`
- Symbolic: `chmod u+x file`, `chmod g-r file`, `chmod u=rw,g=r,o=r file`
- Ownership: `chown user:group file`, `chgrp group file`, `chown -R user:group dir/`
- **setuid** (s on user/owner exec bit): program runs with **file owner’s** privileges.
- **setgid** (s on group exec bit): program runs with **file group’s** privileges.
- Spot SUID: `-rwsr-xr-x root root ... /path/to/bin` (note the **s**).

## 3) Root & sudo
- `sudo <cmd>` → run with elevated privileges.
- `sudo su -` → root shell (be careful!).
- Logs commonly at `/var/log/auth.log` (varies by distro).

## 4) Streams & redirection
- FDs: stdin=0, stdout=1, stderr=2
- Redirect: `cmd > out.txt` (stdout), `cmd 2> err.txt` (stderr), `cmd &> all.txt` (both)
- Discard: `cmd 2> /dev/null`
- File as input: `cat < file.txt`

## 5) Env vars & aliases
- Show: `env` / `printenv`; echo: `echo $HOME`, `echo $PATH`
- Temp var: `VAR=value cmd` (only for that process)
- Persist: add `export VAR=value` to `~/.bashrc` then `source ~/.bashrc`
- Aliases: `alias ll="ls -lah"` (persist by adding to shell rc)

## 6) Vim quickref
- Modes: Normal (Esc), Insert (i), Visual (v)
- Move: `0` start of line, `$` end; search `/word` → `n`/`N`
- Edit: `dd` (delete line), `yy` (copy line), `p` (paste), `u` (undo), `Ctrl+r` (redo)
- Save/Quit: `:w`, `:wq`, `:q!`

## 7) Networking cheats (ssh, nc, openssl, nmap)
- **ssh**: `ssh -i ~/.ssh/id_ed25519 user@host -p 2220`
- **nc (netcat)**: client `nc -nv host port`, server `nc -lvkp 1234`
- **openssl s_client** (speak TLS): `openssl s_client -quiet -connect localhost:31790`
- **nmap** (service/version detect): `nmap -sV -p 31000-32000 localhost`  
  `-sV` = probe to identify **service & version** (helps spot TLS endpoints).

## 8) Archives & compression
- Detect type: `file data`
- bzip2: `bunzip2 data.bz2` → outputs `data` (unknown name: `bunzip2 data` → `data.out`)
- tar:
  - Extract: `tar -xvf file.tar` (x=extract, v=verbose, f=file)
  - Create:  `tar -cvf out.tar dir/`
  - With gzip: `tar -xvzf file.tar.gz` / `tar -cvzf out.tar.gz dir/`

## 9) Text tools (grep, diff, tr)
- **grep**: `grep -R "needle" .`
- **diff**:
  - Basic: `42c42` means “line 42 changed to line 42”.
  - Unified: `diff -u old new` → shows context; `-` old, `+` new.  
    In `@@ -35,7 +35,7 @@` the **7** is the number of context lines.
- **tr** (ROT13 example): `tr 'A-Za-z' 'N-ZA-Mn-za-m'`

## 10) mktemp
- Secure tmp dir: `mktemp -d` (auto name)
- Template must include `XXXXXX` if you provide a pattern:  
  `mktemp -d /tmp/Goku.XXXXXX`

---

## 11) OverTheWire — Bandit 0→20

> Host: `bandit.labs.overthewire.org` • Port: `2220`  
> Pattern: **Goal → Approach → Commands → Why**

### Level 0 → 1
**Goal**: Read `readme` for next password.  
**Cmds**:
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
ls; cat readme
```

### Level 1 → 2
**Goal**: Read file literally named `-`.  
```bash
cat ./-
# or: cat -- -
```

### Level 2 → 3
**Goal**: Read file with spaces in name.  
```bash
cat -- "spaces in this filename"
# or: cat "spaces in this filename"
```

### Level 3 → 4
**Goal**: Hidden file inside `inhere`.  
```bash
cd inhere; ls -a
cat .hidden
```

### Level 4 → 5
**Goal**: Among many, find the human‑readable file.  
```bash
cd inhere
file ./*    # look for “ASCII text”
cat ./-file07
```

### Level 5 → 6
**Goal**: Find a file of exactly 1033 bytes.  
```bash
find . -type f -size 1033c -exec ls -l {} \;
cat ./maybehere07/.file2
```

### Level 6 → 7
**Goal**: Search entire FS for file with specific owner/group/size.  
```bash
find / -type f -size 33c -user bandit7 -group bandit6 2>/dev/null
cat /path/from/above
```

### Level 7 → 8
**Goal**: Line containing “millionth”.  
```bash
grep "millionth" data.txt
```

### Level 8 → 9
**Goal**: Unique line appears exactly once.  
```bash
sort data.txt | uniq -u
```

### Level 9 → 10
**Goal**: Extract readable strings then filter.  
```bash
strings data.txt | grep '='
```

### Level 10 → 11
**Goal**: Base64 decode.  
```bash
base64 -d data.txt
```

### Level 11 → 12
**Goal**: ROT13 decode.  
```bash
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt
```

### Level 12 → 13
**Goal**: Data is repeatedly packed/encoded; unwind step‑by‑step.  
```bash
WORKDIR="$(mktemp -d)"; cd "$WORKDIR"
xxd -r data.txt > data
file data               # pick next: gunzip / bunzip2 / tar -xvf / etc.
# repeat until you reach cleartext password
```

### Level 13 → 14
**Goal**: Login to next level using provided private key.  
```bash
ssh -i /home/bandit13/sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

### Level 14 → 15
**Goal**: Send current password to local port 30000.  
```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

### Level 15 → 16
**Goal**: Same idea but TLS on 30001.  
```bash
cat /etc/bandit_pass/bandit15 | openssl s_client -quiet -connect localhost:30001
```

### Level 16 → 17
**Goal**: Scan 31000–32000, fetch key from TLS service, fix perms, login.  
```bash
nmap -sV -p 31000-32000 localhost
openssl s_client -quiet -connect localhost:31790

# save the key block you receive:
cat > /tmp/key17 <<'KEY'
-----BEGIN RSA PRIVATE KEY-----
...paste...
-----END RSA PRIVATE KEY-----
KEY

chmod 600 /tmp/key17
ssh -i /tmp/key17 bandit17@bandit.labs.overthewire.org -p 2220
```

### Level 17 → 18
**Goal**: One line differs between two files.  
```bash
diff -u passwords.old passwords.new
# the line starting with '+' is the new one (password)
```

### Level 18 → 19
**Goal**: Login auto‑logs you out; run a remote command in the SSH invocation.  
```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 'cat readme'
```

### Level 19 → 20
**Goal**: Use SUID wrapper to run a command as the target user.  
```bash
ls -l
./bandit20-do cat /etc/bandit_pass/bandit20
```

---

## 12) Troubleshooting
- **“UNPROTECTED PRIVATE KEY FILE!”** → `chmod 600 keyfile`
- Nothing after connecting (nc/openssl) → press **ENTER**, verify port & TLS
- SSH “Permission denied (publickey)” → wrong key/user/perms/path
- `nmap -sV` = service/version detection (helps spot TLS endpoints)

## 62) CLI Shortcuts
- `history` → list commands from session, numbered; re-run with `!<num>` (e.g. `!220`)
- `Ctrl+R` → reverse search history; press repeatedly to cycle matches
- `Enter` → execute found command; `Ctrl+J` → insert at prompt without executing

