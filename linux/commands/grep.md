<pre>
You first need to create the following demo_file to use in the examples below to show grep command.
$ cat demo_file
THIS LINE IS THE 1ST UPPER CASE LINE IN THIS FILE.
this line is the 1st lower case line in this file.
This Line Has All Its First Character Of The Word With Upper Case.
Two lines above this line is empty.
And this is the last line.

1. Search for the given string in a single file
The grep command is basically used for searching for a particular string in the individual file as displayed below.
Syntax:
grep "literal_string" filename
$ grep "this" demo_file
this line is the 1st lower case line in this file.
Two lines above this line is empty.

2. Checking for the given string in multiple files.
Syntax:
grep "string" FILE_PATTERN
This is also a fundamental usage of grep command. Letâ€™s copy the demo_file to demo_file1. The grep output will also contain the file name in front of the line that corresponds the particular pattern as displayed below. When the Linux shell identifies the meta character, it does the expansion and offers all the files as input to grep.
$ cp demo_file demo_file1
$ grep "this" demo_*
demo_file:this line is the 1st lower case line in this file.
demo_file:Two lines above this line is empty.
demo_file:And this is the last line.
demo_file1:this line is the 1st lower case line in this file.
demo_file1:Two lines above this line is empty.
demo_file1:And this is the last line.

3. Case insensitive search using grep -i
Syntax:
grep -i "string" FILE
This is also a fundamental usage of the grep. This looks for the provided string/pattern case inconsiderately. Therefore, it matches all the words including 'the', 'THE' and 'The' case insensitively as displayed below.
$ grep -i "the" demo_file
THIS LINE IS THE 1ST UPPER CASE LINE IN THIS FILE.
this line is the 1st lower case line in this file.
This Line Has All Its First Character Of The Word With Upper Case.
And this is the last line.

4. Match regular expression in files
Syntax:
grep "REGEX" filename
This is a very strong feature, in case you can use make use of regular expression efficiently. In the example described here, it looks for all the pattern that begins with 'lines' and terminates with 'empty' with anything in-between. i.e To look for 'lines[anything in-between]empty' in the demo_file.
$ grep "lines.*empty" demo_file
Two lines above this line is empty.
From documentation of grep: A regular expression may be tracked by one of various repetition operators:
? The previous item is elective and matched at most once.
* The previous item will be matched zero or more times.
+ The previous item will be matched one or more times.
{n} The previous item is matched precisely n times.
{n,} The previous item is matched n or more times.
{,m} The previous item is matched at most m times.
{n,m} The previous item is matched at least n times, but not more than m times.

5. Checking for full words, not for sub-strings using grep -w
If you want to look for a word, and want to avoid matching to the substrings use -w option. Just doing out a normal search will display all the lines.
The example given below is the regular grep where it is searching for â€œisâ€. When you look for 'is', without any option it will display 'is', 'his', 'this' and everything which has the substring 'is'.
$ grep -i "is" demo_file
THIS LINE IS THE 1ST UPPER CASE LINE IN THIS FILE.
this line is the 1st lower case line in this file.
This Line Has All Its First Character Of The Word With Upper Case.
Two lines above this line is empty.
And this is the last line.
The example given below is the WORD grep where it is looking only for the word â€œisâ€. This output does not comprise the line 'This Line Has All Its First Character Of The Word With Upper Case', even though 'is' is there in the 'This', as the subsequent is looking only for the word 'is' and not for 'this'.
$ grep -iw "is" demo_file
THIS LINE IS THE 1ST UPPER CASE LINE IN THIS FILE.
this line is the 1st lower case line in this file.
Two lines above this line is empty.
And this is the last line.

6. Displaying lines before/after/around the match using grep -A, -B and -C
When doing a grep on a big file, it may be helpful to view some lines after the match. You might feel handy if grep can display you not only the matching lines but also the lines after/before/around the match.
Please produce the demo_text file for the example given below.
$ cat demo_text
4. Vim Word Navigation
You may want to do several navigation in relation to the words, such as:
* e - go to the end of the current word.
* E - go to the end of the current WORD.
* b - go to the previous (before) word.
* B - go to the previous (before) WORD.
* w - go to the next word.
* W - go to the next WORD.
WORD - WORD comprises of a sequence of non-blank characters, differentiated with white space.
word - word comprises of a sequence of letters, digits and underscores.
Example to show the difference between WORD and word
* 192.168.1.1 - single WORD
* 192.168.1.1 - seven words.
6.1 Display N lines after match
-A is the option which prints the particular N lines after the match as displayed below.
Syntax:
grep -A "string" FILENAME
The example given below prints the matched line, along with the 3 lines after it.
$ grep -A 3 -i "example" demo_text
Example to display the difference between WORD and word
* 192.168.1.1 - single WORD
* 192.168.1.1 - seven words.
6.2 Display N lines before match
-B is the option which prints the specific N lines before the match.
Syntax:
grep -B "string" FILENAME
When you had alternative to display the N lines after match, you have the -B option for the contrary.
$ grep -B 2 "single WORD" demo_text
Example to display the difference between WORD and word
* 192.168.1.1 - single WORD
6.3 Display N lines around match
-C is the option which prints the specific N lines before the match. 
$ grep -C 2 "Example" demo_text
word - word consists of a sequence of letters, digits and underscores.
Example to show the difference between WORD and word
* 192.168.1.1 - single WORD

7. Highlighting the search using GREP_OPTIONS
As grep prints out lines from the file by the pattern / string you had offered, if you wanted it to highlight which part matches the line, then you need to follow the following way.
In the example given below, it will highlight all this when you set the GREP_OPTIONS environment variable as displayed below.
$ export GREP_OPTIONS='--color=auto' GREP_COLOR='100;8'
$ grep this demo_file
this line is the 1st lower case line in this file.
Two lines above this line is empty.
And this is the last line.

8. Searching in all files recursively using grep -r
When you want to look for in all the files under the current directory and its sub directory. -r option is the one which you are required to use. The example described here will look for the string 'suresh' in all the files in the existing directory and all it's subdirectory.
$ grep -r "suresh" *

9. Invert match using grep -v
You had multiple options to display the lines matched, to exhibit the lines before match, and to demonstrate the lines after match, and to highlight match. So certainly, you'd also want the option -v to do capsize match.
When you want to show the lines which does not match the presented string/pattern, use the option -v as demonstrated here. This example will show all the lines that did not match the word 'go'.
$ grep -v "go" demo_text
4. Vim Word Navigation
You may want to do various navigation in relation to the words, including:
WORD - WORD comprises of a sequence of non-blank characters, differentiated with white space.
word - word comprises of a sequence of letters, digits and underscores.
Example to depict the difference between WORD and word
* 192.168.1.1 - single WORD
* 192.168.1.1 - seven words.
```

# 특정단어 제외하고 매칭 (grep 자신을 빼고 싶을 때)
```
ps -ef |grep httpd |grep -v grep
```


```
10. display the lines which does not matches all the given pattern.
Syntax:
grep -v -e "pattern" -e "pattern"
$ cat test-file.txt
a
b
c
d
$ grep -v -e "a" -e "b" -e "c" test-file.txt
d

11. Counting the number of matches using grep -c
When you need to count that how many lines match the provided pattern/string, you can use the option -c.
Syntax:
grep -c "pattern" filename
$ grep -c "go" demo_text
6
When you need do detect how many lines match the pattern
$ grep -c this demo_file
3
When you need do identify how many lines that do not match the pattern
$ grep -v -c this demo_file
4

12. Display only the file names which matches the given pattern using grep -l
If you want the grep to display only the file names which matched the given pattern, use the -l (lower-case L) option.
When you offer numerous files to the grep as input, it shows the names of file which comprises the text that matches the pattern, will be very handy when you try to identify some notes in your complete directory structure.
$ grep -l this demo_*
demo_file
demo_file1

13. Show only the matched string
By default grep will exhibit the line which matches the presented pattern/string, but if you want the grep to display only the matched string of the pattern then go for the -o option.
$ grep -o "is.*line" demo_file
is line is the 1st lower case line
is line
is is the last line

14. Show the position of match in the line
When you want grep to display the location where it matches the pattern in the file, go for the options described here as
Syntax:
grep -o -b "pattern" file
$ cat temp-file.txt
12345
12345
$ grep -o -b "3" temp-file.txt
2:3
8:3

15. Show line number while displaying the output using grep -n
To display the line number of file with the line matched. It does 1-based line numbering for each file. Use -n option to use this feature.
$ grep -n "go" demo_text
5: * e - go to the end of the current word.
6: * E - go to the end of the current WORD.
7: * b - go to the previous (before) word.
8: * B - go to the previous (before) WORD.
9: * w - go to the next word.
10: * W - go to the next WORD.

Via thegeekstuff.com 
</pre>
