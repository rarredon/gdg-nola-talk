# gdg-nola-talk

This document contains notes for the talk given to GDG New Orleans.

# How to use the command line <!-- 5 mins -->

### MacOS and Unix based systems

### Windows

### Bash vs Zsh

# The Basics <!-- 10 mins -->

## Hello, World

### `echo`

Write input back to standard output

**Examples**

    echo "Hello, world"
	echo "Write text to file" >> file.txt

## Navigation

### `pwd`

Return the current directory

### `cd`

Change directory to the one specified

**Examples**

    cd
    cd ~
    cd $HOME
    cd Downloads

### `ls`

List contents of current directory

**Examples**

    ls
    ls -l
    ls -lrS  # Display file info sorted by increasing size

## File interaction

### `cat`

Display the contents of a file

**Examples**

    cat repeated_lines.txt

### `less`

Display file contents within a buffer

**Examples**

    less lipsum.txt

### `head`

Display first lines of a file

**Examples**

    head lipsum.txt
    head -n 20 lipsum.txt

### `tail`

Display last lines of a file

**Examples**

    tail lipsum.txt
    tail -n 20 lipsum.txt

### `wc`

Count number of words, lines, characters in a file

**Examples**

    wc lipsum.txt
	wc -l lipsum.txt
	wc -c lipsum.txt

### `grep`

Search file for a specific word

**Examples**

    grep lorem lipsum.txt
	grep my_function -r code_dir

[Further reading](https://www.gnu.org/software/grep/manual/grep.html)

## Data manipulation <!-- If time permits -->

### `tr`

Substitue or delete selected characters from a file



### `cut`

Parse selected portions from lines of a file

### `uniq`

## `sort`

## The big guns

### `sed`

Short for "steam editor". Useful for string replacement, deletion and all around text processing.

Read the (manual)[https://www.gnu.org/software/sed/manual/sed.html].

### `awk`

A full-fledged programming languange convienient for text processing on the command line.

Read the (manual)[https://www.gnu.org/software/gawk/manual/gawk.html].

## Getting help

### `-h`/`--help`

Most command provide a help flag `-h` or `--help` that displays basic command usage.

### `man`

Display the manual for a command

**Examples**
```
man less
man grep
man man
```

### `help`

Help for builtin commands

**Examples**
```
help cd
```

## Combining commands with the Pipe operator `|`

# Loops and conditional execution <!-- 5 mins... if time permits -->

### `for` loops

### `while` loops

### `&&` operator

### `||` operator

# Commands for web dev <!-- 10 mins -->

### `curl`

### `http`

### `jq`
