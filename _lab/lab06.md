---
layout: lab
num: lab06
ready: true
desc: "Visitor Design Patern - Part 1"
assigned: 2021-05-16
due: 2021-05-20 23:59
github_org_url: https://github.com/ucsb-cs32-s21
---

Goals
=====

This is a two part lab.  This first half is meant to be a a very simple first pass at looking at the visitor pattern.  The purpose is to practice the pattern and associated techology, while the second half of the lab explores the concepts in more detail with larger code revisions.  Learning objectives. At the end of this lab, students should be able to:

-  Implement the visitor design pattern (part 1) for the exisiting code to support a simple visitors pattern to create a combined report for data


Modality
============
This is a pair lab.  You may choose to work alone or with another student.  When working in a pair, please always follow good pair programming methodologies.  In general, set aside time to work together and share your screen to share the work and learning.  

You will need to identify you partner (pair) in your submission (add a header to your main with both your names!).  The remaining labs will also be optional pair labs and you will be asked to only partner with the same person TWICE.  

You *may* work with the same person on part 1 and 2 (assuming they fit the prior rule).

Orientation - part 1
============
At this point, we have a fairly complex program to read in regional data (demographic and police shooting data) and aggreagate that data to various levels (state or data criteria).  
This lab is broken into two parts to help with your development.  The first part is meant as a straight forward introduction to the visitor pattern.  This first pass is intended a very simple addition with minimal changes to our code (and the next part will explore the concepts in more detail with larger code revisions). You will be asked to submit a mandatory working part 1, earlier than the final due date to help keep us all on target for task completion.

With OO programming, there are some design patterns that can be used 'to solve recurring design problems to design flexible and reusable object-oriented software, that is, objects that are easier to implement, change, test, and reuse' (https://en.wikipedia.org/wiki/Design_Patterns).  This is a rich topic which is difficult to explore in a short time.  To get a taste for the design patterns we will explore integrating the visitor design pattern into our exisiting code.  This first pass will be very simple (and not take full advantage of this pattern), and we will do further revisions in part two.

For part 1, the goal is to make minor modifications to use the visitor pattern to print a report combining demographic and police shooting data for specified data.  You could accomplish this without the visitor pattern, but our goal is to practice this pattern.

Steps for part 1 (complete and turn in mid-point code)
============
Introduce and modify the following classes as follows to support printing a combined report, using the visitors pattern.
1) Create a visitor class to be used as an interface.  This should only define pure virtual methods to visit our types: psCombo and demogData, and psData (although for this exercise you are not asked to generate a report with psData).  This file must be called **visitor.h**
2) Modify regionData to also include a pure virtual function (so that derived classes can accept a visitor):
```
    //Lab06 anything that is region data must accept a visitor (aka must be visitable)
    virtual void accept(class Visitor &v) = 0;
```
3) Implement the accept method for psCombo and demogData, and psData.  It should just call visit on the visitor for the given type.
4) Define a visitorReport class that implements the visit method for each of the two types.  For part 1, the visit method just prints a subset of each type's data (match example data shown below).  This file must be called **visitorReport.h**
5) Modify dataAQ.h to add a method to print a report of the data for any state that meets a given criteria - name this method:
```
void dataAQ::comboReport(double thresh);
```
You must implement this method by creating a visitorReport and calling accept with this visitor on a collection of demogData and/or psCombo/psData  that meets the given criteria. You may create the selection first then call accept on all values in the collection.  To be explicit, create one big pile of regionData:
```
std::vector<shared_ptr<regionData>> pileData;
```
Put any demog data that meets the criteria of any state data where the percentage of the population that have graduted high school is above the specified threshold passed in as a parameter to the method.  Also add the police shooting data from the same state to the pile of data.  Then call accept on the pile of data - i.e.:
```
    visitorReport report;

    for (const auto &obj : pileData) {
        obj->accept(report);
    }
 ```

Thus, for example, for a dataAQ called *theAnswers*, calling:
```
theAnswers.comboReport(92);
```
would produce the following report:
```
print summary demog Data:
Region info: comboData, MN
Education info:
(Bachelor or more): 32.81% and total: 1790458
(high school or more): 92.09% and total: 5025407
Total population: 5457173
Racial Demographics Info: 
% American Indian and Alaska Native percent: 1.33 count: 72408
% Asian American percent: 4.72 count: 257453
% Black/African American percent: 5.86 count: 319700
% Hispanic or Latinx percent: 5.07 count: 276522
% Native Hawaiian and Other Pacific Islander percent: 0.07 count: 4020
% Two or More Races percent: 2.33 count: 127059
% White (inclusive) percent: 85.73 count: 4678263
% White (nonHispanic) percent: 81.44 count: 4444343
total Racial Demographic Count: 5457173
print aggregate police shooting data 
State Info: MN, total states: 1
Number of incidents: 73
Racial demographics of state incidents: Racial Demographics Info: 
% American Indian and Alaska Native percent: 4.27 count: 5
% Asian American percent: 2.56 count: 3
% Black/African American percent: 11.11 count: 13
% Hispanic or Latinx percent: 2.56 count: 3
% Native Hawaiian and Other Pacific Islander count: 0
% Two or More Races count: 0
% White (inclusive) percent: 38.46 count: 45
% White (nonHispanic) percent: 38.46 count: 45
% Other percent: 5.48 count: 4
total Racial Demographic Count: 73
print summary demog Data:
Region info: comboData, MT
Education info:
...
```

There are two public test files (and the Makefile that will be used on the autograder) here: https://github.com/ucsb-cs32-s21/Lab06-part1-tests

**While you are working on matching the report output, note that whitespace differences will be important to pay attention to**. A useful tool is to redirect the ouput of the test to a file:
```
 ./testReport> t
```
and then use vi to edit the file:
```
vi t
```
and use
```
:set list
```
to show whitespace (especially to see if there are trailing white space differences.

Mandatory check in part 1 - due May 20th
============
(20) autograder (mandatory on time to receive credit for next portion) : https://www.gradescope.com/courses/259718/assignments/1243215/submissions
