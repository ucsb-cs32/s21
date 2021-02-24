---
layout: lab
num: lab07	
ready: false
desc: "Practicing with development Tools: gdb, valgrind and performance"
assigned: 2021-02-24
due: 2021-03-03 23:59
github_org_url: https://github.com/ucsb-cs32-w21
---

Goals
=====

Learning objectives. At the end of this lab, students should be able to:

- Use gdb to debug buggy C++ code
- Use valgrind to check for memory leaks


Orientation
============

Even the most experienced programmers introduce bugs into their code, especially as the complexity of the code and data management for a larger system expand.  Most software development companies have many in house tools to help their developers.  In addition, there are several open source general tools that are useful to have experience with.  The primary goal of this lab is to expose you to these tools.  You will need to continue to practice with these tools throughout your computing career to truly learn them.

The tools we will play with this week include gnu's debugger gdb, valgrind, and some cross platform tools to measure timing (and possibly alternative performance tools, which tend to be OS dependent).  These tools have different uses.  You are expected to understand some basics about all of them by doing some reading on your own.

1) gdb is a debugger allowing you to examine the state of your program during execution (or at the moment it crashes): https://www.gnu.org/software/gdb/
"GDB can do four main kinds of things (plus other things in support of these) to help you catch bugs in the act:

    Start your program, specifying anything that might affect its behavior.
    Make your program stop on specified conditions.
    Examine what has happened, when your program has stopped.
    Change things in your program, so you can experiment with correcting the effects of one bug and go on to learn about another. 

Those programs might be executing on the same machine as GDB (native), on another machine (remote), or on a simulator. GDB can run on most popular UNIX and Microsoft Windows variants, as well as on Mac OS X."

A useful reference about gdb that we recommend you read: 
https://ucsb-cs32.github.io/topics/tools_gdb/

2) valgrind is a software analysis tool to detect memory management (and threading bugs) and profile your code. https://valgrind.org/

3)<maybe DRAFT> We will also play with various alternative performance tools (mostly timing) to experiment with alternatives for data management. i.e. to answer quested related to the cost of using shared_ptrs, references or instances of vectors.

Step by Step
============

*First 4 qs the same *

## Step 1: gdb

The GNU debugger (a.k.a. gdb) is a very powerful tool for analyzing what your program is doing at run-time. 

First read through the tutorial [tools: gdb](https://ucsb-cs32.github.io/topics/tools_gdb/) at the general CS32 course website (<https://ucsb-cs32.github.io>). <b>. Referring to this tutorial will directly help you respond to the first 4 questions for this lab.

In general to have the output of gdb be useful, you will need to compile with the `-g` option. Add `-g` to the `CXXFLAGS` in your `Makefile`. 

The order of flags on the `CXXFLAGS` line does not matter. You can add it to the end or the beginning.

```
CXXFLAGS = -g -std=c++11 -Wall -Wextra -Wno-unused-parameter -Wno-unused-private-field
```

Every time you change your `Makefile` you should always do a `make clean` first. Rebuild your tests.

Before moving on, may want to just experiment with each of the following gdb commands:

* `help`
* `break`
* `display`
* `print`
* `next`
* `step`
* `backtrace`
* `watch` 

There are examples for these commands on the [[tools: gdb]({{ page.tools_gdb_url }} page. Since you might not always know what you are looking for when debugging, experimentation is very important. 


CONVERT to GRADESCOPE ONLINE Q and A

## Step 3: Debugging someone else's code 

It's time to put your new skills to the test. You will be given an executable file, but not all the source code.

It is possible that you may have a program that calls a library and you won't be given all the source code to the library or the library was built without the -g option. Here we are reversing this a little bit. You are given some code, but the code to the main function is not given to you. You will not be able to step through all of the code. In a sense, you can treat main function like a 'black box', which calls the code you are given. You don't need to know what the main function is doing, but you will have to answer a few questions about how it calls the code you are given.

Download the 4 files from here:

* http://cs.ucsb.edu/~richert/cs32/misc/lab07/

Or copy from here:

* /cs/faculty/richert/public_html/cs32/misc/lab07/*

###  Guidelines for Answering 

To be sure that your answers pass the tests on Gradescope, be sure that you record them carefully.  The tests on Gradescope are very picky about filenames, formatting, etc.

* Do not add extra text to answers (e.g. reduce answers like <code>The answer is: x.</code> to only <code>x</code> )
* If a question asks for you to write a string "my string", do not include the quotation marks (e.g. "my string" => my string )
* All questions should be placed in separate files matching the question name (e.g. your answer to <code>q1a</code> should be placed in a file called <code>q1a</code>; DO NOT create <code>q1a.txt</code>, etc )
* If a question asks you to enter a number 5,000 only include the numbers (e.g. <code>5,000</code> => <code>5000</code>) 

### HINT: Suggestion for Creating the Answer Files

Use the echo command and redirect the output to a file. There is an example below. Note that the quotations in the echo command are not included in the file named 'testfile'. The cat command is just printing the file to the terminal so you can see that the contents were in fact written.

```
-bash-4.2$ echo "100" > testFile
-bash-4.2$ cat testFile
100
```

The source code we've given you is poorly written code. Take your time and look through it, but note that these are examples of code that should be rewritten. However, that is not your job today. Instead, you will use debugging tools to understand why these programs are failing. 

First run the `segProgram`, which is designed to segfault. 

```
./segProgram cgaucho@umail.ucsb.edu
Segmentation fault (core dumped)
```

`gdb` was designed to make handling segfaults trivial. Use `gdb` to pry into `segProgram` and discover the reason why it is crashing. When using `gdb`, make sure you run gdb from the same directory as the program you are analyzing (gdb relies on the current working directory as a path to find the source code). 

### Question 1 (q1a, q1b)

Start up `gdb` and load in `segProgram`.
```
gdb ./segProgram
```

Now run the program with the `run` command followed by your <b>umail address</b>:

```
(gdb) run cgaucho@umail.ucsb.edu
```

It will stop as soon as it encounters the segfault. Note that when you use the command `run [blah]`, it takes `[blah]` as the command line argument (i.e. the value of `argv[1]`). This is a necessary step in order to produce the answer Gradescope is expecting.

* <b>q1a: </b>What index of the array is the program trying to access? Write your answer in <code>q1a</code>. That's q-one-a, not q-L-a.
* <b>q1b: </b>What value is the program trying to store in the array when the fault occurred? Write your answer in file <code>q1b</code>

### Question 2 (q2)

For the remainder of the questions use the debugProgram executable.

```
gdb ./debugProgram 
```

Remember to pass in your umail address when running through gdb in order to obtain the correct values.

```
(gdb) run cgaucho@umail.ucsb.edu
```

<b>q2: </b> What is the value of the string 'a' when debugFunction1 is called?
<br>Remember to omit the quotation marks in your answer. Write your answer to a file named <code>q2</code>.
<br>Hint: use the <code>break</code> feature to stop the program 

### Question 3 (q3)

<b>q3: </b> What is the value of the string 'a' when debugFunction1 is called a second time?

<br>Remember to omit the quotation marks in your answer. Write your answer to a file named <code>q3</code>.

### Question 4 (q4)

<b>q4: </b> How many recursive calls to recursiveFunction are in the backtrace (also called a stack trace) when variable <code> a == 100 </code> in `recursiveFunction`? Put your answer in <code>q4</code>.

<b>Hints: </b>
* Use `backtrace` (abbreviated `bt`), along with conditional breakpoints:  <code>break</code> <em>someplace</em> <code>if </code> <em>condition</em>
* What is the number of stack frames when the last instance of recursiveFunction is created?  You may need to page through them.
* Then think about how many of those stack frames are <em>actually</em> for the recursive function, as opposed to other functions that have been put on stack before or after.

-----
## Step 2: valgrind 

After you are comfortable using gdb and you have stepped through a few routines in your program now it's time to learn about valgrind. Consider reading the quickstart guide here: https://www.valgrind.org/docs/manual/QuickStart.html


....
Starting with the provided versions of lecture code.  Run valgrind on both version1 and version2
<pre>
valgrind --leak-check=full version1/a.out 300 300 out.ppm
valgrind --leak-check=full version2/a.out 300 300 out.ppm
etc...
</pre>
Report on the difference between these two code bases.

Next, fix the code in version3 - you must leave the data as raw pointers (do not swap them to smart pointers). Note that it will be fairly straight forward to address many of the issues, however, one issue will require making sure that the correct destructor is used for each of the shapes.
