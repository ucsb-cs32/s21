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

Learning objectives. At the end of this lab, students should be able to:

-  Implement the visitor design pattern for the exisiting code to support two different visitors (one to report data, the other to collect data)
-  In conjunction with the visitor implementation, use helper functions to compute various statistics for the region data (mean, standard deviation and correlation coefficient)
- Practice writing test cases to confirm the functionality of provided code


Orientation
============
At this point, we have a fairly complex program to read in regional data (demographic and hospital) and aggreagate that data to various levels (county and state).  
We have considered extremums of the data and sorted the data and to understand the data, we can use some statistical methods to report information about the data.
Specifically, computing the correlation coefficient between two variables can indicate whether there is a relationship between those data vairables.
For a basic explanation see: https://www.statisticshowto.com/probability-and-statistics/correlation-coefficient-formula/

With OO programming, there are some design patterns that can be used 'to solve recurring design problems to design flexible and reusable object-oriented software, that is, objects that are easier to implement, change, test, and reuse' (https://en.wikipedia.org/wiki/Design_Patterns)


