# Linux awk

This repository demonstrate the usage of awk command in Linux.

## Why learn awk

- Awk is part of POSIX, so it is installed *everywhere*
- Many of the problems you face are text processing problems
- Awk is the gold standard of text processing tools
- People are impressed with those that use awk:D
- Awk will make you powerful...
- All *real* hackers use awk

 ## What is awk

- A powerful, succinct scripting language for text processing
- More formally, awk is a data-driven scripting language consisting of a set of actions to be taken against streams of textual data for purposes of extracting or transforming text, such as producing formatted reports
- Written by Alfred Aho, Peter Weinberger, and Brian Kernighan
- Initially developed in 1977
- Awk was significantly revised and expanded in 1985-88 into GNU Awk
- GNU Awk (gawk) written by Paul Rubin, Jay Fenlason, and Richard Stallman
- gawk is most widely deployed version
- gawk has been maintained solely by Arnold Robbins since 1994
- Brian Kernighan's nawk (New Awk) source was first released in 1993 unpublicized, and publicly since the late 1990's
- Many BSD systems use nawk to avoid the GPL license (but their users always install gawk;-)

[wiki](https://en.wikipedia.org/wiki/AWK)

## History of awk

Before Awk:
- Was preceded by sed, which was the scripting part of ed
- sed was the first powerful regex tool
- Used main loop and current line variables (awk expanded on this)
- awk was an evolution in the sed line-oriented approach

After Awk:
- awk's powerful regexes and also its limitations inspired Perl
- Perl in turn inspired beautiful languages like Ruby which inspired Elixir
- We have a lot to thank awk for! :D

## Usage

### Hello World

```bash
awk 'BEGIN{print "Hello, world!"}'
```

### Running an awk program

- awk 'program' input files
- awk -f progfile *input files*
- some_program | awk 'program'
- #!/usr/bin/env awk -f -> ./script.awk *.log

### Structure of an awk program

- pattern -> {action}
- awk scans a sequence of input lines one after another searching for lines that are matched.
- Every input line is tested against each pattern in turn
- For each match, the {action} is executed
- After every applicable {action} is executed, the next line is processed
- Action are enclosed in braces to distinguish them frmo the pattern
- Either the pattern or the action can be omitted
    - If the pattern is omitted, every line will match '{print $1}'
    - If the action is omitted, every matching line will be printed '/regex/'

### Awk patterns

- awk patterns are basically just "if" statements to decide to execute the action
- Decide if a match is True or False
- If True, execute the following Action
- If False, skip the action and proceed to test the next pattern with current line

1. BEGIN {statements}: The *statements* are executed once before any input has been read.
1. END {statements}: The *statements* are executed once after all input has been read.
1. expression {statements}: The *statments* are executed at each input line where the *expression* is true, that is, nonzero or nonnull.
1. /*regular expression*/ {statements}: The *statements* are executed at each input line that contains a string matched by the *regular expression*.
1. *compound pattern* {*statements*}: A compound pattern combines expressions with && (AND) , || (OR), ! (NOT), and parenthese; the *statements* are executed at each input line where the *compound pattern* is true.
1. pattern_1, pattern_2 {*statements*}: A range pattern matches each input line from a line matched by *pattern_1* to the next line matched by *pattern_2*, inclusive; the *statments* are executed at each matching line.

COMPARISON OPERATORS
Operator | Meaning
--- | ---
< | less than
<= | less than or equal to
== | equal to
!= | not equal to
\>= | greater than or equal to
\> | greater than
~ | matched by
!~ | not matched by

Examples | Explanation
--- | ---
NF < 10 | If number of Fields is less than 10, then true
NR <= 150 | If number records so far is less than or equal to 150, then true
$1 == "SomeString" | If first element is equal to SomeString, then true
$4 ~ /linux/ | If fourth element matched linux, then true
$5 !~ /awk/ | If fifth element does not matched awk, then true
$2/$3 >= 0.5 | If second element divided by thrid element is greater or equal to 0.5, then true

String-Matching Patterns
1. /regex/ : implies "$0 ~" meanings matching the entire current input line whether it contain a substring that matches by regex.
1. expression ~ /regex/ : Matches if the string value of expression contains a substring matched by regex.
1. expression !~ /regex/ : Matches if the string value of expression does not contain a substring matched by regex.

Any expression may be used in place of /regex/ in the context of \~ and \!~.

Escape Sequences
Sequence | Meaning
--- | ---
\b | backspace
\f | formfeed
\n | newline (line feed)
\r | carriage return
\t | tab
\ddd | octal value ddd, where ddd is 1 to 3 digits between 0 and 7
\c | any other character c literally (e.g. \\ for backslash, \" for ")

Range Patterns

- A range pattern consists of two patterns separated by a comma
- A range pattern matches each line between an occurrence of pattern 1 and the next occurrence of pattern 2 inclusive
- If no instance of the second pattern is subsequently found, then all lines to the end of the input are matched

Summary
Pattern | Example | Matches
--- | --- | ---
BEGIN | BEGIN | before any input has been read
END | END | after all input has been read
expression | $3 < 100 | line in which field is less than 100
string-matching | /Asia/ | line that contain Asia
compound | $3 < 100 && $4 == "Asia" | lines in which third field is less than 100 and fourth field is Aisa
range | NR==10, NR==20 | tenth to twentieth lines of input inclusive

### Action

- Executed if the pattern matches (if there was no pattern)
- Are much like a typical language (such as C)
- Have access to a number of built in variable
- Can create variables or call functions (such as print)
- Parenthesis in function calls are optional
- Can override fields or create new fields

The statements in actions can include: expressions, with constants, variables, assignements, function calls, etc.
1. print : expression-list
1. printf : format, expression-list
1. if (expression) statement
1. if (expression) statement else statement
1. while (expression) statement
1. for (expression; expression; expression) statement
1. for (variable in array) statement
1. do statement while (expression)
1. break
1. continue
1. next
1. exit
1. exit expression
1. {statements}

Variables
Variable | Meaning | Default Value
--- | --- | ---
ARGC | number of command-line arguments | -
ARGV | array of command-line arguments | -
FILENAME | name of current input file | -
FNR | record number in current file | -
FS | controls the input field separator | " "
NF | number of fields in current record | -
NR | number of records read so far (across all files) | -
OFMT | output format for numbers | "%.6g"
OFS | output field separator | " "
ORS | output record separator | "\n"
RLENGTH | length of string matched by match function | -
RS | controls the input records separator | "\n"
RSTART | start of string matched by match function | - 
SUBSEP | subscript separator | "\034"

Examples
```bash
# Print number of fields (columns)
awk '{print NF}'
```

```bash
# Print number of lines read (basically line numbers)
awk '{print NR, $0}'
```

```bash
# Print number of fields (columns)
awk '{print $1 "makes" $3 "per hour"}'
# or
awk '{printf("%s makes $%.2f per hour\n", $1, $3)}'

# Combine with other tools like sort and uniq
awk '{print $1 "makes" $3 "per hour"}' | sort -nk 3
awk '{print $1 "makes" $3 "per hour"}' | uniq -f 2
```

Math Functions
Function | Value Returned
--- | ---
atan2(y,x) | arctangent of y/x in the range of -PI to PI
cos(x) | cosine of x, with x in radians
exp(x) | exponential function of x, e^x
int(x) | integer part of x; truncated towards 0 when x > 0
log(x) | natural (base e) logarithm of x
rand() | random number r, where 0 <= r < 1
sin(x) | sine of x, with x in radians
sqrt(x) | square root of x
srand(x) | x is new seed for rand()

## Reference
- [link](https://www.youtube.com/watch?v=43BNFcOdBlY)