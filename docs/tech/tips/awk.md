# Text processing in command line with `awk` 

`awk` is a command-line tool used for pattern scanning and processing. It's helps search, extract and transform text based on patterns (like regular expressions).

### 

By default, awk treats whitespace (spaces or tabs) as the field separator. However, if you're working with CSV or tab-delimited files, you can easily change the field separator with the -F flag:

```sh
awk -F ',' '{ print $1, $3 }' data.csv
```

```sh
awk '{ if ($1 > 100) print "High", $1; else print "Low", $1 }' data.txt
```

### 


- `awk`
- `sed`
- `grep`

