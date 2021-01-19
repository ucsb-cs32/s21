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

-   sort a collection of data (selection sort)
- (*top ten states for earning bachelors)

Orientation
============
In order to expand the questions/queries about the data we have been working with, we will be adding additional data from CORGIS.
Specifically, we will be adding hospital data: https://corgis-edu.github.io/corgis/csv/hospitals/

Like before, take a look at the full list of data.  There are lots of intersting statistics, but to keep things simple, we will be working 
with just a subset of this data, related to hospital 'Rating'.  Specifically, in addition to identifying information about a hospital 
(Name, city, state, and type), we will look  at:<br>
Rating.Overall	Integer 	Overall rating between 1 and 5 stars, with 5 stars being the highest rating; -1 represents no rating. 	<br>
Rating.Mortality 	String 	Above, Same, Below, or Unknown comparison to national hospital mortality <br>
Rating.Safety 	String 	Above, Same, Below, or Unknown comparison to national hospital safety 	<br>

As our focus this week is not class design, I have provided you with a class to represent hospital data.  Please take a look at:
`HospitalData.h/cpp'

One of the interesting aspects of hospital data is that hospital 'ratings' are represented both numerically and a string.  This makes our job of 
aggregating data more complex.  Take a moment and consider at what regional level hospital data resides.

Note that the hospital data from CORGIS is stored in a csv file: hosptials.csv
To support reading in this data.  There is a new parse.cpp and parse.h, which read in this new data. *If you look carefully at parse.cpp you will
see that there is a good deal of redundancy in the functions (-).  This is something we will strive to fix next week.  Please just notice this redundancy 
this week.


Starting from your lab01 code...
