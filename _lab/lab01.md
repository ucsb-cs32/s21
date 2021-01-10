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


Orientation
=====


Working with real world data allows us to use computing to ask questions and learn about our world.  It also allows us to practice design and implementation of object oriented projects.  This week's lab is the first step in our larger project related to using various data sources to learn about the United States.
This project and later additions using CORGIS datasets (The Collection of Really Great, Interesting, Situated Datasets): https://corgis-edu.github.io/corgis/

You will be provided with base code, written in C++ that reads in a CSV file representing county demographic data (demographic data relates to the structure of a population).  The data file we will use is included in the base code and is named  "county_demographics.csv."

Before you do anything else, goto the web page and take a quick look at all the data this csv file includes:
https://corgis-edu.github.io/corgis/csv/county_demographics/

Which aspects of this demographic data is most interesting to you?

We will only work with some of this data this quarter.  For today, we will only work with the data related to the age and education level of each county's
population.

Step by Step
============

Step 0: Getting Started
-----------------------

### Download base code
Download the base code.  It includes files related to our main data project and files related to testing our code.
When you try to compile the code using the provided Makefile, it should be able to make the executable for our main data project:
<b>dataProj</b> and testDemog1.

You should see some compilation errors related to building the testDemog2.  This is intentional (as you ultimately need to modify the class
definition - see later steps).

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


Step 1: Add comments to show understanding of code
-----------------------

### Add header comments to the following files:
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


Step 2: Add data and methods to the demographicData class
-----------------------
### Add data and methods to the demographicData class

Currently, the demogData class only stores data related to the age of the county's population.  
For this first week, lets add some additional information, specifically, the data related to education:
<tt>Education.Bachelor's Degree or Higher 	
Education.High School or Higher</tt>

There are a few closely related steps in this process:
1) add data to the class demogData to represent the percentage of the county population that have received an undergraduate degree and the percentage
that has graduated from high school
2) add the data fields to the class constructor (*add a new constructor for county data with all fields - leave the prior constructor and set default values for the education fields of -1).  You should have two constructors when you are done.*
3) add the necessary getter methods for this new data (hint: check out testDemog2 for getter names).
4) add code to parse.cpp to read in the two additional data fields (and use them when constructing a demogData object).
5) modify in demogData.cpp the function that overrides the << operator to also print the educational data.  See the below sample for formatting.

Finally, to start making the demogData class conform to good OO style, all the data is private, however, we want to give access to (read) the data, 
so add getters for all of the data currently associated with our demogData. (Note again see testDemg2 for getter names).

Step 3: Make sure your output matches and now all test cases pass
-----------------------
### Make and run
If you completed the steps above, you should now be able to compile all of the code and tests with <tt>make</tt>

So that when you run testDemog2 you see:
<tt>
zwood$ ./testDemog2
Testing class county demographics...
PASSED: c1.getName()
PASSED: c1.getState()
PASSED: c1.getpopOver65()
PASSED: c1.getpopUnder18()
PASSED: c1.getpopUnder5()
PASSED: c1.getBAup()
PASSED: c1.getHSup()
  </tt>

Now, when you print all the county data it should look like:
...
County Demographics Info: Uinta County, WY
Population info: 
(% over 65): 11
(% under 18): 29.8
(% under 5): 7.6
Education info: 
(% Bachelor degree or more): 18.9
(% high school or more): 89.2
County Demographics Info: Washakie County, WY
Population info: 
(% over 65): 20.1
(% under 18): 23.9
(% under 5): 5.5
Education info: 
(% Bachelor degree or more): 23.6
(% high school or more): 90.5
County Demographics Info: Weston County, WY
Population info: 
(% over 65): 18.1
(% under 18): 21.6
(% under 5): 6.5
Education info: 
(% Bachelor degree or more): 17.2
(% high school or more): 90.2

