# Terminal Command - awk

_**awk**_ is a utility that enables a programmer to write tiny but effective programs in the form of statements that define text patterns that are to be searched for in each line of a document and the action that is to be taken when a match is found within a line. <sup>[[1]](#references) <sup>

_**awk**_ is abbrieviated from the names of the developers - Aho, Weinberger & Kernighan. <sup>[[1]](#references) <sup>

The main usage of awk is in

1. Text processing
2. Producing formatted text reports
3. Performing arithmetic operations 
4. Performing string operations and much much more.

A great start to understand any linux command is to to `man` it.

```shell
~$ man awk
```

---

## Structure

_**awk**_ works by scanning 

---

## Conditional Statements

awk also works with conditinal statements

---

## Looping Constructs

we can also use a looping construct, making it one of the most versatile and powerful command in the terminal

---

## Flags

this is a test

---

## Caveats

Only eight-bit characters sets are handled correctly.

The scope rules for variables in functions are a botch; the syntax is worse. 

There are no explicit conversions between numbers and strings.  To force an expression to be treated as a number add 0 to it; to force it to be treated as a string concatenate "" to it.

---

## References

1. [AWK command in Unix/Linux with examples - geeksforgeeks.org](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)


2. Linux Manual (man awk)

---