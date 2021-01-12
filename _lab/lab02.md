---
layout: lab
num: lab02	
ready: false
desc: "Using STL to aggregate data and query"
assigned: 2021-01-20 
due: 2021-01-27 23:59
github_org_url: https://github.com/ucsb-cs32-w21
---

Goals
=====

Learning objectives. At the end of this lab, students should be able to:

-   read and understand base C++ code (related to reading data from CSV file (all lab01))
-   Use STL hashmaps to aggregate 'county' level data to 'state' data (including computing the average)
- 	Design and implement a C++ class representing state demographic data
-   Utilize data aggregated into a hashmap to answer questions about the data (e.g. state with the youngest population)
-   practice using a testing framework, including writing additional tests


Orientation
============
Last week, we developed code to read in county demographic data (age and education).  This week, our goal is to examine that data and be able to asnwer questions about regions in the USA.  For example, which region has the youngest population? Later in the quarter we will combine other datasets and be able to expand our queries.

The first step is deciding what regional level we want to look at our data.  With over three thousand counties, we want to consider larger regions (by grouping counties).  There are lots of ways to understand regional data, but for this week, we will look at state level data. Thus, one of the first tasks is to start aggregating county data together into states.  

Once we have the data aggregated together, we will use various methods to identify extremes in the data (minimums and maximums) of various demographic fields.  *Although you have choices about the core tasks, you will need to wrap your solution in a class that we will use for testing.*

This week's lab is a bit different in that you will have choices about how to solve the primary aspects of the problem and then you will need
to implement a very specific class to help with testing.  Part of your lab grade will depend upon passing tests and another portion of grade
depends on your code will being reviewed by one of the teaching assistants or instructor.  

In general, C++ has many tools to solve various aspects of this problem, it is just important that you
undrestand the tools you are using in your solution.  You can implement a solution to each of these tasks with the material that
has already been discussed in lecture.  Make sure you understand your solution as you will/may be asked to discuss your solution.

Tasks
============

Step 0: Getting Started - think about the problem
-----------------------

### Starting from your code last week
There are various ways to tackle this problem.  To start, make sure you understand the problem.  Given county level data, we want to average all
the county data for a given state together and then be able to query the maximums and minimums of any of the data fields.

There are some clear cut tasks, but the order and exact implmentation is somewhat up to you, with the exception of the <b>dataAQ class</b>, for which you *must* implement the specified functions for use in testing. 

In general, to solve this problem, we must aggregate county data into states.  This means having an implmentation to collect all the counties for a 
given state <b>and</b> combine the county's demographic data to state level data.  For this assignment, to combine the data, we will be averaging any county data in our data set for its associated state.

Recall that when we think about a problem, one of the first tasks is to consider the 'data' associated with that problem (and then closely related, to consider what are the data structures 
we can use to build up necessary data relationships).  There are multiple valid solutions here, but for this lab we do expect to see solutions to the following general tasks. You can tackle them in whatever order makes sense to you, but we will be looking for these aspects in your solution.

Regardless of exactly how you solve the following tasks, you must support the specified queries as a part of the dataAQ class.  Makesure you understand exactly how your solution will be tested before you dive in too deep.

Do create a new github repo for this weeks lab.  We will be looking at your code via git hub.

Task 1: Design and Implement a class to represent 'state' data
-----------------------
### Design and Implement a class to represent 'state' data
Ultimately, we will want to conduct simple data analysis on state level data (i.e. which state has the most people with Bachelor's degrees), etc. 
Design a class to represent state level demographic data.  Again, there are multiple valid solutions here.  Design a solution that makes sense to you. 

<b>At this point we ask that you do not use inheritence or polymorphism</b> - that will come in future weeks. Designing a solution without them will help motivate their use in later labs.

The state data should have the same demographic information that the county data has, that is age and education  State data will need additional data to what is stored in a county (especially associated with averaging the county data). But, yes, this does mean you will have 
two classes that are very similar but represent different regional zones and store different data (as mentioned above, we will revisit this design as we expand our data project).

Task 2: Design and Implement a solution to aggregate data (using an STL hashmap)
-----------------------
### Create and propogate data into a hashmap to aggregate county data to state data
Use an STL hashamp in order to associate any county data with it's state (i.e. recall from our demogData class has a string which is the name of the state where that county is located).  Again you have choices here.  Do what makes sense for you solution.

Depending on the order you tackle these tasks, don't forget that one task is to average the demographic data for all county into state level demographic data.

Task 3: Use data represenation (STL hashmap) to be able to answer queries about data
-----------------------

Once ou have a colletion of state level data, we should be able to identify extremems (maximum and minimums) for any of the data fields (or combination of data fields).

Your solution should be general, i.e. we should be able to ask for you to be able to find extremes of <b>any</b> of the data fields (and you should
expect we will do this during your code review).


Task 4: Testing - implement the dataAQ class exactly as specified for testing
-----------------------
### specific cases that must match output (e.g. state with the youngest population)

For the sake of testing please implement a class that can aggregate data and print out results from specific queries, named <dataAQ>.  See testStates.cpp for example of how this class will be used.  Aain, the exact implementation is up to you, but your dataAQ class must support the following methods:
 
<p style="font-family:'Courier New'">
`//data aggregator and query for testing<br>
class dataAQ {<br>
  public:<br>
    dataAQ();<br>
    //function to aggregate the data - this CAN and SHOULD vary per student - depends on how they map<br>
    void createStateData(std::vector<shared_ptr<demogData>> theData);<br>
    //return the name of the state with the largest population under age 5<br>
    string youngestPop();<br>
    //return the name of the state with the largest population under age 18<br>
    string teenPop();<br>
    //return the name of the state with the largest population over age 65<br>
    string wisePop();<br>
    //return the name of the state with the largest population who did not finish high school<br>
    string underServeHS();<br>
    //return the name of the state with the largest population who completed college<br>
    string collegeGrads();<br>
  <br>
    //additional methods AND data to support above methods.  You are allowed for data to be public<br>
    ...<br>
 }'<br>
 </p>

Again, see testStates.cpp for the use of the dataAQ class to test your implementation.

You are encouraged to write additional test cases for each of the required queries in dataAQ.

The output for dataProj should include a complete version of the following (your code would fill in for <BLANKS>):
 *** the state that needs the most pre-schools**
State Info: UT
Number of Counties: 29
Population info: 
(over 65): 13.7414
(under 18): 29.9069
(under 5): 7.67931
Education info: 
(Bachelor or more): 23.5586
(high school or more): 90.531
*** the state that needs the most high schools**
State Info: <BLANK>
Number of Counties: <BLANK>
Population info: 
(over 65): <BLANK>
(under 18): <BLANK>
(under 5): <BLANK>
Education info: 
(Bachelor or more): <BLANK>
(high school or more): <BLANK>
*** the state that needs the most vaccines**
State Info: <BLANK>
Number of Counties: <BLANK>
Population info: 
(over 65): <BLANK>
(under 18): <BLANK>
(under 5): <BLANK>
Education info: 
(Bachelor or more): <BLANK>
(high school or more): <BLANK>
*** the state that needs the most help with education**
State Info: <BLANK>
Number of Counties: <BLANK>
Population info: 
(over 65): <BLANK>
(under 18): <BLANK>
(under 5): <BLANK>
Education info: 
(Bachelor or more): <BLANK>
(high school or more): <BLANK>
*** the state with most college grads**
State Info: <BLANK>
Number of Counties: <BLANK>
Population info: 
(over 65): <BLANK>
(under 18): <BLANK>
(under 5): <BLANK>
Education info: 
(Bachelor or more): <BLANK>
(high school or more): <BLANK>

