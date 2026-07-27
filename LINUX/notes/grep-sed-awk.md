---
title: "grep, sed, awk Command Reference"
date: 2026-04-09
tags: [study, linux, commands, cli, text-processing]
subject: "Linux Administration"
source: "Class Notes"
status: complete
---

# grep, sed, awk Command Reference

## grep

Search for patterns in files.

```bash
# Basic search
grep "pattern" file.txt

# Case-insensitive search
grep -i "pattern" file.txt

# Recursive search in directory
grep -r "pattern" /path/to/dir

# Show line numbers
grep -n "pattern" file.txt

# Invert match (lines that don't match)
grep -v "pattern" file.txt

# Count matching lines
grep -c "pattern" file.txt

# Count non-matching lines
grep -vc "pattern" file.txt

# Show only matching part
grep -o "pattern" file.txt

# Match whole word
grep -w "word" file.txt

# Use extended regex
grep -E "pattern1|pattern2" file.txt

# Show N lines before/after match
grep -A 2 -B 2 "pattern" file.txt

# Match lines starting with a character
grep "^f" file.txt

# Match lines ending with a character
grep "\.$" file.txt

# Match lines starting with a dot
grep "^\." file.txt
```

### egrep

Extended regex search, equivalent to `grep -E`.

```bash
egrep "pattern1|pattern2" file.txt
egrep "^(foo|bar)" file.txt
```

### fgrep

Fixed string search, no regex. Equivalent to `grep -F`.

```bash
fgrep "exact.string" file.txt
```

> [!TIP]
> Use `fgrep` (or `grep -F`) when you want literal string matching and do not need regex interpretation.

---

## sed

Stream editor for filtering and transforming text.

```bash
# Basic substitution (first occurrence per line)
sed 's/old/new/' file.txt

# Global substitution (all occurrences)
sed 's/old/new/g' file.txt

# Case-insensitive substitution
sed 's/old/new/gi' file.txt

# Edit file in place
sed -i 's/old/new/g' file.txt

# Delete lines matching pattern
sed '/pattern/d' file.txt

# Delete specific line number
sed '3d' file.txt

# Delete a range of lines
sed '5,7d' file.txt

# Print specific line
sed -n '5p' file.txt

# Print line range
sed -n '2,5p' file.txt

# Insert line before match
sed '/pattern/i\
new line' file.txt

# Append line after match
sed '/pattern/a\
new line' file.txt

# Replace entire line matching pattern
sed 's/.*pattern.*/replacement/' file.txt

# Print only changed lines
sed -n 's/old/new/p' file.txt

# Extended regex substitution
sed -E 's/Linux|Unix/OS/g' file.txt
```

> [!WARNING]
> Be careful with `sed -i` as it modifies files in place. Consider backing up files or using `-i.bak` on some systems.

---

## awk

Pattern scanning and text processing language. Processes input line by line, splitting each line into fields (`$1`, `$2`, …). Great for logs, CSVs, and structured data.

### Syntax

```text
awk [options] 'pattern {action}' file
```

Options:
- `-F` : field separator
- `-f` : read program from a script file
- `-v` : define a variable

Built-in variables:
- `$0`  : entire line
- `$1, $2, ...` : individual fields
- `NR`  : current line number
- `NF`  : number of fields in current line
- `FS`  : input field separator (default: whitespace)
- `RS`  : input record separator (default: newline)
- `OFS` : output field separator (default: space)
- `ORS` : output record separator (default: newline)

```bash
# Print specific column (field)
awk '{print $1}' file.txt

# Print multiple columns
awk '{print $1, $3}' file.txt

# Print all lines
awk '{print}' file.txt

# Custom field separator
awk -F: '{print $1}' /etc/passwd
awk -F ',' '{print $1, $2}' file.csv

# Print lines matching pattern
awk '/pattern/ {print}' file.txt

# Print with line numbers
awk '{print NR, $0}' file.txt

# Print first and last column
awk -F ',' '{print $1, $NF}' file.txt

# Print line count
awk 'END {print NR}' file.txt

# Sum a column
awk '{sum += $2} END {print sum}' file.txt

# Print lines where column value > N
awk '$3 > 100 {print}' file.txt

# Print with custom output separator
awk -F: '{print $1 " -> " $6}' /etc/passwd

# If/else logic
awk '{if ($2 > 50) print $1, "high"; else print $1, "low"}' file.txt

# Print number of fields per line
awk '{print NF}' file.txt

# Skip header line
awk 'NR > 1 {print $1}' file.txt

# Print a range of lines
awk 'NR==2, NR==3 {print NR, $0}' file.txt

# Print empty lines (lines with no fields)
awk 'NF <= 0 {print NR}' file.txt

# Define a variable with -v
awk -v limit=20 '$1 < limit {print $1, $2}' file.txt

# Print message before processing
awk -v msg="Details:" 'BEGIN {print msg} {print}' file.txt

# Find length of longest line
awk '{if (length($0) > max) max = length($0)} END {print max}' file.txt

# BEGIN and END blocks
awk 'BEGIN {print "Start"} {print $0} END {print "End"}' file.txt

# Run awk from a script file (-f)
awk -f script.awk file.txt
```

### awk script file (`script.awk`)

Use a shebang to make an awk file directly executable.

```awk
#!/usr/bin/awk -f

BEGIN { print "---- Start ----" }
      { print $1, $2, $5 }
END   { print "---- End ----" }
```

```bash
chmod +x script.awk
./script.awk file.txt
```

---

## Combining grep, sed, awk

```bash
# grep output piped to awk
grep "error" app.log | awk '{print $1, $2}'

# sed output piped to grep
sed 's/foo/bar/g' file.txt | grep "bar"

# Chain all three
grep "pattern" file.txt | sed 's/old/new/g' | awk '{print $1}'
```

> [!INFO]
> A common pattern is: `grep` to filter lines, `sed` to transform them, and `awk` to extract or compute fields from the result.