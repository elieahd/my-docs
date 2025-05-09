# Text processing with `awk`

`awk` is a command-line tool used for pattern scanning and processing. It's helps search, extract and transform text based on patterns. It's also handy when working with files.

### Extracting fields

Extracts username (3rd field) and filenames (9th field) from `ls -l` output.

```sh
ls -l | awk '{ print $3, $9 }'
```

### Filtering rows 

Shows processes using more than 50% CPU

```sh
ps aux | awk '$3 > 50 { print $0 }'
```

`$3` refers to the third field, which is the CPU usage in ps aux output.

### Working with files

Let's say we have the following csv file : `items.csv`

```
item,price
ItemA,12.50
ItemB,7.99
ItemC,20.00
ItemD,5.25
ItemE,9.30
```

You can print the entire file content with 

```sh
awk '{ print $0 }' items.csv
```

We can add a line number by adding `NR`

```sh
awk '{ print NR, $0 }' items.csv
```

Since it's a csv file, We can omit headers by adding `NR > 1`

```sh
awk 'NR > 1 { print $0 }' items.csv
```

We can print by specifying columns

```sh
awk -F ',' '{ print $1, $2 }' items.csv
```

`-F ','` flag define the field separator, the default field separator is a whitespace

### Summing values

To calculate the total price of all items 

```sh
awk -F ',' 'NR > 1 { sum += $2 } END { print "Total:", sum }' items.csv
```

`END` is a block that runs after all lines are processed

### Map based on condition

Label items as "High" or "Low" based on their price

```sh
awk -F ',' 'NR > 1 { if ($2 > 10) print $1, "is High"; else print $1, "is Low" }' items.csv
```