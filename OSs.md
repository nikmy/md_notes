# Операционные системы (2 курс ИВТ)

# Chapter 1: Shell Scripts

```shell
# No spaces!
A=42
echo $A         # out: 42
echo $((A / 2)) # out: 21

# Last returned 

bc -l           # floating-point calculations

W='world'
A='hello $W'  # hello $W
A="hello $W"  # hello world

# Filter output
ls -a | grep 'git'

# Regular expressions
grep '^.... ' file.txt

# Extended regex
grep -E file.txt

# Perl regex (Linux only)
grep -P file.txt

# First column fro file with delimiter ','
cut -d , -f 1 file.csv

# Home dir for root
cat /etc/passwd | grep ^root | cut -d : -f 6

# Display first / last 5 rows
head -n 5
tail -n 5

# Display only unique rows
uniq

# Sort rows
sort

# Replace $regex with $str
sed "s/$regex/$str"

# Swap 1st and 2nd strings
sed -E "s/([a-z]+) ([a-z]+)/\2 \1"

# Remove all entries of $regex
sed -E "/$regex/d"

# Show differences between two files
diff file1.txt file2.txt

# Archive
gzip file.big
gunzip file.big.gz

# For archives:
zcat file.big.gz
zgrep $regex file.big.gz

# File info
stat file.txt

# Search file
whereis gcc
```

- ***Useful references:***
  - https://ravesli.com/bash-v-linux/ - More about bash-scripts
  - https://regex101.com              - Regex explanations
  - https://habr.com/ru/post/545150/  - More about regex

