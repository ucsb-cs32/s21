---
layout: lab
num: lab00	
ready: true
desc: "Review of C++ basics, Makefiles, start thinking about data, and Gradescope"
assigned: 2021-03-30 
due: 2021-04-07 23:59
github_org_url: https://github.com/ucsb-cs32-s21
---

Goals
=====

By the time you have finished this lab, you should have demonstrated
your ability to:

-   Join the Github Organization <{{page.github_org_url}}> 
-   Use some basic Unix commands, and learn about new Unix commands
-   Create a basic Makefile from scratch
-   Do some simple C++ programming as review of C++ basics, and as
    preliminary work towards understanding testing and arrays
-   Do some simple editing of base code related to lecture project
-   Submit work using the Gradescope system

Step by Step
============

Step 0: Getting Started
-----------------------

### Step 0a: Make sure you have a CSIL account and know how to use it

Ideally, before this lab begins, you will have been instructed to visit
the link below, and create your "College of Engineering" computer
account:

-   <https://accounts.engr.ucsb.edu/create>

<strong>You should already know the following from CS16 / CS24. If not, alert your TA/instructor immediately:</strong>

-   How to login to `csil.cs.ucsb.edu` with your CoE/CSIL account


### Q: Can I work on my own computer? A: likely (you will need to work out the final details)

You have a choice about how to work remotely.  You can either set up your own individual working environment (i.e. work locally on your machine).  However, you will always need to test your code on the CSIL machines.  Or you can remotely access the CSIL machines and work remotely logged into CSIL. In lecture, I will give VERY brief demonstrations of how to access the CSIL machines over the internet.

You will definitely need to be comfortable working on CSIL and transferring files between your local machine and CSIL (if you are choosing to work locally). You are welcome to work independently to set up your development environment on your own machine (you will likely want this eventually).  Otherwise you can access CSIL over the internet from your own machine.

At the links below, we a "best effort" introduction to "how to do work
on your own computer", and then you will need to work on your own or with your classmates to set up your own machine.

-   There is no guarantee that this will always work.
-   There are two many different OS versions, flavors, configurations, etc.for us to know the ins and outs of every single one.
-   If/when you run into difficulties there, we cannot be your tech support. If you have a simple question and we know the answer, we'll tell you, but if you don't, our answer will be: "ok, then do your work in CSIL until you figure it out."

So, please be aware:

-   The primary computing environment for this course is the Linux environment on `csil.cs.ucsb.edu`
-   Though many labs can be done from your own computer, there may be some that require you to work on
    the `csil.cs.ucsb.edu` linux systems.

### Step 0b: Adding yourself to our GitHub organization

We will be using github.com in this course. We have created an organization on github.com
<{{page.github_org_url}}>
where you can create repositories (repos) for your assignments in this course.
You may be familiar with GitHub organizations from CS 16 and 24.
The advantage of creating private repos under that organization is that the course staff
(your instructors, TAs and mentors) will be able to see your code and provide you with help,
without you having to do anything special.

To join this organization, you need to do four things.

1. If you don't already have a github.com account, create one on the "free" plan.
2. If you don't already have your `@ucsb.edu` or `@umail.ucsb.edu`
   email address associated with your github.com account, go to
   "settings", add that email, and confirm that email address.

3. Visit <https://ucsb-cs-github-linker.herokuapp.com> and login with
   your github.com account. Click "Home", find this course, and click the
   "join course button". That will automatically send you an invitation
   to join the course organization. There is a link to the invitation for
   the GitHub organization for this course
4. Click on the invitation link and accept it. You can also go straight to <{{page.github_org_url}}>
   and accept the invitation there.

If you are not familiar with git, I highly recommend learning this
skill since this will be extremely valuable when collaborating on
large software projects. More information on git can be found here:
<https://ucsb-cs32.github.io/topics/git/>.

<b> IMPORTANT NOTE! </b>

You can create your own repos under this organization when working on
your labs. However, be sure to create your repo as *private*, since if
it's public, then anyone can view its contents. Since all students are
responsible for their own work, having your solutions visible to
everyone creates a situation that is considered to be a form of
academic dishonesty.

If there are any issues or questions, please post them on Piazza and
include any relevant screenshots, which may help us investigate any
issues.

### Step 0c: Creating your Gradescope account

We will use gradescope for *some* of the labs this quarter, not all.
Pay attention to whether an assignment is submitted to gradescope or github!

*This lab will be auto graded with gradescope.*

I have manually added everyone (using your UCSB email accounts)
currently enrolled in the course to the Gradescope system. You should
have received an email from the Gradescope system asking you to create
a password. Once you follow the instructions to set your password, you
should have access to the autograding system. You should see "CMPSC
32" in your courses for this quarter.

The lab assignment "Lab00" should appear in your Gradescope dashboard in CMPSC 32. 


### Step 0d: On CSIL, create your `~/cs32/lab00` directory

Create a `~/cs32/lab00` directory and make it your current directory. You
should already know how to do this from previous courses, but in case you need a reminder:

```
    mkdir ~/cs32
    mkdir ~/cs32/lab00
    cd ~/cs32/lab00
```

You are responsible for knowing the `mkdir` and `cd` commands—though these should be review, so they will not be covered in detail. Questions about their use, however, appear on any exam in this course. So if, up to this point, you've just "followed the instructions" without really understanding what you are doing, the time for that has passed.

The "shell" is the program that you type Unix commands into—commands such as mkdir, cd, etc.

The tilde symbol (`~`) stands for "the user's home directory", but only in the shell. There are many contexts where you cannot use the `~` symbol—in fact, almost everywhere other than the Unix command line that a filename is needed, you actually CANNOT use the tilde.

Step 1: Copying some programs
-----------------------------

Visit the following web link—you may want to use "right click" (or "control-click" on Mac) to bring up a window where you can open this in a new window or tab:

<http://cs.ucsb.edu/~richert/cs32/misc/lab00/>

You should see a listing of several C++ programs. We are going to copy those into your `~/cs32/lab00` directory all at once with the following command:

```
cp ~zjwood/32Public/lab00/* ~/cs32/lab00
```

Note: If you get the error message:

```
cp: target '/cs/student/youruserid/cs32/lab00' is not a directory
```

then it probably means you didn't create a `~/cs32/lab00` directory
yet. So do that first. The `*` symbol in this command is a
"wildcard"&mdash;it means that we want all of the files from the
source directory copy be copied into the destination directory namely
`~/cs32/lab00.`

After doing this command, if you `cd` into `~/cs32/lab00` and use the
`ls` command, you should see several files in your `~/cs32/lab00`
directory — the same ones that you see if you visit the link
<http://cs.ucsb.edu/~richert/cs32/misc/lab00/> If so, you are ready to
move on to the next step. If you don't see those files, go back
through the instructions and make sure you didn't miss a step. If you
still have trouble, ask your TA and/or mentor for assistance.

Step 2: Learn how to learn about some basic Linux commands
----------------------------------------------------------

The `man` program can be used to find out details about commands,
programs, standard library functions, and anything else for which a
man page has been created. You just used `mkdir` and `cd` without any
options, so why not learn more about those commands right now. First
type:

    man mkdir

With `man`, the space key moves to the next page, and `q` quits. Notice that `mkdir` is a utility (program) to create directories, and it has three options available:

-   `-m` to set the new directory's permission bits (mode),
-   `-p` to create any necessary intermediate parent directories on the path
-   `-v` to be "verbose" about it.

Try making a directory tree without specifying the -p option, for example:

    bash-4.2$ mkdir one/two/three
    mkdir: cannot create directory `one/two/three': No such file or directory

Oops. Let's try it again with -p, and also use the -v option to hear the details:

    bash-4.2$ mkdir -p -v one/two/three
    mkdir: created directory `one'
    mkdir: created directory `one/two'
    mkdir: created directory `one/two/three'

Aaah ... much better, and so informative!

Now learn some more about `cd` as follows:

    man cd

Uh oh ... it seems that `cd` is a built-in shell command, not a program, and it does not have its own man page. If you spacebar down a ways though, you will find a section that starts out as follows:

    cd [-L|-P] [dir]
           Change  the  current directory to dir. ...

That's all you really need to know in this case, which is a good thing since the rest of the text for this command is not very helpful (-L and -P both relate to symbolic links). Some built-in commands do have their own pages though, and so man is usually a good place to start looking for information. By the way, before going to Step 3, learn more about man as follows:

    man man

Step 3: Reviewing Makefiles
---------------------------

We are now going to create a Makefile.

In many previous labs in CS16 and CS24, you may have copied your Makefile from the instructors directory. However, for this lab, you are going to make it yourself from scratch.

### Step 3a: Specifying which C++ compiler to use

The first thing we should do is edit our Makefile using emacs or vim, or whatever text editor you prefer. For example:

-   `emacs Makefile`, OR
-   `vim Makefile`

On the first line of the file, put this, substituting your name  for YOUR NAME(S) HERE, as appropriate:

    # Makefile for lab00, YOUR NAME(S) HERE, CS32, W21

Then, leave a blank line, and add the following two lines shown here, so that you end up with this as the first four lines of your Makefile:

    # Makefile for lab00, YOUR NAME(S) HERE, CS32, W21

    CXX=clang++
    # CXX=g++

<div style="margin:5px; border: 8px inset #ccc; padding:3px; font-size:80%;">
What is a *toolchain*

A *toolchain* refers to a set of tools that you use in some programming environment to get your work done. It typically includes a compiler, but may also include:

-   an editor
-   a linker for creating executables
-   a tool for creating libraries (combining compiled code from multiple
    files into a single file)
-   when compiling on one system and running on another (e.g. development for the Arduino, Android, iPhone, etc.), a tool to transfer the compiled software to the target device.
-   a debugger
-   a profiler (tool to help find where your program is spending most of its cpu time ("hotspots"), or to find memory leaks).

Both GNU and LLVM provide toolchains for working with C++ on Unix. The iOS products (iPhone/iPad/iPod) have their own toolchain, as do platforms such as Android and Arduino.

</div>
There are at least four important concepts about Makefiles to take away here:

1.  The pound sign (`#`) is used to start a comment in a Makefile. That comment extends from the pound sign to the end of the line.
2.  Anytime you have `VARIABLE_NAME=value` in a Makefile, you are defining a variable.
3.  The variable `CXX` is special—it is the variable that by default, indicates which compiler should be used for compiling C++ programs.
4.  There are two commonly used C++ compilers that you should be aware of: g++ (the C++ compiler from the GNU *toolchain*) and clang++ (the C++ compiler that is part of the LLVM *toolchain*). For more information on what a toolchain is, see the discussion at the right hand side of the page.

So what these lines of code do is this:

| Makefile code | Explanation |
| -- | -- |
|  `# Makefile for lab00...`   | comment documenting what the Makefile is for |
| `CXX=clang++`                | The clang++ compiler will be used to compile C++ programs |
|  `# CXX=g++`                 | If you want to switch to the g++ compiler for some reason, you can uncomment this line and comment out the `CXX=clang++` line. |

### Step 3b: Add a rule to link a helloWorld program

In the step of this lab where you copied files into your directory, one
of the files you copied in was a simple HelloWorld.cpp program. Take a
moment to look at the source code of that program, using the Unix `more`
command:

    -bash-4.2$ more helloWorld.cpp

The only reason this simple program is here is so we can practice
setting up a rule in the Makefile, from scratch, to compile a simple
program. Here is what that rule will look like. Add it below the lines
we already have, as shown here.

Two important things:

-   Note that the first of the two lines that we are adding MUST start
    in the leftmost column.
-   The second of the two lines MUST start with a TAB character, NOT
    spaces.
-   Because of the TAB vs. Spaces thing, copying and pasting this WILL
    NOT WORK. At the very least, if you copy and paste, you need to
    delete the spaces in front of `${CXX}` and replace them with a
    single TAB character.

<!-- -->

    # Makefile for lab00, YOUR NAME(S) HERE, CS32, W21

    CXX=clang++
    # CXX=g++

    helloWorld: helloWorld.o
            ${CXX} helloWorld.o -o helloWorld

What do these two lines mean?

-   The first part of the first line, `helloWorld: helloWorld.o` defines
    the start of a <em>target</em>. The part that comes before the
    colon, `helloWorld` is the name of the target, and is a file that we
    want to <b>make</b>. We make this file by typing <b>make
    helloWorld</b> at the Unix command line. The file `helloWorld` is
    going to be our executable program.
-   The second part of the second line, the part <em>after</em> the
    colon, `helloWorld.o`, indicates a list of files that the target
    depends on. In this case, the executable program `helloWorld`
    depends only on the file `helloWorld.o`.
-   `${CXX}` is replace with the name of the C++ compiler (either
    clang++ or gnu++) by dereferencing the symbol `CXX`. We call this
    <em>dereferencing</em> because like the `*` operator used with
    pointers in C/C++, the `$` in a Makefile indicates that instead of
    using the letters `CXX`, the Makefile should use <em>what they refer
    to</em>, i.e. the value of the variable `CXX`.
-   The command `${CXX} helloWorld.o -o helloWorld` therefore turns into
    either `clang++ helloWorld.o -o helloWorld` or
    `g++ helloWorld.o -o helloWorld` depending on the value of the
    symbol `${CXX}`,

### Step 3c: Adding a rule to compile helloWorld.cpp to helloWorld.o

Now it turns out that helloWorld.o is a file we do not have in our
directory at the moment. The following rule is one that will create
that, so add this to our Makefile next. Remember that you need to use a
TAB character on the indented lines, not spaces; so copying and pasting
this WILL NOT WORK.

Leave a blank line after your rule for the `helloWorld` target, and add
these two lines to your Makefile:

    helloWorld.o: helloWorld.cpp
            ${CXX} -c helloWorld.cpp

Now we are ready to test this all out. That's what we'll do in the next
step.

### Step 3d: Testing our Makefile so far

To test what we have so far:

\(1) Save your Makefile, and return to the Unix prompt.

\(2) At the Unix prompt, type `make helloWorld` and you should see output
like the following:

    -bash-4.2$ make helloWorld
    clang++ -c helloWorld.cpp
    clang++ helloWorld.o -o helloWorld
    -bash-4.2$ 

\(3) You can now run the helloWorld program by typing `./helloWorld` as
we have done all along throughout CS16 and CS24. Try that now:

    -bash-4.2$ ./helloWorld
    Hello, World!
    -bash-4.2$ 

\(4) Now, if type `make helloWorld` again, we should see the following
output. Do that now. Notice it is different from before:

    -bash-4.2$ make helloWorld
    make: `helloWorld' is up to date.
    -bash-4.2$ 

\(5) Now, edit your helloWorld.cpp program, changing the program by
adding a comment with your name(s) between the first two comments:

    // helloWorld.cpp  Z. Wood for UCSB CS32 W21
    // Edited by: YOUR NAME(S) HERE
    // minimal Hello World! program for testing Makefiles

Save the change.

\(6) Although this change doesn't really affect the program, it is enough
for the Make utility to see that the file has been changed. If we now
type `make helloWorld` again, we'll see that the program is recompiled:

    -bash-4.2$ make helloWorld
    clang++ -c helloWorld.cpp
    clang++ helloWorld.o -o helloWorld
    -bash-4.2$ 

\(7) <b>Here is what you need to understand, both to work with make, and
for your <em>exams</em> in this course:</b>

-   The make utility works from timestamps and dependencies to figure
    out what does—or does not—need to be relinked and/or compiled.

So, based on the rules:

    helloWorld: helloWorld.o
            ${CXX} helloWorld.o -o helloWorld

    helloWorld.o: helloWorld.cpp
            ${CXX} -c helloWorld.cpp

We have this chain of dependencies:
`helloWorld.cpp`→`helloWorld.o`→`helloWorld`.

-   Here, I'm showing an arrow pointing in the direction in which make
    needs to make the files.
-   For example, if the makefile has `b: a` it means b depends on a, and
    we write a→b to show that we need a's timestamp to be earlier than
    b's timestamp. If a has a later timestamp than b, it means that b is
    "out of date" and needs to be remade.
-   Another case is the case where if b does not exist at all (e.g. if
    if has never been made at all, or if has been deleted since it was
    last made.) In that case, we also need to remake b, typically using
    a as the input file.

After constructing the dependencies, the make program then looks to see
which files already exist (or not), and what the time stamps are, and
executes the necessary commands in the order needed.

That is why the result, when we make a change to helloWorld.cpp is that
the rules are done in this order:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg .tg-fymr{font-weight:bold;border-color:inherit;text-align:left;vertical-align:top}
.tg .tg-7btt{font-weight:bold;border-color:inherit;text-align:center;vertical-align:top}
.tg .tg-0pky{border-color:inherit;text-align:left;vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-fymr">What we see</th>
    <th class="tg-7btt">Explanation</th>
  </tr>
  <tr>
    <td class="tg-0pky">-bash-4.2$ make helloWorld</td>
    <td class="tg-0pky">we type `make helloWorld` to make the executable, and make constructs the dependency chain `helloWorld.cpp`→`helloWorld.o`→`helloWorld`</td>
  </tr>
  <tr>
    <td class="tg-0pky">clang++ -c helloWorld.cpp</td>
    <td class="tg-0pky">From the dependency chain, this is the first thing that must be done. It must be done because helloWorld.cpp is "newer" than helloWorld.o. The command recompiles `helloWorld.cpp` into `helloWorld.o`—the `-c` flag indicates "compile only; do not link", so we get a helloWorld.o file as the result.</td>
  </tr>
  <tr>
    <td class="tg-0pky">clang++ helloWorld.o -o helloWorld</td>
    <td class="tg-0pky">This is the link step. It is done because NOW helloWorld.o, which is newly remade from the previous step, is NOW newer than the executable helloWorld. The command relinks the helloWorld.o code (the machine language version of ONLY the code from the helloWorld.cpp file) with the machine language versions of the code in the standard libaries (e.g. the code for the iostream library that provides cout, endl, among other things.) The result of this command is a new version of the executable file `helloWorld`</td>
  </tr>
  <tr>
    <td class="tg-0pky">-bash-4.2$</td>
    <td class="tg-0pky">The bash prompt indicates that the command is complete and the shell is ready for our next command.</td>
  </tr>
</table>
<p></p>

So what should you know from this for your exams? These items suggest
a few of things you might be asked about.

-   Be able to explain the difference between Makefile commands that
    compile, vs. commands that link.
-   From this step of this lab, be able to write the syntax of Makefiles
    commands for compiling and/or linking a simple standalong C++
    program. (Later we'll also learn how to write Makefiles for complex
    program consisting of multiple source files.)
-   Be able to explain how Makefiles construct a chain of dependencies
    based on timestamps to determine what needs to be recompiled or
    relinked.
-   Be able to explain the variables such as `CXX` are dereferenced when
    the `$` is put in front of them, and they are surrounded by braces.

### Step 3e: Adding a rule for `make clean`

Sometimes we may want to remove all of the executable and .o files from
our directory. As you may recall from Makefiles that were supplied to
you in CS16 and CS24, that is traditionally done with a `clean` target
that allows us to type `make clean`.

Here are some examples of when that is appropriate:

-   When we are switching from one compiler to another, e.g. from
    clang++ to g++—the .o files produced by one compiler are not
    compatible with the other.
-   When we have made signficant changes to the interface between
    multiple parts of a program that uses separate compilation, i.e.
    multiple .cpp files (and hence .o files). By "interface", here we
    typically mean the .h files that specify definitions of structs,
    classes, and function prototypes. If those have changed, a "make
    clean" may be a good idea.
-   If we are about to copy the files to another directory (e.g. to
    share with a pair partner), or if we are finished with a project and
    want to save disk space. We really only need the source files (.h,
    .cpp and Makefile). The .o and executable files can always be remade
    if/when they are needed.

A clean rule looks like this, and is typically at or near the end of
your Makefile. Add this to your Makefile now. Note that the second line
starts with a tab, and that there should be a blank line after your
rule.

    clean: 
            /bin/rm -f *.o helloWorld

`make clean` <b>almost</b> always runs the `clean` rule. In general, any
Makefile target with no files specified after the colon is always run
when it is invoked. Technically, there is one exception: when there is a
file that has exactly the same name as the rule in the file. So it is
best to avoid having any executable or other file with the exact name
`clean`. In such a case, the `make clean` rule would <em>never</em> be
invoked. That's what we call a <em>corner case</em>—it rarely happens in
practice, but is possible in theory, so its good to keep in mind.)

The fact that this rule has `clean:` as the first line with
<em>nothing</em> after the colon (`:`) means that `clean` does not
depend on anything. That has a special meaning in a Makefile—it means
that <em>every</em> time we invoke `make clean`, the commands following
the first line of the rule will <em>always</em> be executed. (Well,
almost always. See the note at right for an exception.)

So `make clean` always results in the command
`/bin/rm -f *.o helloWorld` being executed, which removes all .o files
(the `*` being a <em>wildcard</em> that matches any filename.

Why`/bin/rm -f` rather than just `rm`?

-   `/bin/rm` specifies exactly what version of the rm program (the Unix
    delete program) to use. This is generally safer, in case someone has
    redefined `rm` to do something different than we might expect.
-   The `-f` option stands for <em>force</em> and says "do this even if
    there is a problem". A problem might be, for example, that there
    aren't any .o files or helloWorld files to remove. Without the `-f`
    option, the `/bin/rm` command might given an error message. With
    that option, it just works and doesn't complain.

### Step 3f: Testing the `make clean` rule

    -bash-4.2$ make clean
    /bin/rm -f *.o helloWorld
    -bash-4.2$ make helloWorld
    clang++ -c helloWorld.cpp
    clang++ helloWorld.o -o helloWorld
    -bash-4.2$ make helloWorld
    make: `helloWorld' is up to date.
    -bash-4.2$ 

Now let's test it out. Run `make clean`, then run `make helloWorld`
twice.

Your output should look like what you see at right.

-   You will see that when we type `make clean`, the
    `/bin/rm -f *.o helloWorld` command is executed.
-   When we type `make helloWorld` the <em>first</em> time, the commands
    to compile and link are executed.
-   When we type `make helloWorld` the <em>second</em> time, we get a
    message that `` `helloWorld' is up to date. ``. This is because make
    examined the whole dependency chain
    (`helloWorld.cpp`→`helloWorld.o`→`helloWorld`), and found that
    nothing needed to be done—all of the files needed were present, and
    all the timestamps were in the correct sequence.

Be able to predict how typing `make clean` will affect what happens when
make commands are invoked, and be able to explain why.

Step 4: Adding rules to support separate compilation
----------------------------------------------------

Now that we have practiced a bit on some simple Makefile rules for a
"Hello, World!" progam, we are ready to put in some Makefile rules for
something a bit more complex. In this weeks program, we are working with
some code that is basically review from CS16, but will set us up for
some of the advanced material we'll be covering in CS32. This code deals
with simple arrays in C++, finding min and max, and differentiating
between index and value. So, nothing too complicated.

The code is in the following source files:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:black;}
.tg .tg-baqh{text-align:center;vertical-align:top}
.tg .tg-7btt{font-weight:bold;border-color:inherit;text-align:center;vertical-align:top}
.tg .tg-amwm{font-weight:bold;text-align:center;vertical-align:top}
.tg .tg-0lax{text-align:left;vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-7btt">Filename</th>
    <th class="tg-amwm">Purpose</th>
    <th class="tg-amwm">Do I need to modify this file?</th>
  </tr>
  <tr>
    <td class="tg-0lax">arrayFuncs.cpp</td>
    <td class="tg-0lax">Function definitions for five functions. Two are complete, three are stubs. Your job in this lab is to replace the stubs with working code.</td>
    <td class="tg-baqh">YES</td>
  </tr>
  <tr>
    <td class="tg-0lax">arrayFuncs.h</td>
    <td class="tg-0lax">Function prototypes for five functions defined in arrayFuncs.cpp</td>
    <td class="tg-baqh">NO</td>
  </tr>
  <tr>
    <td class="tg-0lax">lab00Test.cpp</td>
    <td class="tg-0lax">Test cases for functions defined in arrayFuncs.cpp. This is the only file in this lab with a main() function (other than hellowWorld.cpp)</td>
    <td class="tg-baqh">NO</td>
  </tr>
  <tr>
    <td class="tg-0lax">tddFuncs.cpp</td>
    <td class="tg-0lax">Definitions for functions that support Test-Driven Development (TDD):<br>assertEquals, assertTrue, etc.</td>
    <td class="tg-baqh">NO</td>
  </tr>
  <tr>
    <td class="tg-0lax">tddFuncs.h</td>
    <td class="tg-0lax">Function prototypes for functions defined in tddFuncs.cpp</td>
    <td class="tg-baqh">NO</td>
  </tr>
</table>

### Step 4a: Adding a rule to link lab00Test

The file lab00Test.cpp is the one with a main function in it. So that is
the one that we make an executable from.

We make an executable from it by linking its .o version together with
the .o versions of the other .cpp files. The first line of the rule
looks like this:

    lab00Test: lab00Test.o tddFuncs.o arrayFuncs.o

That says that the executable for lab00Test <em>depends on</em> the .o
files lab00Test.o, tddFuncs.o and arrayFuncs.o, which are in turn, the
compiled machine code versions of lab00Test.cpp, tddFuncs.cpp and
arrayFuncs.cpp.

The line that follows this one is the command to link these .o files
into the executable. Remember that the second line here MUST START WITH
A TAB, not with spaces. You CANNOT JUST COPY AND PASTE FROM THIS WEB
PAGE.

    lab00Test: lab00Test.o tddFuncs.o arrayFuncs.o
            ${CXX} lab00Test.o tddFuncs.o arrayFuncs.o -o lab00Test

Put that in your Makefile, and then try running `make lab00Test`

Now, you might think that we need to create a rule such as this one
next:

    lab00Test.o: lab00Test.cpp
            ${CXX} -c lab00Test.cpp 

That is what we would do to tell the make utility how to create
lab00Test.o from lab00Test.cpp, with the -c flag (compile only; don't
link). The output file is automatically named by removing the .cpp and
replacing it with .o. But we don't have to do that. (See the tip below
for an explanation as to why)

Instead, just try typing `make lab00Test` and it should work:

    -bash-4.2$ make lab00Test
    clang++    -c -o lab00Test.o lab00Test.cpp
    clang++    -c -o arrayFuncs.o arrayFuncs.cpp
    clang++    -c -o tddFuncs.o tddFuncs.cpp
    clang++ lab00Test.o arrayFuncs.o tddFuncs.o -o lab00Test
    -bash-4.2$ 

So read the tip now to understand why we didn't need those extra rules:

We can actually omit the rules for `lab00Test.o`, etc.

The reason we can omit this rule is that it follows the pattern of an
implicit rule that the Make utility already has in place. That default
rule looks like this—it is NOT important (at this point)
for you to fully understand all the symbols in this default rule—it is
only important that you understand the idea that it replaces the
specific rule for `helloWorld.o`. Later in the course, we will cover the
meaning of the various symbols (`%`, `$<`, `$@`).

    %.o : %.cpp
            $(CXX) -c $(CFLAGS) $(CPPFLAGS) $< -o $@

Implicit rules are explained more in this section of the [GNU Make
documentation](ftp://ftp.gnu.org/old-gnu/Manuals/make-3.79.1/html_chapter/make_toc.html#TOC93)

As it turns out, we didn't need the rule for helloWorld.o either. Try
commenting it out, and doing a `make clean`, then a `make helloWorld`
and you'll see that everything still works just fine. We typically DO
needs rules for the linking steps, because Make cannot guess which .o
files need to be linked together to create an executable. But we often
do NOT need the rules for compiling, if our compile is following the
normal naming conventions.

### Step 4b: Adjusting the clean rule

So now, we are <em>almost</em> ready to run our `./lab00Test` program
and start working on getting test cases to pass. BUT FIRST, we need to
adjust our make clean rule.

Here's how it looks now:

    clean: 
            /bin/rm -f *.o helloWorld

Here is how it needs to look instead:

    clean: 
            /bin/rm -f *.o helloWorld lab00Test

We need to add the lab00Test executable to the make clean rule. In a
future lab, we'll see how we can factor out parts of this to make
keeping a Makefile up to date less tedious.

Step 5: Make your the code in arrayFuncs.cpp pass its tests
-----------------------------------------------------------

Here you need to follow the instructions inside the file arrayFuncs.cpp
to replace the stubs with working code.

The instructions there should be self-explanatory, and the assignment
should be super easy—this is essentially review from CS16, laying a
foundation for a discussion of sorting algorithms (later).

We need to be sure we understand how to find the index of a minimum and
maximum element, and how to swap two elements in an array.

When your code passes the tests, you are ready to try submitting it to
Gradescope.

Step 6: Checking your work before submitting
--------------------------------------------

When you are finished, you should be able to type `make clean` and then
`make lab00Test` then `./lab00Test` and see the following output:

``` {.bash}
-bash-4.2$ ./lab00Test
arrayToString(a,sizeA)={3,14,15,92,65,35,89}
PASSED: arrayToString(a,sizeA)
PASSED: indexOfMin(a,sizeA)
PASSED: indexOfMax(a,sizeA)
PASSED: arrayToString(a,sizeA); after swap(a,0,1)
PASSED: arrayToString(a,sizeA); after swap(a,0,2)
arrayToString(b,sizeB)={79,32,38,46}
PASSED: arrayToString(b,sizeB)
PASSED: indexOfMin(b,sizeB)
PASSED: indexOfMax(b,sizeB)
PASSED: arrayToString(b,sizeB); after swap(b,1,3)
PASSED: arrayToString(b,sizeB); after swap(b,0,2)
arrayToString(c,sizeC)={40,30,20,10}
PASSED: arrayToString(c,sizeC)
PASSED: indexOfMin(c,sizeC)
PASSED: indexOfMax(c,sizeC)
arrayToString(d,sizeD)={11,21,22,23}
PASSED: arrayToString(d,sizeD)
PASSED: indexOfMin(d,sizeD)
PASSED: indexOfMax(d,sizeD)
arrayToString(e,sizeE)={79,32,32,38,46}
PASSED: arrayToString(e,sizeE)
PASSED: indexOfMin(e,sizeE)
PASSED: indexOfMax(e,sizeE)
arrayToString(f,sizeF)={5,32,32,31,6,4,4}
PASSED: arrayToString(f,sizeF)
PASSED: indexOfMin(f,sizeF)
PASSED: indexOfMax(f,sizeF)
arrayToString(g,sizeG)={32,32,38,46,46,4,4}
PASSED: arrayToString(g,sizeG)
PASSED: indexOfMin(g,sizeG)
PASSED: indexOfMax(g,sizeG)
-bash-4.2$
```

At that point, you are ready to try submitting to the Gradescope system.

### An important word about academic honesty

Take a minute to read UCSB's Academic Integrity Policy: <http://judicialaffairs.sa.ucsb.edu/academic-integrity>

It is important that your code is a product of your work. The only time you are allowed to share code is between you and your pair programming partner. You may not distribute or share your solution to any other student. You may not base your code on other students' code (this includes retyping someone else's solution, make slight modifications, and submit it as your own work).

We will also test your code against other data files too—not just these. So while you might be able to pass the tests on Gradescope now by just doing a hard-coded "cout" of the expected output, that will NOT receive credit.

To be very clear, code like this will pass on Gradescope, BUT REPRESENTS A FORM OF ACADEMIC DISHONESTY since it is an attempt to just "game the system", i.e. to get the tests to pass without really solving the problem.

I would hope this would be obvious, but I have to say it so that there is no ambiguity: hard coding your output is a form of cheating, i.e. a form of "academic dishonesty". Submitting a program of this kind would be subject not only to a reduced grade, but to possible disciplinary penalties. If there is <em>any</em> doubt about this fact, please ask your TA and/or your instructor for clarification.

Step 7: Ading a little bit of code
--------------------------------------------
One final task for lab00 is to test another set of base code (that will we will build up to be our larger lab project).  Download the code from the github:
https://github.com/ucsb-cs32-s21/Lab00-step7-STARTER

If you are set up to use git from the command line, you will be cloning: git@github.com:ucsb-cs32-s21/Lab00-step7-STARTER.git

As a reminder: If you are not familiar with git, I highly recommend learning this skill since this will be extremely valuable when collaborating on large software projects. More information on git can be found here: https://ucsb-cs32.github.io/topics/git/.

Once you have the files (and have created a git repo for this lab like last week), take a look at the files.

Compile the code and look at it to get a sense of what it does.  


Working with real world data allows us to use computing to ask questions and learn about our world. It also allows us to practice design and implementation of object oriented projects. This week's lab is the first step in our larger project related to using various data sources to learn about the United States. This project and later additions will use the CORGIS datasets (The Collection of Really Great, Interesting, Situated Datasets): https://corgis-edu.github.io/corgis/

You will be provided with base code, written in C++ that reads in a CSV file representing county demographic data (demographic data relates to the structure of a population). The data file we will use is included in the base code and is named "county_demographics.csv."

Before you do anything else, goto the web page and take a quick look at all the data this csv file includes: https://corgis-edu.github.io/corgis/csv/county_demographics/

Which aspects of this demographic data is most interesting to you?

We will only work with some of this data this quarter. For today, we will only work with the data related to the age and education level of each county's population.

*Right now this is 'prototype' code - ripe for additions and revisions, which we will work this quarter*

For today, make sure you look at main.cpp and parse.cpp and understand how data is being inserted into vectors from the CSV file.

When you execute the main program 'dataProj' - it prints out the county name and population over the age of 65 for the first 50 counties... something like:
```
zoes-mbp:lab00-step7-STARTER zwood$ ./dataProj
County: Autauga County Percent population over 65: 13.8
County: Baldwin County Percent population over 65: 18.7
County: Barbour County Percent population over 65: 16.5
County: Bibb County Percent population over 65: 14.8
County: Blount County Percent population over 65: 17
County: Bullock County Percent population over 65: 14.9
```

Your task for today is to add the necessary code to also capture the population under age 18 and find and print the population information for
Santa Barbara county. 

To accomplish this task:
1) modify main.cpp and parse.cpp to support collecting a vector of the data associated with the population under age 18.  Specifically, modify the two functions in parse.cpp (and parse.h) to also collect this data. And modify main.cpp to declare and pass this new vector.
2) Modify main.cpp by adding code to now find and print the age population data about __Santa Barbara County__ - You will be asked to turn in a 'lab report' via gradescope to be able to report this data.  When your revisions are complete, executing dataProj, should report:

```
**Info about SB County**: Santa Barbara County Percent population over 65: <DATA>
 Percent population under 18: <DATA>
 ````
Where <DATA> is replaced with real values.  Fill in the values here: https://www.gradescope.com/courses/259718/assignments/1144611/submissions
    

There is an autograder test similar to testDemog1.cpp (but with the population under 18 vectors in use, which are commented out in the example code - but are included for you to uncomment once your changes are complete to test!).


Step 8: Submitting via Gradescope
--------------------------------

The lab assignment you will be making submission to gradescope:
1) First, "lab00" should appear in your Gradescope dashboard in CMPSC 32. If you haven't submitted anything for this assignment yet, Gradescope will prompt you to upload your files.

For this portion of the lab, you will need to upload your modified files (i.e. **`Makefile`** and **`arrayFuncs.cpp`**). For this lab, you are <b>required</b> to submit your files with your github repo.

If you already submitted something on Gradescope, it will take you to their "Autograder Results" page. There is a "Resubmit" button on the bottom right that will allow you to update the files for your submission.


2) Second, "lab00-step7" will also be found in your Gradescope dashboard in CMPSC 32. If you haven't submitted anything for this assignment yet, Gradescope will prompt you to upload your files.  For this portion of the lab, you will need to upload your modified files (i.e. **`parse.cpp`** and **`parse.h`** ). 

For this lab, if everything the autograder tests are correct, you'll see a successful submission passing all of the autograder test for both portions.  Then be sure to fill in the data requested in step 7 for Santa Barbara.


Grading Rubric
==============

This lab is based entirely on the grade assigned by Gradescope (via the autograder and the online 'lab report' to fill in the data about Santa Barbara. There will be labs this quarter where code style is assessed, but this is not
one of those labs.

Gradescope automated
-------------------

-   (40 pts) lab00Test passed Gradescope tests
-   (20 pts) helloWorld passed Gradescope tests
-   (30 and 10 pts) code addition passed Gradescope tests (step 7)(30) and fill in data about Santa Barbara (10)

Acknowledgements
================

Some material in this lab is based on work originally written by Mike
Costanzo and edited by Phill Conrad, and Richert Wang. Other parts are
original work of Phill Conrad.   Step 7 and language edits by Zoë Wood.
