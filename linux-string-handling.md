# Linux String Handling

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
```

### `/etc/shells`
```
awk -F '/' '/^\// {print $NF}' /etc/shells | uniq | sort
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


## AWK

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
Using Regular Expressions specified between two '/' s for selecting specific lines
The following command deals with the lines that start with forward slash `^\/` .
```
awk -F "/" '/^\// {print $NF}' /etc/shells
```

Modifying text
```
awk '{$2="text"}' filename
awk -F ':' '{$2="text";print $0}' /etc/passwd
awk -F ':' '{$2="text";print $1"\t"$2}' /etc/passwd | column -t
```










