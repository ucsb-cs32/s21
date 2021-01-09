---
layout: lab
num: lab01	
ready: false
desc: "C++ class design to support CSV data"
assigned: 2021-01-13 
due: 2021-01-20 23:59
github_org_url: https://github.com/ucsb-cs32-w21
---

Goals
=====

Learning objectives.  At the end of this lab, students should be able to:

-   read and understand  C++ code to read input from a CSV file
- 	read and understand  C++ code representing county demographic data
- 	extend an exisiting C++ class to support additional data and methods
-   be able to run provided test cases and understand the output to confirm code modifications work

Step by Step
============

Step 0: Getting Started
-----------------------

### Download base code

Working with real world data allows us to use computing to ask questions and learn about our world.  It also allows us to practice design and implementation of object oriented projects.  This week's lab is the first step in our larger project related to using various data sources to learn about the United States. This project and later additions using CORGIS datasets (The Collection og Really Great, Interesting, Situated Datasets): https://corgis-edu.github.io/corgis/

You are provided with base code, written in C++ that reads in a CSV file representing county demographic data.  The data file is included in the base 
code and is named  "county_demographics.csv."

Before you do anything else, goto the web page and take a quick look at all the data this csv file includes:
https://corgis-edu.github.io/corgis/csv/county_demographics/

Which aspects of this demographic data is most interesting to you?

We will only work with some of this data this quarter.


Step 1: Add comments to show understanding of code
-----------------------

### Add header comments to the following files:
Make sure you can explain in general what the following files are doing:
demogData.h
demogData.cpp
parse.h
parse.cpp
main.cpp

These are the main files that will be a part of our project.  You will want to make friends with these files.  

The code also includes some files for testing our code.
testDemog1.cpp
testDemog2.cpp
tddFuncs.h
tddFuncs.cpp

Take a quick look at the test files.  Note that as given to you the testDemog2 does not pass.... this is because you have some work to do.

You should confirm that when you run
./dataProj

that it prints out county data.  You might see something like:

....

County Demographics Info: Uinta County, WY
Population info: 
(% over 65): 11
(% under 18): 29.8
(% under 5): 7.6
Education info: fix this for lab01

County Demographics Info: Washakie County, WY
Population info: 
(% over 65): 20.1
(% under 18): 23.9
(% under 5): 5.5
Education info: fix this for lab01

County Demographics Info: Weston County, WY
Population info: 
(% over 65): 18.1
(% under 18): 21.6
(% under 5): 6.5
Education info: fix this for lab01
***

You should also make sure that you can successfully run testDemog1 and see results like:
[zjwood@csilvm-01 Lab01Base]$ ./testDemog1
Testing class demogData...
PASSED: c1.getName()


Step 2: Add data and methods to the demographicData class
-----------------------
### Add data and methods to the demographicData class

Currently, the demogData class only reads in some of the data.  We will will not use all the data, however, in addition to the age data
already reprsented, lets add educational data.  
Start by adding data to demogData to represent the percentage of the county population that have received an undergraduate degree and the percentage
that has graduated from high school.

(Check out testDemog2 for getter names).

This will require you to:
1) add the data fields to the class
2) add the data fields to the class constructor
3) add code to parse.cpp to read in the two additional data fields (and use them when constructing a demogData object).

You will also need to add all the getters used in testDemg2 (for all fields used in the testDemog2).



