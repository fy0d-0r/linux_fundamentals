# Linux String Handling


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

`/etc/passwd`
```
grep -v "false\|nologin" /etc/passwd | tr ":" " " | column -t
awk -F ":" '{print $1}' /etc/passwd
```

Printing first specified lines 
```
head .bashrc
sed 11q .bashrc
awk 'NR < 13' .bashrc
```

## AWK


Specifying field separator using -F flag. Default field separator is space.
```
awk -F ":" '{print $1}' /etc/passwd
awk -F ":" '{print $1":"$6":"$7}' /etc/passwd
awk -F ":" '{print $1"\t"$6"\t"$7}' /etc/passwd
```















