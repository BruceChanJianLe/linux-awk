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


## Reference
- [link](https://www.youtube.com/watch?v=43BNFcOdBlY)