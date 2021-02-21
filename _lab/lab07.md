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
- Use various performance metrics to measure different performance metrics (memory and timing)

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

Download the code.
Run gdb.
Answer some questions...

