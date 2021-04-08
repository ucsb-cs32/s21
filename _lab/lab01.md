---
layout: lab
num: lab01	
ready: false
desc: "C++ class design to support CSV data"
assigned: 2021-04-13 
due: 2021-04-20 23:59
github_org_url: https://github.com/ucsb-cs32-w21
---

Goals
=====

Learning objectives.  At the end of this lab, students should be able to:

-   read and understand  C++ code to read input from a CSV file
- 	read and understand  C++ code representing county demographic data
- 	extend an exisiting C++ class to support additional data and methods (including modifying related code to read in data)
-   be able to run provided test cases and understand the output to confirm code modifications work


Orientation
=====

Similar to step 7 of Lab00, this is the background on the data project for this quarter:
Working with real world data allows us to use computing to ask questions and learn about our world.  It also allows us to practice design and implementation of object oriented projects.  This week's lab is the first step in our larger project related to using various data sources to learn about the United States.
This project and later additions will use the CORGIS datasets (The Collection of Really Great, Interesting, Situated Datasets): https://corgis-edu.github.io/corgis/

You will be provided with base code, written in C++ that reads in a CSV file representing county demographic data (demographic data relates to the structure of a population).  The data file we will use is included in the base code and is named  "county_demographics.csv."

Before you do anything else, goto the web page and take a quick look at all the data this csv file includes:
https://corgis-edu.github.io/corgis/csv/county_demographics/

Which aspects of this demographic data is most interesting to you?

We will only work with some of this data this quarter.  For today, we will only work with the data related to the age and education level of each county's
population.

Unlike the code in Lab00, we want to start encapsulating our data into classes....

Step by Step
============

Step 0: Getting Started
-----------------------

### Download base code and test the executables dataProj and testDemog1
Download the new base code.  It can be found here:

https://github.com/ucsb-cs32-w21/lab01-STARTER

If you are set up to use git from the command line, you will be cloning: git@github.com:ucsb-cs32-w21/lab01-STARTER.git

As a reminder: If you are not familiar with git, I highly recommend learning this skill since this will be extremely valuable when collaborating on large software projects. More information on git can be found here: https://ucsb-cs32.github.io/topics/git/.

Once you have the files (and have created a git repo for this lab like last week), take a look at the files.  Some will look familiar from Lab00 step 7, but now we are *encapsulating* demographic data into a class (no more parallel vectors!). Details are included below.

The starter code includes files related to our main data project and files related to testing our code.
When you try to compile the code using the provided Makefile, it should be able to make the executable for our main data project:
<b>dataProj</b> and testDemog1.

You should see some compilation errors related to building the testDemog2.  This is intentional (as you ultimately need to modify the class
definition - see later steps).

You should confirm that when you run
./dataProj

that it prints out county data (lots of county data - so expect you console to be filled with print outs).  You might see something like:

```
County Demographics Info: Alameda County, CA total population: 1610921
Population info: 
(% over 65): 12.5
(% under 18): 21.4
(% under 5): 6.1
Education info: fix this for lab01

County Demographics Info: Alpine County, CA total population: 1116
Population info: 
(% over 65): 21.1
(% under 18): 20
(% under 5): 3.3
Education info: fix this for lab01

County Demographics Info: Amador County, CA total population: 36742
Population info: 
(% over 65): 25.1
(% under 18): 15.3
(% under 5): 3.7
Education info: fix this for lab01

County Demographics Info: Butte County, CA total population: 224241
Population info: 
(% over 65): 17
(% under 18): 20.2
(% under 5): 5.4
Education info: fix this for lab01
```

Note that with so much data, it will likely be useful to redirect the output to a file.  If you run: Lab01Full zwood$ ./dataProj > outputFile
You can then open the text file "outputFile" to look at all the data using a text editor.
Or for example use "more outputFile" to examine the data one screen at a time.

You should also make sure that you can successfully run testDemog1 and see results like:<br>
[zjwood@csilvm-01 Lab01Base]$ ./testDemog1<br>
Testing class demogData...<br>
PASSED: c1.getName()<br>


Step 1: Read and Understand the code
-----------------------

### Lets take a look at the files (questions about these files is fair game for hw and quizzes this week)
Now, take a moment to look at the various files.
I suggest you start with main.cpp.
In your own words, how would you describe what main.cpp is doing?

Then take a look at our representation of county data:
demogData.h
demogData.cpp
You should note that at this time, we are only storing demographic information related to the age of the county population.
You will be editing and adding to this file, so make sure you understand it.

Next take at the helper functions used to read the data from our CSV file:
parse.h
parse.cpp
You will only have to make small modifications to these files, but should be able to understand the basics of how these
functions are working.

In general the above files will be a part of our project.  You will want to make friends with these files.  

The base code folder also includes some files for testing our code.
testDemog1.cpp
testDemog2.cpp
tddFuncs.h
tddFuncs.cpp

Take a quick look at the test files.  Test driven development helps us catch errors early in our code before we make assumptions and end up
in a dark corner (we still will have to debug but testing can help it be less painful).  
As mentioned above testDemog2 does not compile this is because you have some work to do.

Add comments to any of the files to help you remember what they do.  We will work with this code again this quarter so make sure to ask
questions now.


Step 2: Small modifications to the code (adding additional data to demogData)
-----------------------
### We will need to modify various files to add more demograpic data

Currently, the demogData class only stores data related to the age of the county's population.  
For this first week, lets add some additional information, specifically, the data related to education:
<b>Education.Bachelor's Degree or Higher <br>	
Education.High School or Higher</b>

There are a few closely related steps in this process:
1) add data to the class demogData to represent the percentage of the county population that have received an undergraduate degree and the percentage
that has graduated from high school
2) add the data fields to the class constructor (*add a new constructor for county data with all fields.  THE ORDER SHOULD MATCH THE ORDER OF THE DATA IN THE ORIGINAL FILE> - leave the prior constructor and set default values for the education fields of -1).  You should have two constructors when you are done.*
4) add the necessary getter methods for this new data (hint: check out testDemog2 for getter names).
5) We will be looking at averaging data in future assignments and cannot average percentages across counties (because they each have different sized populations).  Instead, we will total counts (or number of people per category) and divide by total population to report average population (per state).  Thus, you need to add getters to return the count for each data category, for each county.  Each should return an integer.  Name these getters as follows:
 ```
getpopOver65Count()
getpopUnder18Count()
getpopUnder5Count()
getBAupCount()
getHSupCount()
```
7) add code to parse.cpp to read in the two additional data fields (and use them when constructing a demogData object).
8) modify in demogData.cpp the function that overrides the << operator to also print the educational data.  See the below sample for formatting.


Step 3: Make sure your output matches and now all test cases pass
-----------------------
### Make and run
If you completed the steps above, you should now be able to compile all of the code and tests with <tt>make</tt>

So that when you run testDemog2 you see:
```
zwood$ ./testDemog2
Testing class county demographics...
PASSED: c1.getName()
PASSED: c1.getState()
PASSED: c1.getpopOver65()
PASSED: c1.getpopUnder18()
PASSED: c1.getpopUnder5()
PASSED: c1.getBAup()
PASSED: c1.getHSup()
PASSED: c1.getPop()
PASSED: c1.getpopOver65Count()
PASSED: c1.getpopUnder18Count()
PASSED: c1.getpopUnder5Count()
PASSED: c1.getBAupCount()
PASSED: c1.getHSupCount()
```

Now, when you print all the county data it should look like:
```
County Demographics Info: Lewis County, WA total population: 75128
Population info: 
(% over 65): 19.8 Count: 14875
(% under 18): 21.9 Count: 16453
(% under 5): 5.8 Count: 4357
Education info: 
(% Bachelor degree or more): 14 Count: 10517
(% high school or more): 85.9 Count: 64534
County Demographics Info: Lincoln County, WA total population: 10250
Population info: 
(% over 65): 23.9 Count: 2449
(% under 18): 21.7 Count: 2224
(% under 5): 4.7 Count: 481
Education info: 
(% Bachelor degree or more): 20.3 Count: 2080
(% high school or more): 93.5 Count: 9583
County Demographics Info: Mason County, WA total population: 60711
Population info: 
(% over 65): 21.3 Count: 12931
(% under 18): 19.3 Count: 11717
(% under 5): 5.4 Count: 3278
Education info: 
(% Bachelor degree or more): 17.3 Count: 10503
(% high school or more): 88.5 Count: 53729
```
Consider using <b>diff</b> on the file you produce and the provided comparison file.

Step 4: Submitting via Gradescope
-----------------------
### Submitting via Gradescope

The lab assignment "Lab01" should appear in your Gradescope dashboard in CMPSC 32. If you haven't submitted anything for this assignment yet, Gradescope will prompSubmit your files with your github repo like last week.

If you already submitted something on Gradescope, it will take you to their "Autograder Results" page. There is a "Resubmit" button on the bottom right that will allow you to update the files for your submission.

For this lab, if everything is correct, you'll see a successful submission passing all of the autograder tests.

This lab is based entirely on the grade assigned by Gradescope. There may be labs this quarter where code style is assessed, but this is not one of those labs.

Gradescope automated

    (20 pts) each for all 5 of the Gradescope tests

Acknowledgements
================

Winter `21 vesion: Zoë Wood.  Thank you to the original CORGIS crew for their work sharing this data (https://corgis-edu.github.io/corgis/) and to Aaron Keen for curriuclum review. Editing, autograder and general support to thanks to: AMR, SDM, QH, AR, BL
