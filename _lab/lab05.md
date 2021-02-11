---
layout: lab
num: lab05	
ready: false
desc: "Visitor Design Patern - Part 1"
assigned: 2021-02-10
due: 2021-02-17 23:59
github_org_url: https://github.com/ucsb-cs32-w21
---

Goals
=====

This is a two part lab.  This first half is meant to be a a very simple first pass at looking at the visitor pattern.  The purpose is to practice the pattern and associated techology (and the next lab will explore the concepts in more detail with larger code revisions).  Learning objectives. At the end of this lab, students should be able to:

-  Implement the visitor design pattern for the exisiting code to support a simple visitors pattern to create a combined report for data


Orientation
============
At this point, we have a fairly complex program to read in regional data (demographic and hospital) and aggreagate that data to various levels (county and state).  
For this week, we will introduce minor changes as an introduction to the visitor pattern.  This first pass is intended a very simple addition with minimal changes to our code (and the next lab will explore the concepts in more detail with larger code revisions). 

With OO programming, there are some design patterns that can be used 'to solve recurring design problems to design flexible and reusable object-oriented software, that is, objects that are easier to implement, change, test, and reuse' (https://en.wikipedia.org/wiki/Design_Patterns).  This is a rich topic which is difficult to explore in a short time.  To get a taste for the design patterns we will explore integrating the visitor design pattern into our exisiting code.  This first pass will be very simple (and not take full advantage of this pattern), and we will do further revisions next week.

For this week, the goal is to make minor modifications to use the visitor pattern to print a report combining demographic and hospital data for specified data.  You could accomplish this without the visitor pattern, but our goal is to practice this pattern.


Steps
============
Introduce and modify the following classes as follows to support printing a combined report.
1) Create a visitor class to be used as an interface.  This should only define pure virtual methods to visit the two types: hospitalData and demogData
2) Modify placeData to also include a pure virtual function:
```
    //Lab05 anything that is place data must accept a visitor (aka must be visitable)
    virtual void accept(class Visitor &v) = 0;
```
3) Implement the accept method for hospitalData and demogData.  It should just call visit on the visitor for the given type.
4) Define a visitorReport class that implements the visit method for each of the two types.  For this week's lab, the visit method just print a subset of each type's data (match example data)
5) Modify dataAQ.h to add a method to print a report of the data for any state that meets a given criteria.  Start with the state data for any state with a percentage of the population below the poverty line above a threshold:
```
void dataAQ::stateReport(double thresh);
```

An example output would include:
```
States with population below poverty line greater than 20%
*****print special report demog Data: 
Demographics Info (State): MS
Education info: 
(% Bachelor degree or more): 20.43
(% high school or more): 81.62
% below poverty: 22.63
*****print special report hospital data:
Hosptial Info: MS
Overall rating (out of 5): 2.57
*****print special report demog Data: 
Demographics Info (State): NM
Education info: 
(% Bachelor degree or more): 25.58
(% high school or more): 83.39
% below poverty: 20.40
*****print special report hospital data:
Hosptial Info: NM
Overall rating (out of 5): 2.73
-----Generated a report for a total of: 2
```

------
Scoring
--------
This lab is meant to be simple so is worth half credit.  We will expand these technologies and do a more detailed re-design next week.
Autograding (stay tuned) 30
Code review/design matching lab spec 20


