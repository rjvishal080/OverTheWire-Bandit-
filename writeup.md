# OverTheWire: Bandit Write-up (Levels 0-20)

> **Purpose**: This write-up covers Bandit levels 0–20 from OverTheWire with detailed explanations for every command used. Ideal for beginners learning Linux, SSH, and basic security concepts.

---

## ⚔️ Level 0 → 1
**Command:**
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```
**Explanation:** Securely connects to the remote machine using SSH as `bandit0` user on port `2220`.

```bash
ls
cat README
```
- Lists files and prints the content of `README`, which contains the password.

---

## 🧾 Level 1 → 2
```bash
ls
cat ./-
```
- The filename is `-`. We use `./` to reference it as a regular file.

---

## 📁 Level 2 → 3
```bash
ls
cat "spaces in this filename"
```
- Quotes are used to handle filenames with spaces.

---

## 🔍 Level 3 → 4
```bash
cd inhere
ls -la
cat .hidden
```
- Navigates to `inhere`, lists all files including hidden ones, and reads `.hidden`.

---

## 🧱 Level 4 → 5
```bash
cd inhere
cat ./-file07
```
- File name starts with `-`, so we prefix with `./` to read it.

---

## 🧩 Level 5 → 6
```bash
cd inhere
find . -size 1033c ! -executable
cat ./maybehere07/.file2
```
- Finds a 1033-byte non-executable file and reads it.

---

## 🕵️ Level 6 → 7
```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /path/to/file
```
- Searches from root for file owned by `bandit7`, group `bandit6`, 33 bytes in size.

---

## 📄 Level 7 → 8
```bash
cat data.txt | grep millionth
```
- Prints the line containing `millionth`.

---

## 🔍 Level 8 → 9
```bash
cat data.txt | sort | uniq -u
```
- Sorts and finds unique line (appears once only).

---

## 🧪 Level 9 → 10
```bash
cat data.txt | strings | grep "=="
```
- `strings` filters printable characters; `grep` finds Base64 pattern.

---

## 🔐 Level 10 → 11
```bash
base64 -d data.txt
```
- Decodes a Base64-encoded file.

---

## 🔄 Level 11 → 12
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
- Decodes ROT13 (shifts each letter by 13).

---

## 📦 Level 12 → 13
```bash
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
```
- Multiple steps to decode/decompress layers and extract password.

---

## 🔑 Level 13 → 14
```bash
chmod 600 sshkey.private
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```
- Uses private key for SSH authentication.

---

## 🌐 Level 14 → 15
```bash
echo [password] | nc localhost 30000
```
- Sends password to a TCP service using Netcat.

---

## 📶 Level 15 → 16
```bash
openssl s_client -connect localhost:30001 -quiet < /etc/bandit_pass/bandit15
```
- Sends password over SSL connection using `openssl`.

---

## 🛠️ Level 16 → 17
```bash
nmap -p 31000-32000 localhost
```
- Scans ports to find the one with the service.

```bash
cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:31790 -quiet > /tmp/key
chmod 600 /tmp/key
ssh -i /tmp/key bandit17@localhost
```
- Sends password, receives key, logs into next level.

---

## 🧾 Level 17 → 18
```bash
diff passwords.old passwords.new
```
- Compares files to find modified line (new password).

---

## ⚡ Level 18 → 19
```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```
- Reads `readme` directly during login because normal shell logs out.

---

## 🔧 Level 19 → 20
```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```
- Executes command as bandit20 via setuid binary.

---

> **Next:** Want the next levels (21–34) or gamified One Piece-style progression? Let me know!
