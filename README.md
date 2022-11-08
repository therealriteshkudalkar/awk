# Terminal Command - awk

_**awk**_ is a utility that enables a programmer to write tiny but effective programs in the form of statements that define text patterns that are to be searched for in each line of a document and the action that is to be taken when a match is found within a line. <sup>[[1]](#references) <sup>

_**awk**_ is abbrieviated from the names of the developers - Aho, Weinberger & Kernighan. <sup>[[1]](#references) <sup>

<br>

### Usage

The main usage of awk is in

1. Text processing
2. Producing formatted text reports
3. Performing arithmetic operations 
4. Performing string operations and much much more.

<br>

### Working

_**awk**_ works by scanning the input line by line. Compares input line/fields to pattern (regular expression). If the pattern is not provided, it considers the entire line. It then peforms the given action on the matched line.

<br>

### General Syntax

```shell
~$ awk [flags] '[BEGIN {action}] [pattern] {action} [END {action}]' input_file > output_file
```

A great way to understand any linux command is to to `man` it.

```shell
~$ man awk
```

---

## Structure

The awk argument can be separated into three blocks.

<br>

### BEGIN block

The BEGIN block gets executed at program start-up. It executes only once. This is good place to initialize variables. BEGIN is an AWK keyword and hence it must be in upper-case. Please note that this block is optional.

```
BEGIN { awk_commands }
```

<br>

### Body block

The body block applies AWK commands on every input line. By default, AWK executes commands on every line. We can restrict this by providing patterns. Note that there are no keywords for the Body block.

```
/pattern/ { awk_commands }
```

<br>

### END block

The END block executes at the end of the program. END is an AWK keyword and hence it must be in upper-case. Please note that this block is optional.

```
END { awk_commands }
```

---

## Standard awk Commands

The following command carry special meaning in the awk argument:

<br>

### print

The print statement prints its arguments on the standard output (or on a file if > file  or >> file  is present or on a pipe if | cmd  is present), separated by the current output field separator, and terminated by the output record separator.  file and cmd may be literal names or parenthesized expressions; identical string values in different statements denote the same open file.

```shell
~$ awk '{print $3 "\t" $4}' marks.txt
```

<br>

### printf

The printf statement formats its expression list according to the format provided.

```shell
~$ awk '{printf "%5.1f\n", $1}' marks.txt
```

---

## Standard awk Variables

awk provides several built-in variables. They play an important role while writing awk scripts.

<br>

### $n

It represents the nth field in the current record where the fields are separated by FS.

```shell
~$ awk '{print $3 "\t" $4}' marks.txt
```

<br>

### ARGC

It implies the number of arguments provided at the command line.

```shell
~$ awk 'BEGIN {print "Arguments =", ARGC}' One Two Three Four
```

<br>

### ARGV

It is an array that stores the command-line arguments. The array's valid index ranges from 0 to ARGC-1.

```shell
~$ awk 'BEGIN { 
    for (i = 0; i < ARGC - 1; ++i) { 
      printf "ARGV[%d] = %s\n", i, ARGV[i] 
    } 
  }' one two three four
```

<br>

### FS

It represents the (input) field separator and its default value is space. You can also change this by using -F command line option.

```shell
~$ awk 'BEGIN {print "FS = " FS}' marks.txt
```

<br>

### NF

It represents the number of fields in the current record. For instance, the following example prints only those lines that contain more than two fields.

```shell
~$ awk 'NF > 2' test.txt
```

<br>

### NR

It represents the number of the current record. For instance, the following example prints the record if the current record number is less than three.

```shell
~$ awk 'BEGIN {print "FS = " FS}' marks.txt
```

<br>


### RS

It represents (input) record separator and its default value is newline.

```shell
~$ awk awk 'BEGIN {print "RS = " RS}' marks.txt
```

<br>

---

## Conditional Statements

awk also works with conditinal statements

---

## Looping Constructs

we can also use a looping construct, making it one of the most versatile and powerful command in the terminal

---

## Flags

With awk, we can work with the following flags:

### -F <u>fs</u>

The -F fs option defines the input field separator to be the regular expression fs.

###

---

## Caveats

Only eight-bit characters sets are handled correctly. <sup>[[2]](#references) <sup> 

The scope rules for variables in functions are a botch; the syntax is worse. <sup>[[2]](#references) <sup>

There are no explicit conversions between numbers and strings.  To force an expression to be treated as a number add 0 to it; to force it to be treated as a string concatenate "" to it. <sup>[[2]](#references) <sup>

---

## Examples

This is a text

---

## References

1. [AWK command in Unix/Linux with examples - geeksforgeeks.org](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)


2. Linux Manual (man awk)

---