---
layout: lab
num: lab04	
ready: false
desc: "OO polymorphism/inheritence"
assigned: 2021-02-03 
due: 2021-02-10 23:59
github_org_url: https://github.com/ucsb-cs32-w21
---

Goals
=====

Learning objectives. At the end of this lab, students should be able to:

-  Revise exisiting code to lift shared data and members to a parent class (implement inheritence to simplify our exisiting code base)
-  Reduce redundancy in code by using inheritence (re-write parse.cpp to reduce redundent type dependent portions)
-  Aggregate data to correct regional level (use STL and city->county hashmap to create 'county' level hospital data)
-  Possibly add new class for new data types (police)


Orientation
============
At this point, we have a healthy amount of code (most of your lab03 solutions are over 1K lines of code -- which is still a very small software project, but 
is growing in complexity).  Assuming we would like to add yet another data source to build up more information in our software, it is worth taking a moment now
to reflect on the code we have and how to *simplify* that code.

Good questions to consider are: <br>
Where is there redundancy in my code?<br>
What data is repeated or very similar? (that could potentially be simplified)<br>
where are there unique differences that must be preserved.

If we look at parse.cpp for example, there are two functions that do almost the same thing:
```
std::vector<shared_ptr<demogData>> read_csv(std::string filename, typeFlag fileType);
std::vector<shared_ptr<hospitalData> > read_csvHospital(std::string filename, typeFlag fileType);
```
The biggest difference in these functions is that they return a vector of different types, either demogData or hospitalData.  The other difference is that based
on the type of data, the function either calls:
```
shared_ptr<demogData> readCSVLineDemog(std::string theLine);
```
or
```
shared_ptr<hospitalData> readCSVLineHopstial(std::string theLine);
```

Our goal is to use a powerful idea from OO programming, inheritence, to rethink our data types (demogData and hospitalData) and consider what they
have in common and/or very similar *and* whether that commonality can be lifted into a new *parent* type unifying their representation.  

Specifically,
we will introduce a new data type to represent *region data* as a more abstract concept.  Both hospital data and demographic data are examples of *region data*.

Introducing this new type and using inheritence to codify the relationship between these two kinds of data, will allow up to simplify our code, 
and ultimately
make it easier to add any other new data that likewise is associated with a region!  This abstraction will also allow us to remove some redundancy 
between city, county or state level data.


Step by Step
============

Working from your lab03, introduce a new type *region data* that will be a parent class to our primary data.


