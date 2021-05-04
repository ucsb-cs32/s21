---
layout: lab
num: lab05	
ready: false
desc: "OO polymorphism/inheritence"
assigned: 2021-05-05 
due: 2021-05-15
github_org_url: https://github.com/ucsb-cs32-s21
---

Goals
=====

Learning objectives. At the end of this lab, students should be able to:

-  Revise and modify the implementation of existing code to lift shared data and members to parent class(es) (implement inheritance to simplify our existing code base)
-  Reduce redundancy in code by using inheritance (including re-write parse.cpp to reduce redundant type dependent portions)
-  Use inheritance to design types (without redundancy) to aggregate data to correct regional level ( in addition to the code to aggregate to state level also use STL and region1->region2 hashmap to create regional data at various levels)
-  Caompare data at various regional levels


Orientation
============
At this point, we have a healthy amount of code (most of your lab04 solutions are over 1K lines of code -- which is still a very small software project, but 
is growing in complexity).  Assuming we would like to add yet another data source to build up more information in our software, it is worth taking a moment now
to reflect on the code we have and how to *simplify* that code.  The `spirit of the problem' for this assignment is the use of inheritance.

Good questions to consider are: <br>
-Where is there redundancy in my code?<br>
-What data is repeated or very similar? (that could potentially be simplified)<br>
-Where are there unique differences that must be preserved.

There are many ways we could re-write our current project, however, we will ask you to mostly follow a specific re-structuring, but we hope that this 
process allows you to explore the tools of OO (inheritance and polymorphism) and in general to think about design.

To motivate this re-structuring, look at parse.cpp for example, there are two functions that do almost the same thing:
```
std::vector<shared_ptr<demogData>> read_csv(std::string filename, typeFlag fileType);
std::vector<shared_ptr<psData> > read_csvPolice(std::string filename, typeFlag fileType);
```
The biggest difference in these functions is that they return a vector of different types, either demogData or psData.  The other difference is that based
on the type of data, the function either calls:
```
shared_ptr<demogData> readCSVLine(std::string theLine);
```
or
```
shared_ptr<psData> readCSVLinePolice(std::string theLine);
```

In addition to the above redundancy, there is likewise a small amount of redundancy in the state level representation of police shooting and demographic data.

Our goal is to use a powerful idea from OO programming, inheritance and polymorphism, to rethink our data types (demogData and psData) and consider what they
have in common and/or very similar *and* whether that commonality can be lifted into a new *parent* type unifying their representation.  

Specifically,
we will introduce several new data types to represent relationships in our data (to reduce redundant code).  Beginning with the introduction of *place data* as a more abstract concept, of which both police shooting data and demographic data are examples of *place data*.

Introducing these new types and using inheritance to codify the relationship between data, will allow us to simplify our code, 
and ultimately
make it easier to add any other new data that likewise is associated with a region or place!  

This will involve moving around much of the code you have.  Work slowly and use git to keep track of prior versions.

Very skeleton base code to fill in:

![](lab05.jpg)


Task 0 - Introduce new data types
============
Overall, you will be introducing new datatypes:
1) A base class: region data (this base class will unify all our data and represent the region name, state(s), and population)<br>
2) A derived class of region data that abstractly represents demographic data, *demogData* (only demographic data).  This is the data that previously was repeated in both the county and state data.<br>
3) A derived class of demographic data, *demogCombo* that represents combinations/aggregated regions of demographic data .  This should include any additional data, other than just demographic
data in order to represent aggregated data. <br>
4) A derived class of region data that represents individual police shooting incidents<br>
5) A derived class of region data that represents aggregate police shooting data, *psCombo* that represents combinations (aggregated) police shooting data<br>


Given this data and its relationships, you need to move data and getters/setters to their appropriate locations.  
Between demogData and demogCombo, you should not have *any* repeated
data members (You shoudl convince yourself that the types between psData and psCombo are different types).  You should have the minimal set of getters/setters.  You should only have certain methods (such as *addXtoAggregate* in the combo level of the data representations).

