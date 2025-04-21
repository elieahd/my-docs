# Text Editing with sed

`sed`, short for Stream Editor, is a Unix utility that parses and transforms text, often in a single line of code.

## Use Cases

### Find and replace
Replaces the first occurrence of "apple" with "orange" on each line.
```sh
sed 's/apple/orange/g' file.txt
```
Adds the g flag to replace all instances per line.

### Delete a Line

Deletes the 3rd line

```sh
sed '3d' file.txt
```

Deletes any line containing the word "error".
```sh
sed '/error/d' file.txt
```

### Insert or Append
Inserts a line before line 3
```sh
sed '3i\New line above line 3' file.txt
```

Appends a line after line 3
```sh
sed '3a\New line below line 3' file.txt
```

### Print Specific Lines
Prints only line 5. The -n flag suppresses automatic output.
```sh
sed -n '5p' file.txt
```

Prints lines 2 through 4
```sh
sed -n '2,4p' file.txt
```