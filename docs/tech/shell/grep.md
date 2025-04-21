# Text searching with grep
`grep` stands for Global Regular Expression Print. It’s a command-line utility that searches for lines that match a pattern.

## Use cases
```sh
grep "pattern" file.txt
```

This searches for "pattern" in file.txt and prints every matching line.

### Case-insensitive search

Finds "hello", "Hello", "HELLO", etc.

```sh
grep -i "hello" greetings.txt
```

### View line numbers

Adds line numbers to the matching lines.

```sh
grep -n "main" script.py
```

### Exclude lines (inverse match)
Shows every line except the ones with "DEBUG".
```sh
grep -v "DEBUG" logs.txt
```

### Search all files in a directory
Recursively search for "error" in all files under ./src.
```sh
grep -r "error" ./src
```

### Match exact words

Matches only the word "cat", not "catalog" or "educate".
```sh
grep -w "cat" animals.txt
```

### Highlight 

```sh
grep --color=auto "foo" file.txt
```

### Find files 

```sh
grep -l "TODO" *.js
```

### Search with regular expressions?
```sh
grep -E "dog|cat" animals.txt
```
