# Linux String Handling

Uppercase / Lowercase bash
```
echo "Hello" | tr '[:upper:]' '[:lower:]'
echo "Hello" | awk '{print tolower($0)}'
echo "Hello" | awk '{print toupper($0)}'
```
## AWK
