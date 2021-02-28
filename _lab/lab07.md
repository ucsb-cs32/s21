---
layout: lab
num: lab07	
ready: false
desc: "Practicing with development Tools: gdb and valgrind"
assigned: 2021-02-24
due: 2021-03-04 23:59
github_org_url: https://github.com/ucsb-cs32-w21
---

Goals
=====

Learning objectives. At the end of this lab, students should be able to:

- Use gdb to examine buggy C++ code
- Use valgrind to check for memory leaks

Modality
============
Per the modality announced, you may work on this lab in pairs, but really you each should consider this opportunity to learn gdb and valgrind.  This lab would work best with you each in parallel trying things out and talking.  You each really will want the opportunity to experience and practice with these tools.  Regardless, each person must fill out their own gradescope form.  Again, per the prior announcements on modality, you may only work with the same person twice.

Orientation
============

Even the most experienced programmers introduce bugs into their code, especially as the complexity of the code and data management for a larger system expand.  Most software development companies have many in house tools to help their developers.  In addition, there are several open source general tools that are useful to have experience with.  The primary goal of this lab is to expose you to these tools.  You will need to continue to practice with these tools throughout your computing career to truly learn them.

The tools we will play with this week include gnu's debugger gdb and valgrind.  These tools have different uses.  You are expected to understand some basics about all of them by doing some reading on your own.

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

Step by Step
============

## Step 1: gdb

The GNU debugger (a.k.a. gdb) is a very powerful tool for analyzing what your program is doing at run-time. 

There is a useful tutorial at the general CS32 course website (<https://ucsb-cs32.github.io>). Referring to this tutorial will directly help you respond to the first 4 questions for this lab.

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


## Step 2: Debugging someone else's code 

It's time to put your new skills to the test. You will be given an executable file, but not all the source code.

It is possible that you may have a program that calls a library and you won't be given all the source code to the library or the library was built without the -g option. Here we are reversing this a little bit. You are given some code, but the code to the main function is not given to you. You will not be able to step through all of the code. In a sense, you can treat main function like a 'black box', which calls the code you are given. You don't need to know what the main function is doing, but you will have to answer a few questions about how it calls the code you are given.

Download the 4 files from here:

* http://cs.ucsb.edu/~richert/cs32/misc/lab07/

Or copy from here:

* /cs/faculty/richert/public_html/cs32/misc/lab07/*

###  Guidelines for Answering 

Use the associated gradescope online tool to answer questions for this lab.  Note that this lab is about giving you experience with these tools.  'Cheating' really only cheats you of the opportunity to learn.


### Question 1

Start up `gdb` and load in `segProgram`.
```
gdb ./segProgram
```

Now run the program with the `run` command followed by your <b>umail address</b>:

```
(gdb) run cgaucho@umail.ucsb.edu
```

It will stop as soon as it encounters the segfault. Note that when you use the command `run [args]`, it takes `[args]` as the command line argument (i.e. the value of `argv[1]`). This is a necessary step in order to produce the answer Gradescope is expecting.

* <b>q1a: </b>What index of the array is the program trying to access? Write your answer in <code>q1 'free response'</code>. 
* <b>q1b: </b>What value is the program trying to store in the array when the fault occurred? Write your answer in file <code>q1 'free response'</code>

### Question 2

For the remainder of the questions use the debugProgram executable.

```
gdb ./debugProgram 
```
Remember to pass in your umail address when running through gdb in order to obtain the correct values.

```
(gdb) run cgaucho@umail.ucsb.edu
```

<b>q2: </b> What is the value of the string 'a' when debugFunction1 is called?
<br>Hint: use the <code>break</code> feature to stop the program 

### Question 3
<b>q3: </b> What is the value of the string 'a' when debugFunction1 is called a second time?

### Question 4
<b>q4: </b> How many recursive calls to recursiveFunction are in the backtrace (also called a stack trace) when variable <code> a == 100 </code> in `recursiveFunction`? Put your answer in <code>q4</code>.

<b>Hints: </b>
* Use `backtrace` (abbreviated `bt`), along with conditional breakpoints:  <code>break</code> <em>someplace</em> <code>if </code> <em>condition</em>
* What is the number of stack frames when the last instance of recursiveFunction is created?  You may need to page through them.
* Then think about how many of those stack frames are <em>actually</em> for the recursive function, as opposed to other functions that have been put on stack before or after.


## Step 3: Debugging given code (further gdb exploration)
Now grab the next set of files:

and execute the following commands:
```
% gdb example
...
(gdb) b example.c:33
(gdb) r
(gdb) print exp
(gdb) print *exp
(gdb) print exp->c
(gdb) print exp->other
(gdb) print *exp->other
(gdb) print exp->other->a
(gdb) c
(gdb) list
(gdb) back <----- how did we get here?
(gdb) quit
```
For 
### Question 5
Fill in the blank with what is printed here:
(gdb) print exp->other->a

### Question 6
Explain in your own words what is happening with this code:
(gdb) print exp->other->a

## Step 3: valgrind 

After you are comfortable using gdb and you have stepped through a few routines in your program now it's time to learn about valgrind. Consider reading the quickstart guide here: https://www.valgrind.org/docs/manual/QuickStart.html


....
Starting with the provided versions of lecture code.  Run valgrind on both version1 and version2
<pre>
valgrind --leak-check=full version1/a.out 300 300 out.ppm
valgrind --leak-check=full version2/a.out 300 300 out.ppm
etc...
</pre>
Again use the gradescope form to report on the difference between these two code bases.

Next, fix the code in version3 - you must leave the data as raw pointers (do not swap them to smart pointers). Note that it will be fairly straight forward to address many of the issues, however, one issue will require making sure that the correct destructor is used for each of the shapes.

-----
