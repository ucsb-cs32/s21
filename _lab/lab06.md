---
layout: lab
num: lab06	
ready: false
desc: "Visitor Design Patern - Part 2"
assigned: 2021-02-17 
due: 2021-02-24 23:59
github_org_url: https://github.com/ucsb-cs32-w21
---

Goals
=====

Learning objectives. At the end of this lab, students should be able to:

- Use helper functions to compute various statistics for collections (mean, standard dev. and correlation coefficient)(including a basic understanding the use of modern C++ standard algorithms used in the tools)
- Understand the basic ideas of these statistics and write test cases to confirm the provided tool works as expected
- Implement the visitor design pattern (part 2) to combine raw data to state and county level (re-design)
- Use your code to answer questions about the data (specifically focused on the parameters with the strongest correlation coefficients)
- Extra credit (extension) - add an additional visitor to combine data to a new level

Orientation
============
At this point, we have a fairly complex program to read in regional data (demographic and hospital) and aggreagate that data to various levels (county and state).  
We have considered extremums of the data and sorted the data and to understand the data, we can use some statistical methods to report information about the data.
Specifically, you will be provided with code to compute the mean, standard deviation and correlation coefficient for vectors of data.  Note that computing the correlation coefficient between two variables can indicate whether there is a relationship between those data vairables.
For a basic explanation see: https://www.statisticshowto.com/probability-and-statistics/correlation-coefficient-formula/

You are provided with implementations of these statistical tools that use modern standard algorithms (accumulate, inner_product, for_each and llambdas).  You should be able to read the provided code and understand how to identify the iterators and llambdas and basic functionality.  You will be asked to fill in an associated worksheet to demonstrate this knowledge. You will also be asked to write test cases to make sure these tools are behaving as expected.

In addition to this new statistical tool, for this lab with a basic understanding of the visitor pattern, we want to re-design our code to create two new visitors that allow us to combine the raw data into either state level regions or county level regions that can then be compared using the statistical tool.  This redesign will completely remove dataAQ and encapsulate the computation needed to aggregate into the visitors.  This is the primary task for this lab: to re-design our code and use the visitor pattern to collect regional data.

Once you have completed the re-design, you will write additional code to then gather vectors of the data (at various regional levels) and compare the correlation coefficient of various data.  You will fill in a table with your results

Step by Step
============

