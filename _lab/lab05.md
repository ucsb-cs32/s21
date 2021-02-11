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
We have considered extremums of the data and sorted the data and to understand the data, we can use some statistical methods to report information about the data.
Specifically, computing the correlation coefficient between two variables can indicate whether there is a relationship between those data vairables.
For a basic explanation see: https://www.statisticshowto.com/probability-and-statistics/correlation-coefficient-formula/

With OO programming, there are some design patterns that can be used 'to solve recurring design problems to design flexible and reusable object-oriented software, that is, objects that are easier to implement, change, test, and reuse' (https://en.wikipedia.org/wiki/Design_Patterns)


