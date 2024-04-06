# zip,rar,tar

# gzip,7z,zip,rar,tar

# gzip/gunzip

### tar
```
Options
z - gzip
c - compress
x - extract
v - verbose
f - specify archive
```

### Compress tar
`$ tar -cvf <file.tar> <file> <dir>`
### Extract tar
`$ tar -xvf <file.tar> <file> <dir>`

### Compress tar.gz (tar.gz = tgz)
`$ tar zcvf <file.tar.gz> <file> <dir>`

### Extract tar.gz
`$ tar zxvf <file.tar.gz>`
`$ tar zxvf <file.tgz>`

### Compress tar.bz2
`$ tar jcvf <file.tar.bz2> <file> <dir>`
### Extract tar.bz2
`$ tar jxvf <file.tar.bz2> <file> <dir>`

## zip/unzip
```
options:
-r [recursive]
-e [encrypt][password တောင်းတယ်]
```

### zipping a file
`$ zip <file.zip> <file>`
### zipping a directory
`$ zip -r <file.zip> <dir>`
`$ zip -r <file.zip> <dir> <file>`
### encrypt
`$ zip -re <file.zip> <dir>`
`$ zip -re <file.zip> <dir> <file>`
### unzipping file
`$ unzip <file.zip>`

## 7z
```
Options:
a [compress]
e [raw extract][recommend building a empty directory to extract inside]
x [extract in discrete directory]
-p [password protect]
```
### Compress
`$ 7z a <file.7z> <file> <dir>`
`$ 7z a <file.7z> <file> <dir> -p`
### Extract
`$ 7z e <file.7z> `
`$ 7z x <file.7z>`

## rar/unrar
```
Options:
a [compress]
e [raw extract]
x [extract in discrete directory]
-p [password protect]
```
### Compress
`$ rar a <file.rar> <file> <dir> -p`
### Extract
`$ unrar e <file.rar>`
`$ unrar x <file.rar>`
