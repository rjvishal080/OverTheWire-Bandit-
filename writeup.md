# OverTheWire: Bandit Walkthrough (Level 0 to Level 20)

This is a detailed walkthrough for the Bandit Wargame hosted on OverTheWire. It is aimed at absolute beginners and includes explanation for every command used.

---

## Level 0 → Level 1

**Objective**: SSH into the machine using the given credentials and find the password for the next level.

**Credentials**:
- **Username**: `bandit0`
- **Password**: `bandit0`
- **Host**: `bandit.labs.overthewire.org`
- **Port**: `2220`

**Command**:
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

This connects to the Bandit server using SSH with the username `bandit0` and port `2220`.

Once logged in, list files:
```bash
ls
```

You'll see a file called `README`. Display its content:
```bash
cat README
```

This file contains the password for the next level.

---

## Level 1 → Level 2

**Objective**: Read the contents of a file with a tricky filename: `-`

List the files:
```bash
ls
```

Use `cat` with a relative path to avoid confusion with `-`:
```bash
cat ./-
```

This outputs the password for Level 2.

---

## Level 2 → Level 3

**Objective**: Read a file with spaces in its filename.

List the files:
```bash
ls
```

You’ll see a file named `spaces in this filename`. Enclose it in quotes:
```bash
cat "spaces in this filename"
```

---

## Level 3 → Level 4

**Objective**: Find and read a hidden file.

List the contents:
```bash
ls
```

Enter the `inhere` directory:
```bash
cd inhere
```

List all files including hidden ones:
```bash
ls -la
```

Display contents of the hidden file:
```bash
cat .hidden
```

---

## Level 4 → Level 5

**Objective**: Read a human-readable file from a group of files.

Navigate and list files:
```bash
cd inhere
ls
```

Find the readable ASCII file. Use:
```bash
cat ./-file07
```

---

## Level 5 → Level 6

**Objective**: Find a file with a specific size (1033 bytes) and not executable.

Commands:
```bash
cd inhere
find . -size 1033c ! -executable
cat ./maybehere07/.file2
```

- `find` searches for files of exact size (`1033c` = 1033 bytes) and not executable.
- `cat` reads the file with the password.

---

## Level 6 → Level 7

**Objective**: Find a file owned by `bandit7`, group `bandit6`, and of size 33 bytes anywhere on the system.

Command:
```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

- `-type f`: look for files
- `-user bandit7`: owned by user
- `-group bandit6`: owned by group
- `-size 33c`: size is 33 bytes
- `2>/dev/null`: suppress permission errors

Read the file once found:
```bash
cat /path/to/found/file
```

---

## Level 7 → Level 8

**Objective**: Find a line containing the word "millionth".

```bash
cat data.txt | grep millionth
```

---

## Level 8 → Level 9

**Objective**: Find the unique line that appears only once.

```bash
cat data.txt | sort | uniq -u
```

- `sort` organizes lines
- `uniq -u` filters lines that appear only once

---

## Level 9 → Level 10

**Objective**: Find lines that contain the equal sign `=`.

```bash
cat data.txt | grep "="
```

---

## Level 10 → Level 11

**Objective**: Decode base64 encoded text.

```bash
base64 -d data.txt
```

- `-d`: decode the content

---

## Level 11 → Level 12

**Objective**: Decode a ROT13 cipher.

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

- `tr`: translate characters
- This shifts each letter by 13 places

---

## Level 12 → Level 13

**Objective**: Extract the password hidden in a multi-level compressed file.

```bash
mkdir /tmp/bandana
cp data.txt /tmp/bandana
cd /tmp/bandana
xxd -r data.txt > bandit
file bandit
mv bandit bandit.gz
gunzip bandit.gz
file bandit
bzip2 -d bandit
file bandit.out
mv bandit.out bandit.gz
gunzip bandit.gz
file bandit
tar xvf bandit
file data5.bin
tar xvf data5.bin
file data6.bin
bzip2 -d data6.bin
file data6.bin.out
tar xvf data6.bin.out
file data8.bin
mv data8.bin data8.gz
gunzip data8.gz
file data8
cat data8
```

---

## Level 13 → Level 14

**Objective**: Use an SSH private key to login.

Download and save the private key, then run:
```bash
chmod 600 sshkey.private
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

---

## Level 14 → Level 15

**Objective**: Submit the password via netcat to a local service.

```bash
echo <password> | nc localhost 30000
```

---

## Level 15 → Level 16

**Objective**: Connect to an SSL port and submit the password.

```bash
openssl s_client -connect localhost:30001 -quiet < /etc/bandit_pass/bandit15
```

---

## Level 16 → Level 17

**Objective**: Port scan and use correct one to fetch private key.

```bash
nmap -p 31000-32000 localhost
cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:<correct_port> -quiet > /tmp/key/akey
chmod 600 /tmp/key/akey
ssh -i /tmp/key/akey bandit17@localhost -p 2220
```

---

## Level 17 → Level 18

**Objective**: Compare two files.

```bash
ls -la
diff passwords.old passwords.new
```

---

## Level 18 → Level 19

**Objective**: Display file content before session closes.

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```

---

## Level 19 → Level 20

**Objective**: Run a program as another user using setuid.

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

---

✅ **Completed: Bandit Levels 0–20**

