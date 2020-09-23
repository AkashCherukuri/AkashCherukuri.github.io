---
title: ""
permalink: /notes/cs251a_bash/
---

# Sed

---

`Sed` is a "Stream Editor". Meaning unlike a traditional editor, examination window is limited to a single screen. Sed is called as `sed <options> <script> input_files`. The line which `sed` is currently reading is loaded into the "pattern space". We then modify this line via the script, and then we either **hold** the line, or output the modified file. The modified line goes into `std::out`; but can be redirected.

### Passing Scripts to sed

`<script>` variable is passed either in-line enclosed within quotes, or with the `-f` option and writing the script in a text file and doing `sed -f <script file> input_files`.



## Regular Expression Syntax

---

- `/^x1/`: Search for lines beginning with `x1`



## Options

- `-n` : Don't print lines by default. That is, usually, `sed in.txt` would print all lines, and we don't want that. So, if we do `sed -n '/search/p' in.txt` would only print lines with the word "search". Similarly `sed -n '1,10 p' in.txt` would print the first 10 lines.
- `-s`: Treats independent files differently. Meaning, `sed -n '1,10 p' in1.txt in2.txt` would only apply the script to in1.txt and not in2.txt. But if we wanted to print the first ten lines of both, then this option is used. `sed -n -s '1,10 p' in1.txt in2.txt`
- `-r`: enables usage of extended regular expressions, for convenience
- `-e`: Allows grouping of commands together, example given below.

---

## Scripts

A script is of the form: `[address] [!] command`; `[]` represent that the argument is optional. If address is not given, command is applied for all lines. `!` is the `NOT` operator.



### Address Usage

- `sed -n '3 p' in.txt`: prints the third line
- `sed -n '$ p' in.txt`: Prints the last line
- `sed -n -e '10 s/__/  /' -e '10 p' in.txt`: in `s/__/  /`; `s` stands for replace, and here we replace '__' with '    '; after which that line is printed.
- `sed -n -r '/19D[0-9]{6}/ p' in.txt`: Print lines in the form "19D123456"

Using regular expressions, we can do some powerful stuff. Suppose, I wanted to print the lines before line 15, which started with the word `engi`; we do this as `sed -n -r '/^engi/,15 p' in.txt ` and to print all statements which are between lines starting with `x1` and `x2`; `sed -n -r '/^x1/,/^x2/ p' in.txt`

**Nesting** is done using the curly braces `{}`; for example, to show all statements between lines 4 and 20 beginning with `x1` is done as `sed -n -e '4,20{^x1 p}' in.txt`



### Commands

- `=` : print the line number and `p`: print the line

### Modify Commands 

- Insert `i\`: Used to insert the given string before the line address. `sed '10 i\ /'This string is inserted at line 10'/' in.txt `

- Append `i\`: Similar to insert, but the new line is AFTER the given line number. Insert and append dont work for ranged addresses.

- change `c\`: Change the entire matched line with given text. `sed -n -r '/19D[0-9]{6}/ c\ Dual Degree' in.txt` would change entire row to just "Dual Degree"

- delete `d\`: Similar to Change, but deletes the entire line. Can be used for all types of addresses.

- Substitute `s`: 

  `s/x1/x2/[flags]`; replaces the first occurrence of `x1` with `x2`. If `/g` (global) is passed into flag; all occurrences are removed.

  `&`:   To find `x1`, and replace with `x1+x2`; do `sed -n 's/x1/&x2/' in.txt`

  `n\`:  Suppose we wanna replace "Blue is very sus" to "Red is not sus" (Imagine we have roll no instead of colours and using -r)  `sed 's/Blue( is )very( sus)/Red\1not\2' in.txt`; `\1` holds the value in the first parentheses and so on.

- Transform `y` Syntax: `[address1],[address2]y/x1/x2/ `: replace occurrences of `x1` with `x2`; **x1 and x2 must have same length**

### I/O Commands

- `n`: (default) Read a line, without `\n` char, execute commands, print if `-n` is not used
- `N`: Read a line, **add a newline**, add to pattern space and execute. Used to join lines. `sed -r 'N; s/\n//' in.txt`; joins lines 1,2; 3,4 and so on
- `p`: Copies entire pattern space to output                 `P`: Prints only the first line of the pattern space
- `h`: Overwrites pattern space onto hold space          `H`: Appends pattern space to hold space (pattern space unchanged in both)
- `g`: Overwrites hold space onto pattern space           `G`: Appends hold space to pattern space(hold space unchanged in both)
- `d`: deletes pattern space
- `r filename`: reads file and sends to output. The file is not passed to pattern space.
- `w filename`: writes to the file from the pattern space
- `b`: Similar to `goto` statement; can be used for if-else statements ig, usage given below
- `q`: Quit reading the file



## Script Writing

```bash
#!/bin/bash
#just put each indiv word in a new line
sed -n -r '
/19D[0-9]{6}/ b save	#branch to save; otherwise continue
	w others.txt
	b					#branch to end
	
	:save
	w dd-students.txt
'
in.txt

```





# Awk

---

Scans every line, splits each line into field, compare fields to pattern, perform action. The difference between `awk` and `sed` is that `awk` has capability to remember history between files. The syntax of the script is very similar to C.

```bash
#Basic Awk Syntax
awk [options] 'script' file(s)			#Direct console
awk [options] -f scriptfile file(s)		#input via file
```

The script part is as follows: `pattern [action]`; if `pattern` is missing then action is done for all lines, and if `action` is missing, then matched line is printed. **Either pattern or action must be given.**

A line is divided into fields by `awk` by using a delimiter (default - `whitespace`); and each of these fields can be accessed by using variables, `$1` refers to the first field and so on.



## Pre-Defined Variables

- `FS` -- Field Separator, default: whitespace
- `RS` -- Record Separator, default: newline
- `NF` -- Number of fields in current record
- `NR` -- Number of the current record -- idx
- `OFS` -- Output Field Separator, default: whitespace
- `FILENAME` - Current Filename

```bash
ls -al | awk '{print NR, $9}'		#Print all files with numbering
```

## 

## Script structure

The scripts are divided into three parts; BEGIN, BODY, END. The statements in BEGIN are executed once(declare variables and stuff), the ones in BODY are executed for every line, and the statements in END are executed once at the end of the file (post processing).

```bash
#Structure of Body
pattern {statement}
pattern {statement; statement; ...}
pattern {
	statement
	statement
	...
}
```



## Pattern Types

- `awk '/special/ {print}'`: prints the lines with the word "special".

- Instead of this, we can check if the field matches a regular expression as: `awk -F, '$1~/19D[0-9]{6}/{print NR, $0}'`; meaning if the student is dd, then print his name with numbering. 

- `~` stands for Matching; and `!~` stands for not matching in this case

- However, they need just be pattern matching; we can use boolean arguments as well such as `$1 + $2 > 5 {statement}`



## Expressions

```bash
#We are feeding the input from wc -c *; in which the first variable is the number of characters of the given line
awk '
BEGIN{
	lines=0; char=0;
}
{
	lines++; char+=$1;
}
END{
	print lines, " lines read";
	print "Total characters: ",char;
}
'
```



### Passing Variables to awk

To pass the variables from the shell script to the awk script, use the flag `-v`; as:- `awk -v var1="$shell_var" '{script}'`



## Associative Arrays

No need for pre-allocating, they get defined with use.

```bash
awk -F, '
	#($9~/[A-Z][A-Z]/){
		state[$9]+=$10
	}
	END{
		for(i in state){
			print state[i], i;
		}
	}
'
```



## Output Statements

- `print`: simple w/o no formatting
- `printf`: print with formatting
- `sprintf`: format a string

