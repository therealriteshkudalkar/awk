# Terminal Command - awk

_**awk**_ is a utility that enables a programmer to write tiny but effective programs in the form of statements that define text patterns that are to be searched for in each line of a document and the action that is to be taken when a match is found within a line. <sup>[[1]](#references) <sup>

_**awk**_ is abbrieviated from the names of the developers - Aho, Weinberger & Kernighan. <sup>[[1]](#references) <sup>

### Usage

The main usage of awk is in

1. Text processing
2. Producing formatted text reports
3. Performing arithmetic operations 
4. Performing string operations and much much more.

### Working

_**awk**_ works by scanning the input line by line. Compares input line/fields to pattern (regular expression). If the pattern is not provided, it considers the entire line. It then peforms the given action on the matched line.


### General Syntax

```bash
awk [flags] '[BEGIN {action}] [pattern] {action} [END {action}]' input_file > output_file
```

A great way to understand any linux command is to to `man` it.

```shell
man awk
```

## Structure

The awk argument can be separated into three blocks.


### BEGIN block

The BEGIN block gets executed at program start-up. It executes only once. This is good place to initialize variables. BEGIN is an AWK keyword and hence it must be in upper-case. Please note that this block is optional.

```
BEGIN { awk_commands }
```

### Body block

The body block applies AWK commands on every input line. By default, AWK executes commands on every line. We can restrict this by providing patterns. Note that there are no keywords for the Body block.

```
/pattern/ { awk_commands }
```

### END block

The END block executes at the end of the program. END is an AWK keyword and hence it must be in upper-case. Please note that this block is optional.

```
END { awk_commands }
```

## Standard awk Commands

The following command carry special meaning in the awk argument:

### print

The print statement prints its arguments on the standard output (or on a file if > file  or >> file  is present or on a pipe if | cmd  is present), separated by the current output field separator, and terminated by the output record separator.  file and cmd may be literal names or parenthesized expressions; identical string values in different statements denote the same open file.

```bash
awk '{print $3 "\t" $4}' marks.txt
```

### printf

The printf statement formats its expression list according to the format provided.

```bash
awk '{printf "%5.1f\n", $1}' marks.txt
```

## Standard awk Variables

awk provides several built-in variables. They play an important role while writing awk scripts.

### $n

It represents the nth field in the current record where the fields are separated by FS.

```bash
awk '{print $3 "\t" $4}' marks.txt
```

### ARGC

It implies the number of arguments provided at the command line.

```bash
awk 'BEGIN {print "Arguments =", ARGC}' One Two Three Four
```

### ARGV

It is an array that stores the command-line arguments. The array's valid index ranges from 0 to ARGC-1.

```bash
awk 'BEGIN { 
    for (i = 0; i < ARGC - 1; ++i) { 
      printf "ARGV[%d] = %s\n", i, ARGV[i] 
    } 
  }' one two three four
```

### FS

It represents the (input) field separator and its default value is space. You can also change this by using -F command line option.

```bash
awk 'BEGIN {print "FS = " FS}' marks.txt
```

### NF

It represents the number of fields in the current record. For instance, the following example prints only those lines that contain more than two fields.

```bash
awk 'NF > 2' test.txt
```

### NR

It represents the number of the current record. For instance, the following example prints the record if the current record number is less than three.

```bash
awk 'BEGIN {print "FS = " FS}' marks.txt
```

### RS

It represents (input) record separator and its default value is newline.

```bash
awk 'BEGIN {print "RS = " RS}' marks.txt
```

## Control FLow Statements

awk provides conditional statements to control the flow of a program. It supports if, if-else and if-else ladder. The syntax of which is as follows:

```
awk '{ if (condition) 
          awk_command;
        else 
          awk_command;
    }' filename
```

## Looping Constructs

We can also use looping construct, like for loop, while loop, making it one of the most versatile and powerful command in the terminal. The syntax is as follows:

```
awk '{ for (initialization; condition; increment/decrement) {
        awk_command;
      }
    }' filename
```

```
awk '{ while (condition) {
        awk_command;
      }
    }' filename
```

## Flags

With awk, we can work with the following flags:

### -F <u>fs</u>

The -F fs option defines the input field separator to be the regular expression fs.

```bash
awk -F ',' '{print $2 "\t" $3} sales.txt
```

### -f <u>progfile</u>

The -f progfile option is used to specify the pattern or the block argument inside a file rather than typing it out in its entirity.

```bash
awk -f cal_sal.awk sales.txt
```

The cal_sal.awk contains the following code

```bash
{
  sales[i++]=$2;
  sum=0;
}
END {
  for (i in sales) {
    sum=sum+sales[i];
  }
  print "Total sales amount=" sum;
}
```

## Caveats

Only eight-bit characters sets are handled correctly. <sup>[[2]](#references) <sup> 

The scope rules for variables in functions are a botch; the syntax is worse. <sup>[[2]](#references) <sup>

There are no explicit conversions between numbers and strings.  To force an expression to be treated as a number add 0 to it; to force it to be treated as a string concatenate "" to it. <sup>[[2]](#references) <sup>

## Examples

Let's start with simple example. Say I have a text file marks.txt

```
Name	Math	History Physics	English	CS	Chemsitry	
Ayush	90	50	44	90	60	53
Aman	100	90	53	88	80	64
Sajal	90	54	53	64	91	84
Rohit	73	93	36	39	99	93
Muskan	90	90	88	94	50	46
Tanvi	80	93	57	66	76	96
Tarun	53	84	50	87	53	48
```

and marks2.txt

```
Name,Math,History,Physics,English,CS,Chemsitry	
Ayush,90,50,44,90,60,53
Aman,100,90,53,88,80,64
Sajal,90,54,53,64,91,84
Rohit,73,93,36,39,99,93
Muskan,90,90,88,94,50,46
Tanvi,80,93,57,66,76,96
Tarun,53,84,50,87,53,48
```

Say I want to print only the name of the students.

```bash
awk '{ print $1 }' marks.txt
```

By default the field delimiter is a space. Say I have a file that is not space separated but comma separated.

```bash
awk -F ',' '{ print $1 }' marks2.txt
```

Now lets say I want the name and marks of all students whose name contains a `u`.

```bash
awk '/u/ { print $0 }' marks.txt
```

I want marks of students whose name starts with `A` and I want their marks in Physics.

```bash
awk '/^A/ { print $1 "\t" $4 }' marks.txt
```

I want to look at the permissions of files that end with `.txt`

```bash
ls -al | awk '/.txt$/ {print $1 "\t" $NF }'
```

Now say, I want to look at marks of students whose score in English is odd.

```bash
awk '{ if($5 % 2 != 0) print $0 }' marks.txt
```

Say I want to print whether the marks in English are divisible by 3.

```bash
awk 'NR > 1 { if($5 % 3 == 0) print $1 " have their English marks divisible by 3."; else print $1 " dont have their English marks divisible by 3."  }' marks.txt
```

Say I want to print whether the marks in English are divisible by a number specified in the argument.

```bash
awk 'NR > 1 { if($5 % ARGV[2] == 0) print $1 " have their English marks divisible by " ARGV[2] "."; else print $1 " dont have their English marks divisible by " ARGV[2] "."  }' marks.txt 5
```

Say I want to print the average obtained by each student.

```bash
awk 'BEGIN { print "Name\tAverage" } NR > 1 { curr_sum = 0; for(i = 2; i <=NF; i++) { curr_sum += $i; }; print $1 "\t" curr_sum / (NF - 1) }' marks.txt
```

Say I want the class average in Physics.

```bash
awk 'BEGIN { sum = 0 } NR > 1 { sum += $4 } END { print "The class average in Physics is " sum / (NR - 1) }' marks.txt
```

## References

1. [AWK command in Unix/Linux with examples - geeksforgeeks.org](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)


2. Linux Manual (man awk)