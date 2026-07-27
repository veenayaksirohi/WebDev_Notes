	# Shell Scripting Notes

## Basics

### Shebang

```bash
#!/bin/bash
# Specifies the interpreter to use
```

### Making a script executable

```bash
chmod +x script.sh
./script.sh
```

### Comments

```bash
# Single line comment

: '
Multi-line comment
goes here
'
```

---

## Variables

```bash
# Define a variable (no spaces around =)
name="John"
age=25

# Access a variable
echo $name
echo ${name}

# Read-only variable
readonly PI=3.14

# Unset a variable
unset name
```

### Special Variables

```bash
$0    # Script name
$1-$9 # Positional parameters (arguments)
$#    # Number of arguments
$@    # All arguments as separate words
$*    # All arguments as a single word
$?    # Exit status of last command
$$    # Process ID of current shell
$!    # Process ID of last background command
```

---

## Input/Output

```bash
# Print to console
echo "Hello World"
echo -n "No newline"              # Suppress newline
echo -e "Line1\nLine2"            # Enable escape sequences
printf "Name: %s\n" "$name"

# Read user input
read var
read -p "Enter name: " name
read -sp "Enter password: " password  # silent input

# Read multiple values
read -p "Enter two numbers: " num1 num2
```

---

## Conditionals

### if-else

```bash
if [ condition ]; then
    # commands
elif [ condition ]; then
    # commands
else
    # commands
fi
```

### Test Operators

**Numeric comparisons:**

```bash
-eq   # equal
-ne   # not equal
-lt   # less than
-le   # less than or equal
-gt   # greater than
-ge   # greater than or equal
```

**String comparisons:**

```bash
=     # equal
!=    # not equal
-z    # empty string
-n    # non-empty string
```

**File tests:**

```bash
-e    # exists
-f    # regular file
-d    # directory
-r    # readable
-w    # writable
-x    # executable
-s    # non-empty file
```

### Examples

```bash
if [ $age -gt 18 ]; then
    echo "Adult"
fi

if [ -f "file.txt" ]; then
    echo "File exists"
fi

if [ "$name" = "John" ]; then
    echo "Hello John"
fi
```

### case statement

```bash
case $var in
    pattern1)
        # commands
        ;;
    pattern2)
        # commands
        ;;
    *)
        # default
        ;;
esac

# Example: Calculator
read -p "Enter operation (1-Add 2-Sub 3-Mul 4-Div): " choice
read -p "Enter two operands: " op1 op2

case $choice in
    1)
        echo $(expr $op1 + $op2)
        ;;
    2)
        echo $(expr $op1 - $op2)
        ;;
    3)
        echo $(expr $op1 \* $op2)
        ;;
    4)
        echo $(expr $op1 / $op2)
        ;;
    *)
        echo "Invalid operation"
        ;;
esac
```

### select statement

Creates an interactive menu automatically.

```bash
select option in Add Sub Mul Div Quit; do
    case $option in
        Add|Sub|Mul|Div)
            read -p "Enter two operands: " op1 op2
            ;;
    esac
    
    case $option in
        Add)
            echo $(expr $op1 + $op2)
            ;;
        Sub)
            echo $(expr $op1 - $op2)
            ;;
        Mul)
            echo $(expr $op1 \* $op2)
            ;;
        Div)
            echo $(expr $op1 / $op2)
            ;;
        Quit)
            break
            ;;
        *)
            echo "Invalid option"
            ;;
    esac
done
```

### Regex matching with [[

```bash
# Pattern matching with =~
if [[ $string =~ ^pattern ]]; then
    echo "Matches pattern"
fi

# Example: Check if file is hidden (starts with .)
if [[ $filename =~ ^\. ]]; then
    echo "Hidden file"
fi

# Example: Check file extension
if [[ $filename =~ \.png$ ]]; then
    echo "PNG image"
elif [[ $filename =~ \.mp4$ ]]; then
    echo "MP4 video"
fi
```

---

## Loops

### for loop

```bash
# Iterate over list
for item in item1 item2 item3; do
    echo $item
done

# Using seq command
for i in $(seq 10); do
    echo $i
done

# C-style for loop
for ((i=0; i<5; i++)); do
    echo $i
done

# Iterate over files
for file in *.txt; do
    echo $file
done
```

### while loop

```bash
while [ condition ]; do
    # commands
done

# Example
count=1
while [ $count -le 5 ]; do
    echo $count
    ((count++))
done
```

### until loop

```bash
until [ condition ]; do
    # commands
done

# Example: Print multiplication table
read -p "Enter number: " num
i=1
until [ $i -eq 11 ]; do
    echo $(expr $i \* $num)
    i=$(expr $i + 1)
done
```

### Loop control

```bash
break     # Exit loop
continue  # Skip to next iteration
```

---

## Functions

```bash
# Define a function
function_name() {
    # commands
    echo "Hello from function"
}

# Using function keyword
function print_msg {
    echo "This is my first function in bash"
}

# Call a function
function_name

# Function with parameters
greet() {
    echo "Hello $1"
}
greet "John"

# Return value
add() {
    return $(($1 + $2))
}
add 5 3
echo $?  # prints 8

# Function with echo return
factorial() {
    fact=1
    for ((i=1; i<=$1; i++)); do
        fact=$(expr $fact \* $i)
    done
    echo $fact
}

result=$(factorial 5)
echo "5! = $result"
```

---

## Arrays

```bash
# Define array
arr=(item1 item2 item3)

# Using declare
declare -a arr

# Access elements
echo ${arr[0]}      # first element
echo ${arr[@]}      # all elements (also ${arr[*]})
echo ${#arr[@]}     # array length (also ${#arr[*]})

# Array slicing
echo ${arr[@]:2}        # elements from index 2
echo ${arr[@]:1:3}      # 3 elements from index 1

# Add element
arr+=(item4)

# Iterate over array
for item in "${arr[@]}"; do
    echo $item
done

# Iterate with index
for ((i=0; i<${#arr[@]}; i++)); do
    echo "arr[$i] = ${arr[$i]}"
done
```

### Array input from user

```bash
declare -a arr

echo "Enter 5 array elements:"
for ((i=0; i<5; i++)); do
    read -p "arr[$i]: " arr[$i]
done

echo "Array elements:"
for ((i=0; i<${#arr[@]}; i++)); do
    echo -n " ${arr[$i]}"
done
echo ""
```

### Array operations

```bash
arr=(10 20 30 40 50)

# Sum of array elements
sum=0
for ele in ${arr[@]}; do
    sum=$(expr $sum + $ele)
done
echo "Sum: $sum"

# Average
avg=$(expr $sum / ${#arr[@]})
echo "Average: $avg"
```

---

## String Operations

```bash
# Length
${#string}

# Substring
${string:position}               # From position to end
${string:position:length}        # Specific length from position

# Concatenation
str3=$str1$str2

# Replace
${string/pattern/replacement}    # first occurrence
${string//pattern/replacement}   # all occurrences

# Remove prefix/suffix
${string#pattern}    # remove shortest prefix
${string##pattern}   # remove longest prefix
${string%pattern}    # remove shortest suffix
${string%%pattern}   # remove longest suffix

# Uppercase/Lowercase
${string^^}          # to uppercase
${string,,}          # to lowercase

# Reverse string (using rev command)
reversed=$(echo "$string" | rev)
```

---

## Arithmetic

```bash
# Using (( ))
((result = 5 + 3))
echo $result

# Using let
let result=5+3

# Using expr (for integers)
result=$(expr 5 + 3)
result=$(expr $num1 \* $num2)    # Escape * for multiplication

# Using $[ ]
result=$[5 + 3]

# Using bc (for floating-point)
result=$(echo "3.142 * 5 * 5" | bc)
result=$(echo "scale=2; 10 / 3" | bc)  # Set decimal places
```

---

## Command Substitution

```bash
# Using $( )
current_date=$(date)

# Using backticks (older style)
current_date=`date`
```

---

## Redirection

```bash
command > file       # Redirect stdout to file (overwrite)
command >> file      # Redirect stdout to file (append)
command 2> file      # Redirect stderr to file
command &> file      # Redirect both stdout and stderr
command < file       # Read input from file
command1 | command2  # Pipe output to another command
```

---

## Exit Status

```bash
exit 0    # Success
exit 1    # Failure

# Check exit status
if [ $? -eq 0 ]; then
    echo "Success"
fi
```

---

## Debugging

```bash
# Run script in debug mode
bash -x script.sh

# Enable debugging in script
set -x    # Enable
set +x    # Disable

# Exit on error
set -e
```

---

## Best Practices

- Always quote variables: `"$var"`
- Use `[[` instead of `[` for conditionals (bash)
- Check if file exists before operations
- Use meaningful variable names
- Add comments for complex logic
- Handle errors appropriately
- Use functions for reusable code
- Validate user input before using it
- Use `chmod +x script.sh` to make scripts executable

---

## Practical Examples

### Example 1: Calculate Rectangle Area

```bash
#!/bin/bash
read -p "Enter length and breadth: " length breadth
area=$(expr $length \* $breadth)
echo "Area of rectangle: $area"
```

### Example 2: Calculate Circle Area

```bash
#!/bin/bash
read -p "Enter radius: " radius
area=$(echo "3.142 * $radius * $radius" | bc)
echo "Area of circle: $area"
```

### Example 3: Find Maximum of Two Numbers

```bash
#!/bin/bash
read -p "Enter two numbers: " num1 num2

if [ $num1 -eq $num2 ]; then
    echo "Both numbers are equal"
    max=$num1
elif [ $num1 -gt $num2 ]; then
    echo "num1 is greater"
    max=$num1
else
    echo "num2 is greater"
    max=$num2
fi

echo "Maximum value: $max"
```

### Example 4: Check Palindrome String

```bash
#!/bin/bash
read -p "Enter string: " str

if [ -z "$str" ]; then
    echo "String is empty"
    exit 1
fi

reversed=$(echo "$str" | rev)

if [ "$str" = "$reversed" ]; then
    echo "$str is a palindrome"
else
    echo "$str is not a palindrome"
fi
```

### Example 5: String Operations

```bash
#!/bin/bash
str1="sunbeam"
str2="infotech"

# Concatenation
str3=$str1$str2
echo "Concatenated: $str3"

# Substring from index 7
echo "From index 7: ${str3:7}"

# 4 characters from index 7
echo "4 chars from index 7: ${str3:7:4}"

# Check equality
if [ "$str1" = "$str2" ]; then
    echo "Strings are equal"
else
    echo "Strings are not equal"
fi
```

### Example 6: System Information Script

```bash
#!/bin/bash
echo "=== System Information ==="
echo -n "Today's date: "; date
echo "Current month calendar:"
cal
echo "Logged in user: $USER"
echo "Home directory: $HOME"
echo -n "Operating system: "; uname
```

### Example 7: Prime Number Check

```bash
#!/bin/bash
read -p "Enter number: " num

i=2
while [ $i -lt $num ]; do
    if [ $(expr $num % $i) -eq 0 ]; then
        break
    fi
    i=$(expr $i + 1)
done

if [ $i -eq $num ]; then
    echo "$num is prime number"
else
    echo "$num is not prime number"
fi
```

### Example 8: Count Files and Directories

```bash
#!/bin/bash
f_cnt=0
d_cnt=0

for entry in $(ls); do
    if [ -f $entry ]; then
        f_cnt=$(expr $f_cnt + 1)
    elif [ -d $entry ]; then
        d_cnt=$(expr $d_cnt + 1)
    fi
done

echo "Current directory: $PWD"
echo "File count: $f_cnt"
echo "Directory count: $d_cnt"
```

### Example 9: Count Hidden Files

```bash
#!/bin/bash
cnt=0

for entry in $(ls -A); do
    if [[ $entry =~ ^\. ]]; then
        cnt=$(expr $cnt + 1)
    fi
done

echo "Hidden files count: $cnt"

# Alternative using grep
cnt=$(ls -A | grep -c "^\.")
echo "Hidden files count (using grep): $cnt"
```

### Example 10: Separate Images and Videos

```bash
#!/bin/bash
# Create directories if they don't exist
mkdir -p images videos

for entry in $(ls); do
    if [[ $entry =~ \.png$ ]] || [[ $entry =~ \.jpg$ ]]; then
        mv "$entry" images/
    elif [[ $entry =~ \.mp4$ ]] || [[ $entry =~ \.avi$ ]]; then
        mv "$entry" videos/
    fi
done

echo "Images and videos are separated!"
```

### Example 11: Package Installation Script

```bash
#!/bin/bash
pkgs=(git gcc vim curl wget)

echo "Updating package lists..."
sudo apt-get update

for pkg in ${pkgs[@]}; do
    echo "Installing $pkg..."
    sudo apt-get -y install $pkg
done

echo "All packages installed!"
```

### Example 12: Positional Parameters

```bash
#!/bin/bash
echo "Script name: $0"
echo "PID of bash shell: $$"
echo "Number of arguments: $#"
echo "All arguments: $*"

echo "1st parameter: $1"
echo "2nd parameter: $2"
echo "3rd parameter: $3"
echo "4th parameter: $4"

# Usage: ./script.sh arg1 arg2 arg3 arg4
```
