# gdg-nola-talk

This document contains notes for my talk given to GDG New Orleans.

# How to use the command line <!-- 5 mins -->

### MacOS

* Built in - `<CMD-Space>` "terminal"
* iTerm2 - [https://iterm2.com/](https://iterm2.com/)

### Windows

* Windows Subsystem for Linux (Windows 10) - [Installation](https://itsfoss.com/install-bash-on-windows/)
* Cygwin - [https://www.cygwin.com/](https://www.cygwin.com/)

### Bash vs Zsh

* Bash - Bourne Again Shell
* Zsh - Z shell
* Bash is default on most Linux based systems.
* Zsh is recently the default on MasOS as of 2019.
* Almost identical in terms of functionality.
* I'll be running the following commands in Bash.

# The Basics <!-- 10 mins -->

## Hello, World

### `echo`

Write input back to standard output

**Examples**

    echo "Hello, world"

	echo "Direct output to a file" > file.txt

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

    cat file.txt

	cat <<EOF >cat_contents.txt
	all of this
	will go
	in my new file
	"cat_contents.txt"
	Until I type "EOF"
	to denote the End Of File
	EOF
	
### `less`

Display file contents within a buffer

**Examples**

    less cat_contents.txt

### `head`

Display first lines of a file

**Examples**

    head lipsum.txt

### `tail`

Display last lines of a file

**Examples**

    tail lipsum.txt

### `wc`

Count number of words, lines, characters in a file

**Examples**

	wc lipsum.txt

### `grep`

Search file for a specific word

**Examples**

    grep lorem lipsum.txt

	grep my_function -r code_dir

[Further reading](https://www.gnu.org/software/grep/manual/grep.html)

## Data manipulation <!-- If time permits -->

### `tr`

Substitue or delete selected characters from a file

**Examples**

    tr "f" "p" cat_contents.txt

    tr -d "\n" cat_contents.txt

### `cut`

Parse selected portions from lines of a file

**Examples**

    cut -d "," -f 3 Tree_Locations.csv > Trees.txt

## `sort`

**Examples**

    sort Trees.txt > Alphabetical_trees.txt

	sort -u Trees.txt > Unique_trees.txt

## The big guns

### `sed`

Short for "steam editor". Useful for string replacement, deletion and all around text processing.

Read the [manual](https://www.gnu.org/software/sed/manual/sed.html).

### `awk`

A full-fledged programming languange convienient for text processing on the command line.

Read the [manual](https://www.gnu.org/software/gawk/manual/gawk.html).

## Getting help

### `-h`/`--help`

Most command provide a help flag `-h` or `--help` that displays basic command usage.

### `man`

Display the manual for a command

**Examples**

    man less
    man grep
    man man

### `help`

Help for builtin commands

**Examples**

    help cd


## Combining commands with the Pipe operator `|`

A pipe, `|`, connects the output from one command to be used as the input to another command

**Examples**

	cat lipsum.txt | less

    cat Tree_Locations.csv | cut -d, -f3 | sort -u


# Loops and conditional execution <!-- 5 mins... if time permits -->

### `for` loops

The classic construct for iteration; convenient when iterating over items.

**Examples**

    for I in 0 1 2 3 4 5 6 7 8 9; do
	  echo $I
    done

### `while` loops

Another looping construst, convenient for iterating over lines of a file

**Examples**

	while read LINE; do
	  echo $LINE
    done < lipsum.txt

### `&&` operator

Optionally execute a second command based on success of first command

**Examples**

    ./successful_cmd && echo "success"  # success

    ./failure_cmd && echo "failure"  # No output


### `||` operator

Optionally execute a second command based on success of first command

**Examples**

    ./successful_cmd || echo "success"  # No output

    ./failure_cmd || echo "failure"  # failure

# Commands for web dev <!-- 10 mins -->

### `curl`

The de-facto standard for command line web requests

**Examples**

	curl www.example.com

	curl -o example.html www.example.com

    curl https://reqres.in/api/users/

### `http`

User-friendly http client, convenient for API development

**Examples**

	http https://reqres.in/api/users/

	http POST https://reqres.in/api/users/ first_name="Ryan A" job="Backend Extraordinaire" zip_code:=70119

[Further Reading](https://httpie.io/)

### `jq`

Flexible text processor for JSON

**Examples**

	echo '{"name": "Ryan A", "job": "Backend"}' | jq

	echo '{"name": "Ryan A", "job": "Backend"}' | jq .job

	http https://reqres.in/api/users/ | jq .data[].avatar

[Further Reading](https://stedolan.github.io/jq/manual/)

### `wget`

Utility for network file downloads

**Examples**

	wget "https://reqres.in/img/faces/1-image.jpg" -O image.jpg

# Additional techniques

### Variables

Variables can be used in the command line like in any programming language.

**Examples**

	STR="Hello, World."
	echo $STR

### Sub-shell

A subshell allows you to run a command within a command, using parentheses `()`.

**Examples**

	STR="Hello, World."
	echo "$(echo $STR | cut -d "," -f 1), Nola."

	for I in $(seq 1 10); do
      echo $I
    done

# Piecing it together

    for I in $(seq 1 10); do
      IMAGE_URL=$(http https://api.thedogapi.com/v1/images/search/ | jq .[0].url | tr -d '"')
      FILENAME=$(echo "${IMAGE_URL}" | cut -d "/" -f 5)
	  FILE_EXT=$(echo ${FILENAME} | cut -d "." -f 2)
      wget "${IMAGE_URL}" -O "image_${I}.${FILE_EXT}" -q
    done
