# 🛡️ OverTheWire: Bandit Write-up (Levels 0–20)

This write-up documents my journey through Levels 0 to 20 of the [Bandit wargame](https://overthewire.org/wargames/bandit/) by OverTheWire. This game is a fantastic way to learn Linux commands, file handling, permissions, searching, and more through hands-on problem-solving.

---

## ⚔️ Level 0 → 1

**Goal:** Learn to connect to a remote machine using SSH.

**Details:** We're given a host, port, and username/password. This teaches us how to initiate a secure shell connection, which is fundamental for any CTF or server-based work.

**Solution:**
    ssh bandit0@bandit.labs.overthewire.org -p 2220

Once connected:
    ls
    cat README

This reveals the password for the next level.

---

## 🧾 Level 1 → 2

**Goal:** Read a file with a tricky filename (`-`), which could confuse the `cat` command.

**Details:** Filenames that start with `-` are interpreted as options. To prevent this, we explicitly tell the shell that it’s a filename by using `./`.

**Solution:**
    ls
    cat ./-

---

## 📁 Level 2 → 3

**Goal:** Read a file with spaces in its name.

**Details:** Filenames with spaces must be quoted or escaped. This teaches the importance of careful command usage with such files.

**Solution:**
    ls
    cat "spaces in this filename"

---

## 🔍 Level 3 → 4

**Goal:** Discover a hidden file in a directory.

**Details:** Hidden files in Linux start with a dot (`.`) and don’t appear with regular `ls`. Using `ls -la` lists all files including hidden ones.

**Solution:**
    cd inhere
    ls -la
    cat .hidden

---

## 🧱 Level 4 → 5

**Goal:** Find a specific file among many that contains ASCII text.

**Details:** Among files named similarly, only one has readable content. Use `file` or attempt to read them one by one.

**Solution:**
    cd inhere
    ls
    cat ./-file07

---

## 🧩 Level 5 → 6

**Goal:** Locate a file with specific characteristics using `find`.

**Details:** Learn to search by file size and properties like being non-executable. Reinforces `find` command syntax.

**Solution:**
    cd inhere
    find . -size 1033c ! -executable
    cat ./maybehere07/.file2

---

## 🕵️ Level 6 → 7

**Goal:** Find a file anywhere on the filesystem with specific user/group ownership and size.

**Details:** Use `find` to locate files by owner, group, and size. Suppress error messages with `2>/dev/null`.

**Solution:**
    find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
    cat /path/to/file

---

## 📄 Level 7 → 8

**Goal:** Search inside a text file for a specific line using `grep`.

**Details:** Practice using `grep` to match strings. Here, we look for the line that contains the word `millionth`.

**Solution:**
    cat data.txt | grep millionth

---

## 🔍 Level 8 → 9

**Goal:** Find the only line that occurs once in a large file.

**Details:** Teaches sorting and uniqueness tools like `sort` and `uniq`.

**Solution:**
    cat data.txt | sort | uniq -u

---

## 🧪 Level 9 → 10

**Goal:** Find lines with special characters (like `=`).

**Details:** Practice using `grep` to search for symbols and filtering outputs.

**Solution:**
    cat data.txt | grep "="

---

## 🔐 Level 10 → 11

**Goal:** Decode a Base64-encoded file.

**Details:** Introduces encoding/decoding tasks. Base64 is common in CTFs and Linux.

**Solution:**
    base64 -d data.txt

---

## 🔄 Level 11 → 12

**Goal:** Decode a file encrypted using ROT13.

**Details:** `tr` is used to shift letters. ROT13 is a simple Caesar cipher used for obfuscation.

**Solution:**
    cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

---

## 📦 Level 12 → 13

**Goal:** Unpack a file that's compressed and archived multiple times.

**Details:** Teaches how to work with different compression tools like `xxd`, `gzip`, `bzip2`, and `tar`.

**Solution:**
    mkdir /tmp/bandana
    cp data.txt /tmp/bandana
    cd /tmp/bandana
    xxd -r data.txt > bandit
    mv bandit bandit.gz
    gunzip bandit.gz
    bzip2 -d bandit
    mv bandit.out bandit.gz
    gunzip bandit.gz
    tar xvf bandit
    tar xvf data5.bin
    bzip2 -d data6.bin
    tar xvf data6.bin.out
    mv data8.bin data8.gz
    gunzip data8.gz
    cat data8

---

## 🔑 Level 13 → 14

**Goal:** Use a private SSH key instead of a password.

**Details:** SSH keys are safer than passwords. This level teaches permission control (`chmod 600`) and key-based auth.

**Solution:**
    chmod 600 sshkey.private
    ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220

---

## 🌐 Level 14 → 15

**Goal:** Send the password to a port using `netcat`.

**Details:** Learn to send data to services via local ports.

**Solution:**
    echo [password] | nc localhost 30000

---

## 📶 Level 15 → 16

**Goal:** Use SSL client to send the password securely.

**Details:** Introduces OpenSSL and sending secure messages to servers.

**Solution:**
    openssl s_client -connect localhost:30001 -quiet < /etc/bandit_pass/bandit15

---

## 🛠️ Level 16 → 17

**Goal:** Scan ports and use OpenSSL with a returned key.

**Details:** Combine port scanning (`nmap`), OpenSSL, file permissions, and SSH login.

**Solution:**
    nmap -p 31000-32000 localhost
    cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:[found-port] -quiet > /tmp/key/akey
    chmod 600 /tmp/key/akey
    ssh -i /tmp/key/akey bandit17@localhost

---

## 🧾 Level 17 → 18

**Goal:** Compare two versions of a password file.

**Details:** Introduces `diff`, a simple and powerful tool to spot changes between files.

**Solution:**
    diff passwords.old passwords.new

---

## ⚡ Level 18 → 19

**Goal:** Automatically read a file before the shell logs you out.

**Details:** The shell logs out immediately, so we run the `cat` inline with `ssh`.

**Solution:**
    ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme

---

## 🔧 Level 19 → 20

**Goal:** Exploit a SUID binary to read another user’s password file.

**Details:** Learn how `setuid` works — it allows a binary to run as its owner (bandit20), so we can temporarily become that user.

**Solution:**
    ./bandit20-do cat /etc/bandit_pass/bandit20

---

