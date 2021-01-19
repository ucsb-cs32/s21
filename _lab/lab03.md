---
layout: lab
num: lab03	
ready: false
desc: "Sorting"
assigned: 2021-01-27 
due: 2021-02-03 23:59
github_org_url: https://github.com/ucsb-cs32-w21
---

Goals
=====

Learning objectives. At the end of this lab, students should be able to:

- read C++ code and understand how data representation
- design a data representation (rating), including practice implementing operator overloading
- aggregate city data to county region (hosptial data)
- implement sort on a collection of data (selection sort)(?)(*implement code to list top ten states for earning bachelors)

Orientation
============
In order to expand the questions/queries about the US data we have been working with, we will be adding additional data from CORGIS.
Specifically, we will be adding hospital data: https://corgis-edu.github.io/corgis/csv/hospitals/

Like before, take a look at the full list of data at the above link.  There are lots of intersting statistics, but to keep things simple, we will be working 
with just a subset of this data, related to hospital 'Rating'.  Specifically, in addition to identifying information about a hospital 
(Name, city, state, and type), we will look  at:<br>
Rating.Overall: Integer: Overall rating between 1 and 5 stars, with 5 stars being the highest rating; -1 represents no rating. 	<br>
Rating.Mortality: String: 'Above', 'Same', 'Below', or 'Unknown' comparison to national hospital mortality <br>
Rating.Safety: String: 'Above', 'Same', 'Below', or 'Unknown' comparison to national hospital safety 	<br>

As our focus this week is not class design, I have provided you with a partial class to represent hospital data.  Please take a look at:
'HospitalData.h/cpp'

One of the interesting aspects of hospital data is that 'rating' is represented both numerically and a string, depending upon the category.  
This makes our job of aggregating data more complex. This will be one of your first tasks, to create a data type for hosptial rating. 

Next, take a moment and consider at what regional level hospital data resides, then consider the
problem that if we want to correlate hospital data with demographic data,how can we do this.  This will be one of your second challenges.

Note that the hospital data from CORGIS is stored in a csv file: hosptials.csv
To support reading in this data, there is a new parse.cpp and parse.h, which reads in this new data (in part, because you need to resolve the representation of
ratings). *Note that if you look carefully at parse.cpp you will
see that there is a good deal of redundancy in the functions (-).  This is something we will strive to fix next week.  Please just notice this redundancy 
this week and know that it is something we aim to address this quarter.

Step 1
============
Starting from your lab01 code, integrate the new files (-) and get the code to compile and run as is.  At this point, the hospital data is not super interesting
as it only has identifying information (Name, city, state, and type).

You need to fill in the Rating class to represent a hospital rating. Specifically, ...

Step 2
============
Aggregate the hospital to the state level.  This will be very similar to lab02.  There are many correct solutions.  I recommend using a hashmap of statename
hospital data (aggregating hospital ratings using the operators you overloaded in step 1).

Step 3
============
Sort the data based on various data values.  You can use comparators and std::sort().

