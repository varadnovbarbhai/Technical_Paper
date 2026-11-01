# Linux CLI Cheatsheet

## 1. Introduction to CLI

**CLI (Command Line Interface)** is a way to interact with an operating system by entering commands in a terminal.

### Important Terminology

| Term | Description |
|---|---|
| Terminal | Application used to access the command line. |
| Shell | Program that interprets and executes commands. |
| Bash | A popular Unix/Linux shell. |
| Kernel | Core component of an operating system that manages hardware and system resources. |
| Process | An instance of a running program. |
| PID | Process ID, a unique identifier assigned to a process. |
| Parent Process | Process that creates another process. |
| Child Process | Process created by another process. |
| Root User | Administrator account with unrestricted system privileges. |

---

# 2. Navigation Commands

## pwd – Print Working Directory

Displays the current working directory.

```bash
pwd
```

Example:

```bash
/home/varad
```

## cd – Change Directory

Used to navigate between directories.

```bash
cd /home/varad
```

### Important cd Shortcuts

| Command | Description |
|---|---|
| `cd` | Go to home directory. |
| `cd ~` | Go to home directory. |
| `cd /` | Go to root directory. |
| `cd .` | Current directory. |
| `cd ..` | Move one directory up. |
| `cd ../..` | Move two directories up. |
| `cd -` | Return to previous working directory. |
| `cd ~/Downloads` | Go to Downloads directory inside home. |

### Absolute vs Relative Paths

**Absolute Path:**
- Complete path starting from the root directory `/`.
- Does not depend on the current working directory.

Example:

```bash
cd /home/varad/Documents
```

**Relative Path:**
- Path specified relative to the current working directory.
- Does not start with `/`.

Example:

```bash
cd Documents
cd ../Downloads
```

---

# 3. File and Directory Management

## mkdir – Make Directory

Creates directories.

```bash
mkdir folder1
```

Create multiple directories:

```bash
mkdir folder1 folder2 folder3
```

Create nested directories:

```bash
mkdir -p folder1/folder2/folder3
```

`-p` creates parent directories if they do not exist.

## touch – Create File

Creates an empty file or updates its timestamp if it already exists.

```bash
touch a.txt
```

Create multiple files:

```bash
touch a.txt b.txt c.txt
```

## cp – Copy Files and Directories

Copy a file:

```bash
cp a.txt b.txt
```

Copy a file into another directory:

```bash
cp a.txt folder1/
```

Copy a directory recursively:

```bash
cp -r folder1 folder2
```

Important flags:

| Flag | Description |
|---|---|
| `-r` | Copy directories recursively. |
| `-i` | Ask before overwriting. |
| `-v` | Display copied files. |

## mv – Move or Rename

Rename a file:

```bash
mv old.txt new.txt
```

Move a file:

```bash
mv a.txt folder1/
```

Move multiple files:

```bash
mv a.txt b.txt folder1/
```

Rename a directory:

```bash
mv old_folder new_folder
```

## rm – Remove Files and Directories

Remove a file:

```bash
rm a.txt
```

Remove multiple files:

```bash
rm a.txt b.txt
```

Remove a directory recursively:

```bash
rm -r folder1
```

Forcefully remove files:

```bash
rm -f a.txt
```

Forcefully remove a directory recursively:

```bash
rm -rf folder1
```

**Important:** `rm -rf` permanently removes files without asking for confirmation. Use carefully.

## tree – Display Directory Structure

Displays files and folders in a tree format.

```bash
tree
```

Display hidden files:

```bash
tree -a
```

Install tree:

```bash
sudo apt update
sudo apt install tree
```

---

# 4. Listing Files – ls

Displays files and directories.

```bash
ls
```

### Five Important ls Flags

| Command | Description |
|---|---|
| `ls -a` | Display hidden files. |
| `ls -l` | Long listing format with permissions, owner, size and date. |
| `ls -t` | Sort files by modification time (newest first). |
| `ls -r` | Reverse sorting order. |
| `ls -h` | Display file sizes in human-readable format (when used with `-l`). |

### Combining Flags

Display hidden files:

```bash
ls -a
```

Display file details:

```bash
ls -l
```

Display human-readable file sizes:

```bash
ls -lh
```

Display hidden files, sorted by modification time in reverse order, with human-readable sizes:

```bash
ls -lathr
```

Alternative:

```bash
ls -alhtr
```

---

# 5. Reading Files

## cat – Concatenate and Display

Display file contents:

```bash
cat a.txt
```

Display multiple files:

```bash
cat a.txt b.txt
```

Create a file using cat:

```bash
cat > a.txt
```

Append content:

```bash
cat >> a.txt
```

Press `Ctrl + D` to finish input.

## less – Read Large Files

```bash
less a.txt
```

Useful navigation:

| Key | Action |
|---|---|
| `Space` | Next page |
| `b` | Previous page |
| `/word` | Search forward |
| `?word` | Search backward |
| `n` | Next search result |
| `q` | Quit |

## more – Read Files Page by Page

```bash
more a.txt
```

Useful for viewing large files one screen at a time.

## head – Display First Lines

Display first 10 lines:

```bash
head a.txt
```

Display first 20 lines:

```bash
head -n 20 a.txt
```

## tail – Display Last Lines

Display last 10 lines:

```bash
tail a.txt
```

Display last 30 lines:

```bash
tail -n 30 a.txt
```

Continuously monitor a file:

```bash
tail -f application.log
```

---

# 6. File Permissions – chmod

Linux permissions control who can read, write and execute files.

There are three permission categories:

| Category | Meaning |
|---|---|
| User (u) | File owner |
| Group (g) | Users belonging to the file's group |
| Others (o) | Everyone else |

### Three Permission Types

| Permission | Symbol | Numerical Value |
|---|---|---|
| Read | r | 4 |
| Write | w | 2 |
| Execute | x | 1 |
| No permission | - | 0 |

### Understanding Numerical Permissions

Permissions are calculated by adding the numerical values.

| Permission | Calculation | Value |
|---|---|---|
| --- | 0 | 0 |
| --x | 1 | 1 |
| -w- | 2 | 2 |
| -wx | 2+1 | 3 |
| r-- | 4 | 4 |
| r-x | 4+1 | 5 |
| rw- | 4+2 | 6 |
| rwx | 4+2+1 | 7 |

### Understanding 755

```bash
chmod 755 a.txt
```

755 means:

- Owner = 7 = rwx
- Group = 5 = r-x
- Others = 5 = r-x

Therefore:

```text
rwxr-xr-x
```

### Understanding Binary Conversion

Each permission uses three binary bits:

| Permission | Binary | Decimal |
|---|---|---|
| Read | 100 | 4 |
| Write | 010 | 2 |
| Execute | 001 | 1 |
| Read + Execute | 101 | 5 |
| Read + Write | 110 | 6 |
| Read + Write + Execute | 111 | 7 |

Example:

```text
755

7 = 111
5 = 101
5 = 101

755 = 111 101 101
```

### Important chmod Commands

Change permissions numerically:

```bash
chmod 755 a.txt
```

Give everyone read permission:

```bash
chmod a+r a.txt
```

Give the owner write permission:

```bash
chmod u+w a.txt
```

Remove write permission from others:

```bash
chmod o-w a.txt
```

Give execute permission to everyone:

```bash
chmod a+x a.txt
```

Recursively change permissions:

```bash
chmod -R 755 folder1
```

Check permissions:

```bash
ls -l a.txt
```

Example output:

```text
-rwxr-xr-x 1 varad varad 100 Nov 1 10:00 a.txt
```

The first character represents the file type:

- `-` = Regular file
- `d` = Directory
- `l` = Symbolic link

The next nine characters represent permissions.

**Important:** Execute permission on a directory allows users to enter/traverse it. Read permission allows listing its contents.

---

# 7. File Ownership – chown

`chown` stands for Change Owner.

It changes the ownership of files and directories.

Check ownership:

```bash
ls -l
```

Change owner:

```bash
sudo chown username a.txt
```

Change owner and group:

```bash
sudo chown username:groupname a.txt
```

Change only group:

```bash
sudo chown :groupname a.txt
```

Change ownership recursively:

```bash
sudo chown -R username:groupname folder1
```

Example:

```bash
sudo chown varad:varad a.txt
```

### chmod vs chown

| Command | Purpose |
|---|---|
| chmod | Changes file permissions. |
| chown | Changes file ownership. |

---

# 8. sudo – Superuser Do

Allows an authorized user to execute commands with elevated privileges.

Example:

```bash
sudo apt update
```

Run a command as another user:

```bash
sudo -u username command
```

Open a root shell:

```bash
sudo -i
```

**Important:** Use sudo carefully because it provides elevated system privileges.

---

# 9. Package Management – apt

`apt` is the package management tool used in Debian-based Linux distributions such as Ubuntu.

Update package information:

```bash
sudo apt update
```

Upgrade installed packages:

```bash
sudo apt upgrade
```

Install a package:

```bash
sudo apt install tree
```

Remove a package:

```bash
sudo apt remove tree
```

Remove package and its configuration files:

```bash
sudo apt purge tree
```

Search for a package:

```bash
apt search package_name
```

Display installed package information:

```bash
apt show package_name
```

---

# 10. Searching Files and Directories – find

`find` searches for files and directories based on specified conditions.

Find a file by name:

```bash
find /home/varad -name "a.txt"
```

Find directories:

```bash
find . -type d
```

Find files:

```bash
find . -type f
```

Find files with a particular extension:

```bash
find . -name "*.txt"
```

Find files containing a particular word in their filename:

```bash
find /home/varad -name "*java*"
```

Case-insensitive search:

```bash
find . -iname "*java*"
```

Find files modified within the last 7 days:

```bash
find . -mtime -7
```

Find files larger than 100 MB:

```bash
find . -size +100M
```

Find and delete files:

```bash
find . -name "*.tmp" -delete
```

Find files and execute a command:

```bash
find . -name "*.txt" -exec ls -l {} \;
```

### Important find Options

| Option | Description |
|---|---|
| `-name` | Search by filename. |
| `-iname` | Case-insensitive filename search. |
| `-type f` | Find regular files. |
| `-type d` | Find directories. |
| `-mtime` | Search based on modification time. |
| `-size` | Search based on file size. |
| `-exec` | Execute a command on matching results. |
| `-delete` | Delete matching files. |

**Remember:** `find` searches filenames and directory names. It does not search inside file contents.

---

# 11. Text Searching – grep

`grep` searches for a particular pattern or word inside files.

Search for a word:

```bash
grep "java" a.txt
```

Search across multiple files:

```bash
grep "java" *.txt
```

Case-insensitive search:

```bash
grep -i "java" a.txt
```

Display line numbers:

```bash
grep -n "java" a.txt
```

Count matching lines:

```bash
grep -c "java" a.txt
```

Search recursively inside directories:

```bash
grep -r "java" folder1/
```

Display lines that do not contain a word:

```bash
grep -v "java" a.txt
```

Search for whole words only:

```bash
grep -w "java" a.txt
```

---

# 12. Text Processing – wc, sort, sed and awk

## wc – Word Count

Count lines:

```bash
wc -l a.txt
```

Count words:

```bash
wc -w a.txt
```

Count characters:

```bash
wc -m a.txt
```

Count bytes:

```bash
wc -c a.txt
```

Count words in a particular file:

```bash
grep -o -w "Harry" harry_potter.txt | wc -l
```

Here:

- `grep -o` prints each matching occurrence separately.
- `-w` matches whole words.
- `wc -l` counts the matching occurrences.

## sort – Sort Lines

Sort alphabetically:

```bash
sort a.txt
```

Reverse sorting:

```bash
sort -r a.txt
```

Numerical sorting:

```bash
sort -n numbers.txt
```

Sort and remove duplicate lines:

```bash
sort -u a.txt
```

## sed – Stream Editor

Used to search, replace, delete and modify text.

Display a particular line:

```bash
sed -n '5p' a.txt
```

Display lines 1 to 10:

```bash
sed -n '1,10p' a.txt
```

Replace the first occurrence of a word on each line:

```bash
sed 's/java/python/' a.txt
```

Replace all occurrences on each line:

```bash
sed 's/java/python/g' a.txt
```

Modify the original file:

```bash
sed -i 's/java/python/g' a.txt
```

Delete a particular line:

```bash
sed '5d' a.txt
```

**Important:** `sed` normally prints modified output without changing the original file. Use `-i` to edit the file directly.

## awk – Text Processing

`awk` processes text using fields and patterns.

Print entire file:

```bash
awk '{print}' a.txt
```

Print first column:

```bash
awk '{print $1}' a.txt
```

Print second column:

```bash
awk '{print $2}' a.txt
```

Print first and third columns:

```bash
awk '{print $1, $3}' a.txt
```

Print line numbers:

```bash
awk '{print NR, $0}' a.txt
```

Print lines containing a particular word:

```bash
awk '/java/ {print}' a.txt
```

Calculate the sum of values in the second column:

```bash
awk '{sum += $2} END {print sum}' numbers.txt
```

### Important awk Variables

| Variable | Description |
|---|---|
| `$0` | Entire current line. |
| `$1` | First field. |
| `$2` | Second field. |
| `$NF` | Last field. |
| `NR` | Current record/line number. |
| `NF` | Number of fields in current record. |

---

# 13. Pipes and Redirection

## Pipe Operator – |

The pipe operator passes the output of one command as input to another command.

Example:

```bash
ls -l | grep ".txt"
```

Here:
1. `ls -l` lists files.
2. `grep ".txt"` filters the output.
3. The final output displays matching lines.

More examples:

```bash
ps aux | grep firefox
```

```bash
cat a.txt | grep "java"
```

```bash
ls -l | wc -l
```

```bash
ps aux | sort -k 3 -nr
```

### Output Redirection

Save output to a file:

```bash
ls > output.txt
```

Append output:

```bash
ls >> output.txt
```

Redirect errors:

```bash
command 2> error.txt
```

Redirect both standard output and errors:

```bash
command > output.txt 2>&1
```

---

# 14. xargs – Build and Execute Commands

`xargs` takes input from standard input and passes it as arguments to another command.

Example:

```bash
echo "a.txt b.txt" | xargs rm
```

Find and remove temporary files:

```bash
find . -name "*.tmp" | xargs rm
```

Safer version for filenames containing spaces:

```bash
find . -name "*.tmp" -print0 | xargs -0 rm
```

Example with echo:

```bash
echo "hello world" | xargs
```

**Important:** `xargs` is useful when you need to pass the output of one command as arguments to another command.

---

# 15. OS and Process Management

## ps – Process Status

Displays information about running processes.

Display processes associated with the current terminal:

```bash
ps
```

Display all processes:

```bash
ps -e
```

Display detailed information about all processes:

```bash
ps aux
```

Display process hierarchy:

```bash
ps -ef --forest
```

### Important ps Options

| Option | Description |
|---|---|
| `-e` | Select all processes. |
| `-f` | Full-format listing. |
| `-a` | Select processes associated with terminals. |
| `-u` | Display user-oriented information. |
| `aux` | Common BSD-style format displaying processes. |
| `--forest` | Display process hierarchy. |

### Find Firefox PID

```bash
ps aux | grep firefox
```

A cleaner approach:

```bash
pgrep -a firefox
```

Find only the PID:

```bash
pgrep firefox
```

## Parent and Child Processes

A parent process creates another process.

A child process is created by a parent process.

Important identifiers:

- PID = Process ID.
- PPID = Parent Process ID.

Display PID and PPID:

```bash
ps -eo pid,ppid,cmd
```

Display process hierarchy:

```bash
pstree -p
```

Display the parent process of a particular PID:

```bash
ps -o pid,ppid,cmd -p PID
```

Find the parent process:

```bash
ps -p PID -o ppid=
```

To trace the complete parent chain, repeatedly inspect the PPID until reaching PID 1 or another top-level process.

## top – Monitor Processes

Displays real-time system and process information.

```bash
top
```

Important shortcuts inside top:

| Key | Action |
|---|---|
| `q` | Quit |
| `P` | Sort by CPU usage |
| `M` | Sort by memory usage |
| `k` | Kill a process |
| `1` | Display individual CPU cores |

## kill – Terminate Processes

Terminate a process gracefully:

```bash
kill PID
```

Send a particular signal:

```bash
kill -SIGNAL PID
```

### Important Kill Signals

| Signal | Number | Description |
|---|---|---|
| SIGHUP | 1 | Hangup signal. |
| SIGINT | 2 | Interrupt signal. |
| SIGQUIT | 3 | Quit signal. |
| SIGKILL | 9 | Forcefully terminate a process. |
| SIGTERM | 15 | Request graceful termination. |
| SIGSTOP | 19 | Stop a process. |
| SIGCONT | 18 | Continue a stopped process. |

Examples:

```bash
kill -15 PID
```

```bash
kill -9 PID
```

**Difference between kill -9 and kill -15:**

- `kill -15` sends SIGTERM and allows the process to clean up and terminate gracefully.
- `kill -9` sends SIGKILL and forces immediate termination.
- SIGKILL cannot be caught, blocked or ignored by the process.

Always try SIGTERM first. Use SIGKILL only when necessary.

### Find and Kill Firefox

Find PID:

```bash
pgrep firefox
```

Terminate Firefox:

```bash
pkill firefox
```

Forcefully terminate:

```bash
pkill -9 firefox
```

Using pipes:

```bash
ps aux | grep '[f]irefox'
```

Extract PID:

```bash
ps aux | grep '[f]irefox' | awk '{print $2}'
```

Pass PID to kill:

```bash
ps aux | grep '[f]irefox' | awk '{print $2}' | xargs kill
```

**Note:** Prefer `pgrep` and `pkill` when possible because they avoid some common PID extraction mistakes.

---

# 16. Disk and System Information

## df – Disk Free

Displays available disk space.

```bash
df
```

Human-readable format:

```bash
df -h
```

Display filesystem types:

```bash
df -Th
```

## free – Memory Information

Displays RAM and swap memory usage.

```bash
free
```

Human-readable output:

```bash
free -h
```

## uname – System Information

Display kernel name:

```bash
uname
```

Display all available system information:

```bash
uname -a
```

Display kernel version:

```bash
uname -r
```

Display machine hardware architecture:

```bash
uname -m
```

Common architecture output:

```text
x86_64
```

This indicates a 64-bit x86 architecture.

## lspci – List PCI Devices

Displays information about PCI devices connected to the system.

```bash
lspci
```

Display detailed information:

```bash
lspci -v
```

Search for audio devices:

```bash
lspci | grep -i audio
```

Search for VGA/display devices:

```bash
lspci | grep -i vga
```

---

# 17. Networking Commands

## ping – Check Network Connectivity

Send packets to a host:

```bash
ping google.com
```

Send a limited number of packets:

```bash
ping -c 4 google.com
```

Stop continuous ping:

```bash
Ctrl + C
```

## ifconfig – Network Interface Configuration

Displays network interface information.

```bash
ifconfig
```

Display a specific interface:

```bash
ifconfig eth0
```

Modern Linux systems commonly use `ip` instead:

```bash
ip addr
```

Display network interfaces:

```bash
ip link
```

## ssh – Secure Shell

SSH is a network protocol that provides secure remote access to another computer over an encrypted connection.

Connect to a remote server:

```bash
ssh username@server_ip
```

Example:

```bash
ssh varad@192.168.1.100
```

Connect using a particular port:

```bash
ssh -p 2222 username@server_ip
```

Connect using a private key:

```bash
ssh -i ~/.ssh/id_ed25519 username@server_ip
```

### SSH Key Authentication

Generate SSH keys:

```bash
ssh-keygen -t ed25519
```

Copy public key to the remote server:

```bash
ssh-copy-id username@server_ip
```

Common SSH files:

```text
~/.ssh/id_ed25519       Private key
~/.ssh/id_ed25519.pub   Public key
~/.ssh/known_hosts      Known server fingerprints
~/.ssh/config           SSH client configuration
```

**Important:** Never share your private SSH key.

---

# 18. Bash Environment Commands

## printenv – Print Environment Variables

Display all environment variables:

```bash
printenv
```

Display a specific variable:

```bash
printenv HOME
```

Other useful variables:

```bash
echo $USER
echo $HOME
echo $PATH
echo $SHELL
```

| Variable | Description |
|---|---|
| `$USER` | Current username. |
| `$HOME` | Home directory. |
| `$PATH` | Directories searched for executable commands. |
| `$SHELL` | Default login shell. |
| `$PWD` | Current working directory. |

## date – Display Date and Time

Display current date and time:

```bash
date
```

Display date:

```bash
date +%Y-%m-%d
```

Display time:

```bash
date +%H:%M:%S
```

---

# 19. nano – Command Line Text Editor

Open or create a file:

```bash
nano a.txt
```

Important shortcuts:

| Shortcut | Action |
|---|---|
| Ctrl + O | Save file. |
| Enter | Confirm filename. |
| Ctrl + X | Exit nano. |
| Ctrl + K | Cut current line. |
| Ctrl + U | Paste cut text. |
| Ctrl + W | Search text. |
| Ctrl + G | Help. |

---

# 20. Wildcards and Special Characters

Wildcards help match filenames and patterns.

| Symbol | Meaning | Example |
|---|---|---|
| `*` | Matches zero or more characters. | `ls *.txt` |
| `?` | Matches exactly one character. | `ls file?.txt` |
| `~` | Represents home directory. | `cd ~/Documents` |
| `.` | Current directory. | `./script.sh` |
| `..` | Parent directory. | `cd ..` |
| `/` | Root directory/path separator. | `cd /home` |

Examples:

List all text files:

```bash
ls *.txt
```

List files with exactly one character before `.txt`:

```bash
ls ?.txt
```

List files starting with `test`:

```bash
ls test*
```

**Important:** `*` and `?` are shell wildcards. `.` and `..` are directory references, while `~` is a shell expansion for the home directory.

---

# 21. Terminal Control Codes and Shortcuts

These shortcuts help control command execution and terminal navigation.

| Shortcut | Description |
|---|---|
| Ctrl + C | Interrupt/terminate the foreground command. |
| Ctrl + Z | Suspend the foreground process. |
| Ctrl + D | Send EOF (End of File) to the terminal input. |
| Ctrl + R | Reverse search command history. |
| Ctrl + L | Clear the terminal screen. |
| Ctrl + A | Move cursor to beginning of line. |
| Ctrl + E | Move cursor to end of line. |
| Ctrl + U | Delete text before cursor. |
| Ctrl + K | Delete text after cursor. |
| Ctrl + W | Delete previous word. |
| Tab | Autocomplete commands and filenames. |
| Up Arrow | Previous command in history. |
| Down Arrow | Next command in history. |

### Ctrl + C vs Ctrl + Z

**Ctrl + C:**
- Sends SIGINT to the foreground process.
- Requests the process to stop.
- Usually terminates the command.

**Ctrl + Z:**
- Sends SIGTSTP to the foreground process.
- Suspends the process.
- Does not terminate it.

Manage suspended processes:

```bash
jobs
```

Resume in foreground:

```bash
fg
```

Resume in background:

```bash
bg
```

Run a command in the background:

```bash
command &
```

### Ctrl + R – Reverse Search

Search previously executed commands.

1. Press `Ctrl + R`.
2. Type a command or keyword.
3. The shell searches command history.
4. Press `Ctrl + R` again to find an older match.
5. Press Enter to execute the displayed command.
6. Press the right arrow to edit the displayed command before execution.

### Tab Autocompletion

Start typing a command or filename and press Tab.

Example:

```bash
cd Doc<Tab>
```

If there is only one matching directory, Bash completes the name.

If multiple matches exist, press Tab twice to display suggestions.

### Command History

Display previously executed commands:

```bash
history
```

Display the last 10 commands:

```bash
history 10
```

Execute a command by its history number:

```bash
!123
```

---

# 22. Important Practical Review Questions

## Question 1: Create a directory and file

Go to home directory:

```bash
cd ~
```

Create directory:

```bash
mkdir d1
```

Create file:

```bash
touch d1/a.txt
```

Check permissions:

```bash
ls -l d1/a.txt
```

## Question 2: Change file permissions to 755

```bash
chmod 755 d1/a.txt
```

Verify:

```bash
ls -l d1/a.txt
```

Expected permissions:

```text
-rwxr-xr-x
```

## Question 3: Create another directory and file

```bash
mkdir d2
touch d2/b.txt
```

Change permissions recursively:

```bash
chmod -R 755 d2
```

Verify:

```bash
ls -lR d2
```

## Question 4: Start Firefox

```bash
firefox
```

Alternatively, launch it in the background:

```bash
firefox &
```

## Question 5: List all running processes

```bash
ps aux
```

## Question 6: Find Firefox PID

```bash
pgrep -a firefox
```

## Question 7: Find Parent Process ID

```bash
ps -o pid,ppid,cmd -p PID
```

Replace PID with the actual process ID.

## Question 8: Terminate Firefox

```bash
pkill firefox
```

Or:

```bash
kill PID
```

## Question 9: Find Current Username

```bash
whoami
```

## Question 10: Find Current Group

```bash
id -gn
```

Display all groups:

```bash
groups
```

Display user and group IDs:

```bash
id
```

## Question 11: Find Computer Architecture

```bash
uname -m
```

Display complete system information:

```bash
uname -a
```

## Question 12: Find Audio Hardware

```bash
lspci | grep -i audio
```

## Question 13: Find filenames or directories containing java

```bash
find /home/varad -iname "*java*"
```

Search the entire system (may require elevated permissions):

```bash
sudo find / -iname "*java*" 2>/dev/null
```

This searches filenames and directory names, not file contents.

## Question 14: List all home directory files

Display hidden files, sorted by modification time in reverse order, with human-readable sizes:

```bash
ls -alhtr ~
```

## Question 15: Display last 30 lines of Harry Potter

```bash
tail -n 30 harry_potter.txt
```

## Question 16: Count occurrences of a particular word

Count occurrences of the whole word Harry:

```bash
grep -o -w "Harry" harry_potter.txt | wc -l
```

Search for a word:

```bash
grep -in "Harry" harry_potter.txt
```

---

# 23. Frequently Asked Conceptual Questions

### 1. Difference between Service and Application

**Application:**
- A software program designed to perform a particular task.
- Usually interacts directly with the user.
- Examples: Firefox, VS Code, LibreOffice.

**Service:**
- A background process that provides functionality to other applications or the operating system.
- Usually runs without direct user interaction.
- Examples: SSH service, cron service, networking service.

An application can also run as a background service.

### 2. What are Parent and Child Processes?

A parent process creates a child process.

Example:

When a terminal launches Firefox, the terminal or its shell may be the parent process, while Firefox runs as a child process.

The relationship can be inspected using:

```bash
ps -ef --forest
```

### 3. Why do we use kill -9?

`kill -9` sends SIGKILL, which forces a process to terminate immediately.

It is generally used when a process does not respond to normal termination requests.

Prefer:

```bash
kill PID
```

Before:

```bash
kill -9 PID
```

### 4. What is the difference between chmod and chown?

- `chmod`: Changes file permissions.
- `chown`: Changes file ownership.

Example:

```bash
chmod 755 a.txt
sudo chown varad:varad a.txt
```

### 5. What is the difference between Ctrl + C and Ctrl + Z?

- Ctrl + C interrupts the foreground process.
- Ctrl + Z suspends the foreground process.

### 6. What is the difference between Absolute and Relative Paths?

Absolute path starts from `/`.

Example:

```bash
/home/varad/Documents
```

Relative path starts from the current working directory.

Example:

```bash
Documents
```

### 7. What is the difference between find and grep?

- `find` searches for files and directories.
- `grep` searches for text patterns inside files.

Example:

```bash
find . -name "*.txt"
```

```bash
grep "hello" a.txt
```

### 8. What is the difference between Terminal and Shell?

- Terminal: Interface through which commands are entered.
- Shell: Program that interprets and executes commands.

Bash is an example of a shell.

---

# 24. Quick Command Revision

| Command | Purpose |
|---|---|
| `man` | Read command manual. |
| `pwd` | Display current directory. |
| `cd` | Change directory. |
| `mkdir` | Create directory. |
| `touch` | Create empty file. |
| `ls` | List files and directories. |
| `cp` | Copy files/directories. |
| `mv` | Move or rename files. |
| `rm` | Remove files/directories. |
| `cat` | Display file contents. |
| `less` | Read files page by page. |
| `more` | Read files page by page. |
| `head` | Display first lines. |
| `tail` | Display last lines. |
| `chmod` | Change permissions. |
| `chown` | Change ownership. |
| `sudo` | Execute commands with elevated privileges. |
| `apt` | Manage packages. |
| `find` | Search files and directories. |
| `grep` | Search text patterns. |
| `wc` | Count lines, words and bytes. |
| `sort` | Sort lines. |
| `sed` | Stream editor for text manipulation. |
| `awk` | Text processing and field extraction. |
| `xargs` | Convert input into command arguments. |
| `ps` | Display processes. |
| `top` | Monitor running processes. |
| `kill` | Send signals to processes. |
| `df` | Display disk usage. |
| `free` | Display memory usage. |
| `uname` | Display system information. |
| `lspci` | List PCI devices. |
| `ping` | Test network connectivity. |
| `ssh` | Secure remote connection. |
| `ifconfig` | Display/configure network interfaces. |
| `printenv` | Display environment variables. |
| `date` | Display date and time. |
| `tree` | Display directory tree. |
| `nano` | Terminal text editor. |
| `man` | Command documentation. |

---

# 25. Important Practice Commands

Try these combinations to improve your CLI skills.


# Find all Python files
find . -name "*.py"

# Find all text files
find . -name "*.txt"

# Search for a word recursively
grep -rn "python" .

# Count lines in a file
wc -l a.txt

# Count occurrences of a word
grep -o -w "python" a.txt | wc -l

# Display the last 20 lines
tail -n 20 a.txt

# Display hidden files
ls -la

# Display file sizes in human-readable format
ls -lh

# Display process hierarchy
ps -ef --forest

# Find Firefox PID
pgrep firefox

# Check disk space
df -h

# Check RAM usage
free -h

# Check system architecture
uname -m

# Find audio device
lspci | grep -i audio

# Find files modified in the last 24 hours
find . -mtime -1

# Find files larger than 50 MB
find . -size +50M

# Display command history
history

# Reverse search command history
Ctrl + R


