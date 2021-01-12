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
-   Use STL hashmaps to aggregate 'county' level data to 'state' data
- 	Design and implement a C++ class representing state demographic data
- 	Extend C++ class to support additional data and methods
-   Utilize data aggregated into a hashmap to answer questions about the data (e.g. state with the youngest population)
-   (gradescope test?)


Orientation
============
Last week, we developed code to read in county demographic data (age and education).  This week, our goal is to examine that data and be able to asnwer questions about regions in the US.  Such as which region has the youngest population? Later in the quarter we will combine other datasets and be able to expand our queries.

The first step is deciding at what regional level we want to look at the data.  With over three thousand counties, we want to consider larger regions (by grouping counties).  There are lots of ways to understand regional data, but for this week, we will look at state level data. Thus, one of the first tasks is to start aggregating county data together into states.  

Once we have the data aggregated together, we will use various methods to identify extremes in the data (minimums and maximums).

This week's lab is a bit different in that you will have choices about how to solve aspects of the solution and then conduct a code review with one of the teaching, learning assistants or instructor.  C++ has many tools to solve this problem, you will be able to solve these tasks with what
has already been discussed in lecture.  Just make sure you understand your solution and you will be asked to discuss your solution.

Tasks
============

Step 0: Getting Started - think about the problem
-----------------------

### Starting from your code last week
There are various ways to tackle this problem.  There are some clear cut tasks, but the order you takle them will be somewhat up to you.  
In general to solve this problem, we must aggregate county data into states (this means having a method to collect all the counties for a 
given state <b>and</b> combine the county's demographic data to state level data (for this assignment we will be averaging the county data).

Recall that when we think about a problem, one of the first tasks is to consider the 'data' (and then closely related, what are the data structures 
to use to build up data relationships).  There are multiple right solutions here, and here are some of the general tasks. You can tackle them in whatever order makes sense to you, but we will be looking for these aspects in your solution.

Do create a new github repo for this weeks lab.  We will be looking at your code via git hub.

Task 1: Design and Implement a class to represent 'state' data
-----------------------
### Design and Implement a class to represent 'state' data
Ultimately, we will want to conduct simple data analysis on state level data (i.e. which state has the most people with Bachelor's degrees), etc. 
Design a class to represent state level demographic data.  Again, there are multiple valid solutions here.  Design a solution that makes sense to you. 

<b>At this point we ask that you do not use inheritence or polymorphism</b> - that will come in future weeks. Designing a solution without them will help motivate their use in later labs.

The state data should have the same demographic information that the county data has, that is age and education.  It likewise will need additional data (especially associated with averaging the county data).

Task 2: Design and Implement solution to aggregate data (STL hashmap)
-----------------------
### Create and propogate data into hashmap to aggregate county data to state data
Use an STL hashamp in order to aggregate the county data into state data.  Again you have choices here.  Do what makes sense for you solution.

Task 3: Use data represenation (STL hashmap) to answer queries about data
-----------------------
### (e.g. state with the youngest population)
Your solution should be general, i.e. we should be able to ask for you to be able to find extremes of <b>any</b> of the data fields (and you should
expect we will do this during your code review).



Task 4: Testing - specific cases that must match output
-----------------------
### (e.g. state with the youngest population)

For the sake of testing please submit a solution to gradescope that matches the provided test cases (state with youngest population and state 
with most backelor's degrees).  Output should match:

...
