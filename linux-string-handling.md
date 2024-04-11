# Linux String Handling

Uppercase / Lowercase bash
```
echo "Hello" | tr '[:upper:]' '[:lower:]'
echo "Hello" | awk '{print tolower($0)}'
echo "Hello" | awk '{print toupper($0)}'
```

`/etc/passwd`
```
grep -v "false\|nologin" /etc/passwd | tr ":" " " | column -t
```
## AWK
