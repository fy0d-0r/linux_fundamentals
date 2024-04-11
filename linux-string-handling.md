# Linux String Handling



## AWK
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


