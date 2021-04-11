---
layout: lab
num: lab02	
ready: true
desc: "Practicing with development Tools: gdb and valgrind"
assigned: 2021-04-14
due: 2021-04-21 23:59
github_org_url: https://github.com/ucsb-cs32-s21
---

Goals
=====

Learning objectives. At the end of this lab, students should be able to:

- Use gdb to examine and fix buggy C++ code
- Use valgrind to check for memory leaks and explore memory use

Modality
============
Solo

Orientation
============

Even the most experienced programmers introduce bugs into their code, especially as the complexity of the code and data management for a larger system expand.  Most software development companies have many in house tools to help their developers.  In addition, there are several open source general tools that are useful to have experience with.  The primary goal of this lab is to expose you to these tools.  You will need to continue to practice with these tools throughout your computing career to truly learn them.

The tools we will play with this week include gnu's debugger gdb and valgrind.  These tools have different uses.  You are expected to understand some basics about all of them by doing some reading on your own.

1) gdb is a debugger allowing you to examine the state of your program during execution (or at the moment it crashes): https://www.gnu.org/software/gdb/
"GDB can do four main kinds of things (plus other things in support of these) to help you catch bugs in the act:

    Start your program, specifying anything that might affect its behavior.<br>
    Make your program stop on specified conditions.<br>
    Examine what has happened, when your program has stopped.<br>
    Change things in your program, so you can experiment with correcting the effects of one bug and go on to learn about another. <br>

    Those programs might be executing on the same machine as GDB (native), on another machine (remote), or on a simulator. GDB can run on most popular UNIX and         Microsoft Windows variants, as well as on Mac OS X."

A useful reference about gdb that we recommend you read: 
https://ucsb-cs32.github.io/topics/tools_gdb/

2) valgrind is a software analysis tool to detect memory management (and threading bugs) and profile your code. https://valgrind.org/

Step by Step
============
