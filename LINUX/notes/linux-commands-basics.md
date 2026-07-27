---
title: "Linux Commands Basics"
date: 2026-04-09
tags: [study, linux, commands, cli, basics]
subject: "Linux Administration"
source: "Class Notes"
status: complete
---

# Linux Commands Basics

## Key Concepts
- Linux commands are case-sensitive.
- `.` means current directory.
- `..` means parent directory.
- `~` means home directory.
- Hidden files and directories usually start with `.`.
- `sudo` runs a command with administrator privileges.
- `man <command>` opens the manual page for a command.
- `stdin` means standard input, `stdout` means standard output, and `stderr` means standard error.

---

## Navigation Commands

### `pwd` - Print Working Directory

| Command | Meaning |
|---------|---------|
| `pwd` | Show the full path of the current directory |

### `cd` - Change Directory

| Command | Meaning |
|---------|---------|
| `cd folder` | Move into `folder` |
| `cd ..` | Move to the parent directory |
| `cd ~` | Go to the home directory |
| `cd -` | Return to the previous directory |
| `cd .` | Stay in the current directory |
| `cd /` | Go to the root directory |

### `ls` - List Files and Directories

| Command | Meaning |
|---------|---------|
| `ls` | Show files and folders |
| `ls -l` | Long listing format |
| `ls -a` | Show hidden files |
| `ls -la` | Long format with hidden files |
| `ls -lh` | Long listing with human-readable sizes |
| `ls -lt` | Sort by modification time |
| `ls -lS` | Sort by file size |
| `ls -li` | Show inode numbers |
| `ls -R` | Recursive listing |
| `ls -r` | Reverse the sorting order |
| `ls -A` | Show hidden files except `.` and `..` |
| `ls -s` | Show file size in blocks |
| `ls subdir/` | List contents of `subdir` |
| `ls -al subdir/` | Detailed listing of `subdir` |

> [!TIP]
> `ls -la` is a common combination because it shows detailed output and hidden files together.

---

## Environment Variables and Shell Info

### `echo` - Print Text or Variable Values

| Command | Meaning |
|---------|---------|
| `echo "Hello"` | Print text |
| `echo $SHELL` | Show current shell |
| `echo $HOME` | Show home directory |
| `echo $USER` | Show current user |
| `echo $PWD` | Show current working directory |
| `echo $OLDPWD` | Show previous working directory |
| `echo $PATH` | Show executable search path |
| `echo $$` | Show current shell process ID |

### `env` - Show Environment Variables

| Command | Meaning |
|---------|---------|
| `env` | Display all environment variables |

---

## Directory Management Commands

### `mkdir` - Make Directory

| Command | Meaning |
|---------|---------|
| `mkdir dirname` | Create one directory |
| `mkdir dir1 dir2 dir3` | Create multiple directories |
| `mkdir -p d1/d2/d3` | Create nested directories |
| `mkdir -p a/b a/c` | Create multiple nested paths |

> [!NOTE]
> `mkdir -p` creates parent directories automatically if they do not already exist.

### `rmdir` - Remove Empty Directory

| Command           | Meaning                           |
| ----------------- | --------------------------------- |
| `rmdir dirname`   | Remove an empty directory         |
| `rmdir dir1 dir2` | Remove multiple empty directories |

### `tree` - View Directory Structure

| Command        | Meaning                                       |
| -------------- | --------------------------------------------- |
| `tree`         | Show directory tree from the current location |
| `tree dirname` | Show the tree of `dirname`                    |
| `tree -a`      | Include hidden files                          |
| `tree -L 2`    | Limit output to 2 levels                      |

> [!NOTE]
> `tree` may not be installed by default on every Linux system.

---

## File Management Commands

### `touch` - Create or Update File Timestamp

| Command | Meaning |
|---------|---------|
| `touch file.txt` | Create an empty file if it does not exist |
| `touch f1.txt f2.txt f3.txt` | Create multiple empty files |
| `touch existing.txt` | Update the timestamp of an existing file |

### `cat` - Display or Write File Content

| Command | Meaning |
|---------|---------|
| `cat file.txt` | Display file contents |
| `cat f1.txt f2.txt` | Display multiple files |
| `cat > file.txt` | Write to a file and overwrite old content |
| `cat >> file.txt` | Append content to a file |
| `cat < file.txt` | Read input from a file |
| `cat` | Read from keyboard until end-of-input |
| `cat -n file.txt` | Show all lines with line numbers |
| `cat -b file.txt` | Show non-empty lines with line numbers |
| `cat -s file.txt` | Squeeze repeated blank lines |

> [!WARNING]
> `cat > file.txt` replaces the existing content of the file.

### `cp` - Copy Files and Directories

| Command | Meaning |
|---------|---------|
| `cp file.txt copy.txt` | Copy a file to a new file |
| `cp file.txt dir1` | Copy a file into a directory |
| `cp file.txt dir1/new.txt` | Copy and rename in one step |
| `cp -r dir1 copy` | Copy a directory recursively |
| `cp file.txt ~/Desktop` | Copy a file to another location |
| `cp -R folder ~/backup` | Copy a folder to another location |

### `mv` - Move or Rename Files and Directories

| Command                      | Meaning                             |
| ---------------------------- | ----------------------------------- |
| `mv file.txt move.txt`       | Rename a file                       |
| `mv file2.txt dir2`          | Move a file into a directory        |
| `mv dir1 dir`                | Rename a directory                  |
| `mv dir2 dir`                | Move one directory into another     |
| `mv file.txt ~/Desktop`      | Move a file to another location     |
| `mv oldname.txt newname.txt` | Rename a file in the same directory |

### `rename` - Rename Multiple Files

| Command | Meaning |
|---------|---------|
| `rename 's/.txt$/.html/' *.txt` | Rename all `.txt` files to `.html` |

### `ln` - Create Links

| Command | Meaning |
|---------|---------|
| `ln file1 file_hardlink` | Create a hard link |
| `ln -s file1 file_link` | Create a symbolic link |

### `mkfifo` - Create Named Pipe

| Command | Meaning |
|---------|---------|
| `mkfifo fifo` | Create a named pipe file |

### `rm` - Remove Files or Directories

| Command | Meaning |
|---------|---------|
| `rm file.txt` | Delete a file |
| `rm f1.txt f2.txt` | Delete multiple files |
| `rm *.txt` | Delete all `.txt` files in the current directory |
| `rm -i file.txt` | Ask before deleting |
| `rm -r dirname` | Delete a directory and its contents |
| `rm -rf dirname` | Force delete without confirmation |

> [!WARNING]
> `rm -rf` is dangerous because it permanently deletes files and folders without asking.

---

## Viewing and Inspecting File Content

### `head` - Show Beginning of File

| Command | Meaning |
|---------|---------|
| `head file.txt` | Show the first 10 lines |
| `head -5 file.txt` | Show the first 5 lines |
| `head -4 file.txt` | Show the first 4 lines |

### `tail` - Show End of File

| Command | Meaning |
|---------|---------|
| `tail file.txt` | Show the last 10 lines |
| `tail -7 file.txt` | Show the last 7 lines |
| `tail -2 file.txt` | Show the last 2 lines |

### `wc` - Word, Line, and Byte Count

| Command | Meaning |
|---------|---------|
| `wc file.txt` | Show line, word, and byte counts |
| `wc -l file.txt` | Show only line count |
| `wc -w file.txt` | Show only word count |
| `wc -c file.txt` | Show only byte count |
| `wc -m file.txt` | Show character count |

### `tac` - Reverse Line Order

| Command | Meaning |
|---------|---------|
| `tac file.txt` | Show lines in reverse order |

### `rev` - Reverse Characters in Each Line

| Command | Meaning |
|---------|---------|
| `rev file.txt` | Reverse the characters of each line |
| `rev < input.txt` | Reverse text read from a file |
| `rev > output.txt` | Save keyboard input after reversing it |

> [!NOTE]
> `cat -r` is not a standard Linux `cat` option. Use `tac` to reverse line order or `rev` to reverse characters.

---

## Sorting and Filtering Text

### `sort` - Sort Lines

| Command | Meaning |
|---------|---------|
| `sort file.txt` | Sort lines alphabetically |
| `sort -n file.txt` | Sort lines numerically |
| `sort file.txt > sorted.txt` | Save sorted output to another file |

### `uniq` - Remove Adjacent Duplicate Lines

| Command | Meaning |
|---------|---------|
| `uniq file.txt` | Remove consecutive duplicate lines |
| `sort file.txt \| uniq` | Sort first, then remove duplicates |

> [!NOTE]
> `uniq` only removes duplicate lines that are next to each other, so it is often used after `sort`.

---

## Redirection and Pipes

### Output Redirection

| Command | Meaning |
|---------|---------|
| `command > file.txt` | Save standard output to a file |
| `command >> file.txt` | Append standard output to a file |
| `command 1> file.txt` | Save standard output explicitly |
| `command 2> error.txt` | Save standard error to a file |
| `command > out.txt 2> err.txt` | Save output and errors separately |
| `command > all.txt 2>&1` | Save output and errors to the same file |

### Input Redirection

| Command | Meaning |
|---------|---------|
| `command < input.txt` | Read input from a file |
| `bc < input > output 2> error` | Read input, save output, and save errors |

### Pipes

| Command | Meaning |
|---------|---------|
| `sort numbers.txt \| uniq` | Send sorted output into `uniq` |
| `head -10 numbers.txt \| tail -5` | Show lines 6 to 10 from the first 10 lines |
| `echo "Hello SunBeam" \| tr " " "#"` | Replace spaces with `#` |

> [!NOTE]
> A pipe (`|`) sends the output of one command directly into another command.

---

## Text Processing Commands

### `tr` - Translate or Squeeze Characters

| Command | Meaning |
|---------|---------|
| `echo "Hello SunBeam" \| tr " " "#"` | Replace spaces with `#` |
| `echo "Hello SunBeam" \| tr "a-z" "A-Z"` | Convert lowercase to uppercase |
| `echo "Hello SunBeam" \| tr "A-Z" "a-z"` | Convert uppercase to lowercase |
| `echo "Hello        SunBeam" \| tr -s " "` | Squeeze repeated spaces into one |
| `echo "Hello        SunBeam" \| tr -s " l"` | Squeeze repeated spaces and `l` |

### `cut` - Extract Fields

| Command | Meaning |
|---------|---------|
| `echo "itiss esd mc ac bda" \| cut -d " " -f1` | Show field 1 |
| `echo "itiss esd mc ac bda" \| cut -d " " -f3` | Show field 3 |
| `echo "itiss esd mc ac bda" \| cut -d " " -f3,4` | Show fields 3 and 4 |
| `echo "itiss esd mc ac bda" \| cut -d " " -f2-4` | Show fields 2 through 4 |
| `cut -d "," -f2 students.csv` | Show column 2 from CSV |
| `cut -d "," -f4 students.csv` | Show column 4 from CSV |
| `cut -d "," -f5 students.csv` | Show column 5 from CSV |

---

## Search Commands

### `find` - Search Files and Directories

| Command | Meaning |
|---------|---------|
| `find .` | Search from the current directory |
| `find . -type f` | Find only files |
| `find . -type d` | Find only directories |
| `find . -type p` | Find named pipes |
| `find /boot -type l` | Find symbolic links |
| `find . -name "file.txt"` | Find by exact name |
| `find . -size +4k` | Find files larger than 4 KB |
| `find . -size -4k` | Find files smaller than 4 KB |
| `find . -size 100c` | Find files of 100 bytes |
| `find . -mtime 1` | Find files modified 1 day ago |
| `find . -type f > all_students.txt` | Save the list of files to a file |

> [!NOTE]
> `find` is useful for searching deep directory structures.

---

## Calculator Command

### `bc` - Basic Calculator

| Command                        | Meaning                            |
| ------------------------------ | ---------------------------------- |
| `bc`                           | Open the calculator interactively  |
| `bc < input`                   | Read expressions from a file       |
| `bc < input > output 2> error` | Save calculation output and errors |

### `factor` - Prime Factorization

| Command | Meaning |
|---------|---------|
| `factor 24` | Show the prime factors of `24` |
| `factor 100` | Show the prime factors of `100` |

---

## System and Utility Commands

### `vim` - Text Editor

| Command | Meaning |
|---------|---------|
| `vim file.txt` | Open a file in the Vim editor |

### `uname` - System Information

| Command | Meaning |
|---------|---------|
| `uname` | Show basic system information |
| `uname -a` | Show all available system information |

### `hostname` - Host Name

| Command | Meaning |
|---------|---------|
| `hostname` | Show the system host name |

### `date` - Current Date and Time

| Command | Meaning |
|---------|---------|
| `date` | Show the current date and time |

### `cal` - Calendar

| Command | Meaning |
|---------|---------|
| `cal` | Show the current month's calendar |
| `cal 2026` | Show the full calendar for a year |

### `ps` - Process Status

| Command | Meaning |
|---------|---------|
| `ps` | Show processes of the current shell |
| `ps -ef` | Show all running processes in full format |
| `ps -e` | Show all running processes |
| `ps -e -o pid,cmd` | Show process ID and command |
| `ps -e -o pid,ppid,cmd` | Show process ID, parent ID, and command |

### `kill` - Stop a Process

| Command | Meaning |
|---------|---------|
| `kill 1234` | Send the default termination signal to process `1234` |
| `kill -9 1234` | Force stop process `1234` |

### `whoami` - Current User

| Command | Meaning |
|---------|---------|
| `whoami` | Show the current logged-in user |

### `tty` - Terminal Name

| Command | Meaning |
|---------|---------|
| `tty` | Show the terminal device name |

### `who` - Logged-in Users

| Command | Meaning |
|---------|---------|
| `who` | Show logged-in users |
| `who am i` | Show information about the current session |

### `users` - User Names

| Command | Meaning |
|---------|---------|
| `users` | Show logged-in user names |

### `reboot` - Restart System

| Command | Meaning |
|---------|---------|
| `reboot` | Restart the system |
| `init 6` | Reboot using init |

### `poweroff` - Shut Down System

| Command | Meaning |
|---------|---------|
| `poweroff` | Shut down the system |
| `init 0` | Power off using init |

### `alias` - Create Command Shortcuts

| Command | Meaning |
|---------|---------|
| `alias ll='ls -la'` | Create a shortcut command |
| `alias` | Show current aliases |

### `unalias` - Remove Aliases

| Command | Meaning |
|---------|---------|
| `unalias ll` | Remove the alias named `ll` |

### `stat` - File Information

| Command | Meaning |
|---------|---------|
| `stat file.txt` | Show detailed file information |
| `stat file.txt -c %y` | Show last modification time |
| `stat file.txt -c %h` | Show hard link count |
| `stat file.txt -c "%F %A"` | Show file type and permissions |


### `man` - Manual Pages

| Command | Meaning |
|---------|---------|
| `man` | Open the manual system help overview |
| `man ls` | Open the manual page for `ls` |
| `man mkdir` | Open the manual page for `mkdir` |
| `man 2 mkdir` | Open section 2 for `mkdir` |
| `man 3 printf` | Open section 3 for `printf` |

Common man page sections:
- `1` User commands
- `2` System calls
- `3` Library functions
- `5` File formats
- `8` Administrative commands

### `history` - Command History

| Command | Meaning |
|---------|---------|
| `history` | Show previously used commands |

### `sudo` - Run as Administrator

| Command | Meaning |
|---------|---------|
| `sudo <command>` | Run a command with elevated privileges |

---

## Grouped Commands and Common Flags

### Listing and Navigation

| Command | Purpose |
|---------|---------|
| `pwd` | Show current path |
| `ls -la` | Detailed list including hidden files |
| `ls -a` | Show hidden files |
| `ls -A` | Show hidden files except `.` and `..` |
| `ls -lh` | Show human-readable sizes |
| `ls -r` | Reverse sort order |
| `cd ..` | Go up one level |
| `cd ~` | Go to the home directory |
| `cd -` | Return to the previous location |

### Environment and Shell

| Command | Purpose |
|---------|---------|
| `echo $HOME` | Show home directory |
| `echo $PATH` | Show executable search path |
| `env` | Show all environment variables |
| `echo $$` | Show shell process ID |

### File and Directory Operations

| Command | Purpose |
|---------|---------|
| `mkdir -p a/b/c` | Create nested directories |
| `touch file.txt` | Create an empty file |
| `cp file.txt copy.txt` | Copy a file |
| `cp -R dir1 backup` | Copy a directory |
| `mv file.txt new.txt` | Rename or move a file |
| `ln -s file1 link1` | Create a symbolic link |
| `mkfifo fifo` | Create a named pipe |
| `rm -r dirname` | Remove a non-empty directory |

### Viewing and Processing Text

| Command | Purpose |
|---------|---------|
| `cat file.txt` | Show file content |
| `cat -n file.txt` | Show line numbers |
| `cat -b file.txt` | Number non-empty lines |
| `cat -s file.txt` | Squeeze blank lines |
| `head -5 file.txt` | Show first 5 lines |
| `head -5 file.txt \| tail -3` | Show lines 3 to 5 |
| `tail -7 file.txt` | Show last 7 lines |
| `wc file.txt` | Count lines, words, and bytes |
| `wc -m file.txt` | Count characters |
| `sort -n numbers.txt` | Sort numbers numerically |
| `sort numbers.txt \| uniq` | Sort and remove duplicates |
| `tac file.txt` | Reverse line order |
| `rev file.txt` | Reverse characters in each line |
| `tr -s " "` | Squeeze repeated spaces |
| `cut -d "," -f2 students.csv` | Extract a CSV column |
| `find . -type f` | Find files recursively |

### System and Shell

| Command | Purpose |
|---------|---------|
| `uname -a` | Show system details |
| `hostname` | Show host name |
| `date` | Show date and time |
| `cal` | Show calendar |
| `ps -ef` | List running processes |
| `kill 1234` | Stop a process |
| `whoami` | Show current user |
| `who` | Show logged-in users |
| `users` | Show user names |
| `tty` | Show terminal name |
| `stat file.txt` | Show file details |
| `chmod 755 script.sh` | Change permissions |
| `chown user:group file.txt` | Change ownership |
| `vim file.txt` | Open a text editor |
| `alias ll='ls -la'` | Create a shortcut |
| `unalias ll` | Remove a shortcut |
| `factor 24` | Show prime factors |
| `man ls` | Open command help |

### Redirection and Pipes

| Command | Purpose |
|---------|---------|
| `command > out.txt` | Save output to a file |
| `command 2> err.txt` | Save errors to a file |
| `command > all.txt 2>&1` | Save output and errors together |
| `command < input.txt` | Read input from a file |
| `command1 \| command2` | Pass output to another command |

---

## Quick Reference

| Task | Command |
|------|---------|
| Show current directory | `pwd` |
| Show home directory | `echo $HOME` |
| Show shell | `echo $SHELL` |
| Show environment variables | `env` |
| List files | `ls` |
| Change directory | `cd <dir>` |
| Create directory | `mkdir dirname` |
| Create nested directories | `mkdir -p a/b/c` |
| Create file | `touch file.txt` |
| Read file | `cat file.txt` |
| Copy file | `cp source.txt dest.txt` |
| Copy directory | `cp -R source_dir dest_dir` |
| Move or rename file | `mv old.txt new.txt` |
| Create link | `ln -s source link_name` |
| Create named pipe | `mkfifo fifo` |
| Find files | `find . -type f` |
| Count lines and words | `wc file.txt` |
| Count characters | `wc -m file.txt` |
| Show first lines | `head file.txt` |
| Show last lines | `tail file.txt` |
| Show middle lines | `head -5 file.txt \| tail -3` |
| Sort lines | `sort file.txt` |
| Remove adjacent duplicates | `uniq file.txt` |
| Reverse line order | `tac file.txt` |
| Reverse characters | `rev file.txt` |
| Translate characters | `tr` |
| Extract columns | `cut` |
| Show system info | `uname -a` |
| Show host name | `hostname` |
| Show date and time | `date` |
| Show calendar | `cal` |
| List processes | `ps` |
| Stop a process | `kill <pid>` |
| Show current user | `whoami` |
| Show logged-in users | `who` |
| Show terminal | `tty` |
| Show file details | `stat file.txt` |
| Change permissions | `chmod 755 file.txt` |
| Change owner | `chown user file.txt` |
| Open text editor | `vim file.txt` |
| Create alias | `alias name='command'` |
| Remove alias | `unalias name` |
| Prime factors | `factor <number>` |
| Save output to a file | `command > out.txt` |
| Save errors to a file | `command 2> err.txt` |
| Use pipe | `command1 \| command2` |
| View command help | `man <command>` |

---

## Summary

Basic Linux command-line work includes navigation, environment variables, file and directory operations, links, ownership, permissions, content viewing, sorting, searching, text processing, redirection, and system/session commands. Useful flags and operators to remember include `-l`, `-a`, `-A`, `-h`, `-t`, `-S`, `-p`, `-r`, `-R`, `-f`, `-i`, `-n`, `-b`, `-s`, `-v`, `-c`, `-w`, `-E`, `-i`, `>`, `>>`, `2>`, and `|`.

## Related

- [[Setting Up Apache HTTP Server]]
- [[HAProxy Setup]]
- [[Squid Proxy Server]]