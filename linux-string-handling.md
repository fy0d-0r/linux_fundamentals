# Linux String Handling

Utilities
```
echo,seq,grep
awk,sed,cut,tr
uniq,sort,wc,column
xargs,xclip
```

## `echo` and `seq` Utilities

generate a sequence of numbers/characters
```
echo {1..9}
echo {a..e}
echo {A..Z}
```
disable outputting trailing newline
```
echo -n
```
enable interpretation of backslash escapes
```
echo -e
```

```
seq 1 5
seq 0 2 10
```

## `sort` and `wc` Utilities
byte count and line count
```
wc -c
wc -l
```

numeric sorting
```
sort -n
```

## The `grep` Utility

Format
```
grep <sometext> <file1> <file2> <file3> 
```

```
grep "function" file1.php file2.php file3.php
grep "function" ./* (The same as: grep "function" *)
```
```
grep ^[0-9] file.txt #starts with number
-i #case insensitive
 ifconfig | grep -i '^(linux|unix)'
grep -w "text" file.txt #exactly only "test"
-n #also show line number
-B #before
-A #after
-C #Before & After
-r #recursive search
-l #L return all the files that contain a match
-c #return all the files that contain a match and the number of matches
grep -m 1 "test" file.txt #first line of where word "test" found
grep -m 5 "test" file.txt #first five lines of where word "test" found
grep -v <sth> #invert search (exclude what is specified)
Eg: cat /etc/passwd | grep -v "false\|nologin" "It search users that are disabled standard shell"
```

## The `awk` Utility
`awk` manipulates each line in loop

`$0` represents the whole line
```
awk '{print $0}' filename
```

Specifying field separator using -F flag. Default field separator is space.
```
awk -F ":" '{print $1}' /etc/passwd
awk -F ":" '{print $1":"$6":"$7}' /etc/passwd
awk -F ":" '{print $1"\t"$6"\t"$7}' /etc/passwd
```

Using $NF to print last field
```
awk -F "/" '{print $NF}' file.txt
```

Regular expressions are used to select lines according to the rules defined. Regular expressions are specified between `/` s.

The following command deals with the lines that start with forward slash `/` .
```
awk -F "/" '/^\// {print $NF}' /etc/shells
```

Regular expressions can also be used as followings.
```
awk '/sshd/' /etc/passwd
awk '/^sshd/' /etc/passwd
awk '/nologin$/' /etc/passwd
awk '!/false$|nologin$/' /etc/passwd
awk -F ':' '!/false$|nologin$/ {print $1}' /etc/passwd
```

Modifying text
```
awk '{$2="text"}' filename
awk -F ':' '{$2="text";print $0}' /etc/passwd
awk -F ':' '{$2="text";print $1"\t"$2}' /etc/passwd | column -t
```

Replacing field separators
```
awk 'BEGIN{FS=":";OFS="|"} {print $1,$6,$7}' /etc/passwd
```

```
BEGIN {
    FS = ":";   # Set input field separator to colon (:)
    OFS = "|";  # Set output field separator to pipe (|)
}

{
    # Process each input line (not executed for BEGIN block)
    print $1, $6, $7;  # Print specific fields using OFS (|)
}
```
- The BEGIN block initializes FS and OFS to specify field separators.
- The main block ({ ... }) processes each input line and prints specific fields separated by | (OFS).




Handling line numbers

Line number can be specified in `NR` variable.
```
awk 'NR==2' /etc/passwd
awk 'NR==2 {print $3}' /etc/passwd
```

We can aslo use `>` and `<` operators.
```
awk 'NR<11 /etc/passwd`
awk 'NR>20' /etc/passwd

awk -F ':' 'NR<11 {print $1}' /etc/passwd
awk -F ':' 'NR>20 {print $1}' /etc/passwd

awk 'NR>3 && NR<10' /etc/passwd
```
## `cut & tr` Utilities

Search and replace characters
```
echo "This is a line of text" | tr 'a' 'A'
echo "This is a line of text" | tr 'aeio' 'AEIO'
```

Deleting/Complement Deleting characters
```
echo "This is a line of text" | tr -d 'aeio'
echo "This is a line of text" | tr -cd 'aeio\n'
```

Squeezing characters
```
echo "Thiis iis aa liiinee ooof teeext" | tr -s 'aeio'
```

Translate lower case to upper case
```
echo "This is a line of text" | tr '[:lower:]' '[:upper:]'
```

Generate Random Passwords
```
head 3 /dev/urandom | tr -cd '[:print:]'
```

Extract Digits
```
echo "my phone number is 09123456789" | tr -cd '[:digit:]\n'
```

## The `sed` Utility

`sed` stands for "String Editor".
```
sed 's/red/green' file.txt
sed 's/red/green/g' file.txt
```
```
echo "Derek" | sed 's/Derek/DT/g'
```

```
echo "The Emacs file manager is dired red" | sed 's/ red/ green/g' 
```

Rewirte or Modify the file
```
sed -i 's/find/replace/g' filename.txt
sed -i 's/Taylor/Tyler/g' .bashrc
```

Search for specific lines and subsititude
```
tldr sed | sed '/Replace/s/the/THE'
```
Delete lines matching the pattern
```
sed '/pattern/d' filename
```

Multiple Substitutions
```
cat /etc/shells | sed -e 's/usr/u/g' -e 's/bin/b/g'
```

Deleting unnessary spaces only (not tabs) at the end of each line
```
sed -i 's/ *$//' filename
```

Deleting unnessary spaces and tabs at the end of each line
```
sed -i 's/[[:space:]]*$//' filename
```

Deleting Empty lines
```
cat filename | sed -i '/^$/d'
```

## Use Cases
### Upper Case/Lower Case
Translating lowercases to uppercases
```
sed 's/[a-z]/\U&/g' filename
echo "Hello" | tr '[:lower:]' '[:upper:]'
echo "Hello" | awk '{print toupper($0)}'
```
Translating uppercases to lowercases
```
sed 's/[A-Z]/\L&/g' filename
echo "Hello" | tr '[:upper:]' '[:lower:]'
echo "Hello" | awk '{print tolower($0)}'
```

### `/etc/passwd`
```
grep -v "false\|nologin" /etc/passwd | tr ":" " " | column -t
awk -F ":" '{print $1}' /etc/passwd
awk -F ":" '{print $1"\t"$7}' /etc/passwd | column -t
awk '!/false$|nologin$/' /etc/passwd
awk -F ':' '!/false$|nologin$/ {print $1}' /etc/passwd
awk -F ':' 'NR<11 {print $1}' /etc/passwd
```

### `/etc/shells`
```
awk -F '/' '/^\// {print $NF}' /etc/shells | uniq | sort
```

### `df -h`
```
df -h | awk '/^\/dev\/nvme/ {print $1"\t"$2"\t"$3}'
```

### `ps` Command

```
ps -ef | wc -l
ps -ef | awk 'END {print NR}'
```

### Printing first lines 
```
head .bashrc
sed 11q .bashrc
awk 'NR < 13' .bashrc
```
### Printing last lines
```
tail .bashrc 
```
### Using `ls` with Wildcard
```
ls *
```


