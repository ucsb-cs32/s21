---
layout: lab
num: lab04	
ready: false
desc: "New type and predicates (for sorting)"
assigned: 2021-04-27 
due: 2021-05-05 23:59
github_org_url: https://github.com/ucsb-cs32-w21
---

Goals
=====

Learning objectives. At the end of this lab, students should be able to:

- read example C++ code and understand the data representations used in the base code
- design and implement a new class to represent police shootings (which supports aggregation and comparisons)at two regional levels (county and state)
- use a new data representation for racial demographics (including integration into exisiting code)
- aggregate regional data to state level data using a hashmap
- implement various *compare predicates* to sort regional data and state demographic data on various data fields 
*for example, list the top 10 states in order based on highest number of police shooting incidents and print out the demographic data for these states or list the 5 states with the lowest percentage of people below the poverty line and the associated police shooting information


Orientation
============
In order to expand the questions/queries about the US data we have been working with, we will be adding additional data from CORGIS. Specifically, we will be adding regional data reporting police shootings: https://corgis-edu.github.io/corgis/csv/police_shootings/ However, there is a more up to date version of this data, compiled by the Washington Post that has been cleaned by UCSB students working on a data project.  The exact csv file we will be using is included in the STARTER code and is called: police_shootings_cleaned.csv

There is lots of important data for each incident, but we will focus on the fields:
name,age,gender,race,county,state,signs_of_mental_illness,flee
Note there is other data associated with each incident, but you will need to design a class to represent the specified data, called policeData.  We will be representing and aggreating this data into state level information (similar to lab03).  

An important data component for both the demographic census data and the police shooting data is racial demographic data.  To support this, you are provided with a new (mostly complete) data type raceDemogData.  Personal and community identity with respect to race and ethnicity are complex topics.  This page describes the categories used in the US Census and some reasons why this data is collected: https://www.census.gov/topics/population/race/about.html  Developing an understanding of civil rights issues faced by our nation involve representing and examining data related to race.  One of your tasks for this lab is to integrate this data type into your code.

Once you have expanded your code to represent this new data (police shootings at the county level and aggregated to the state level) and you have integrated the raceDemogData, we will practice using the standard sorting algorithm, by writing some specified compare predicates to sort the data on various fields.  Your program will also need to report various data findings.

To support reading in the new csv data (police_shootings_cleaned.csv), there is a new parse.cpp and parse.h, which reads in this new data (it is incomplete until you design and integrate the new types).  *Note that if you look carefully at parse.cpp you will see that there is a good deal of redundancy in the functions for reading police data or demographic data. This is something that will be addressed in next weeks lab.

Tasks
============
Starting with your lab03 code take a look at the new files and integrate the new files (and modified files).  
<p>
-Familiarize yourself with the raceDemoData.h/cpp and be sure you understand what it represents<br>
-Start by designing the Police Data representation in policeData.h/cpp<br>
-Design the state level Police Data representation in policeState.h/cpp<br>
-Modify parse.cpp to support the use of the new data types<br>
-Modify dataAQ.h/cpp to support aggregating the police data to the the state level<br>
-Confirm that your output can match the example below<br>
-Use sort to sort state data based on various criteria and report<br>

Example report
============
```
State Demographic Info: State Info: AK
Number of Counties: 29
Population info: 
(over 65): 9.44% and total: 69541
(under 18): 25.32% and total: 186508
(under 5): 7.45% and total: 54857
Education info: 
(Bachelor or more): 27.29% and total: 201059
(high school or more): 91.51% and total: 674168
persons below poverty: 9.86% and total: 72611
community racial demographics: Racial Demographics Info: 
% American Indian and Alaska Native percent: 14.79 count: 108954
% Asian American percent: 6.06 count: 44663
% Black/African American percent: 3.90 count: 28731
% Hispanic or Latinx percent: 6.81 count: 50152
% Native Hawaiian and Other Pacific Islander percent: 1.27 count: 9352
% Two or More Races percent: 7.09 count: 52270
% White (inclusive) percent: 66.86 count: 492579
% White (nonHispanic) percent: 61.95 count: 456399
total Racial Demographic Count: 736732
Total population: 736732
**Police shooting incidents:State Info: AK
Number of incidents: 44
Incidents with age 
(over 65): 0
(19 to 64): 42
(under 18): 2
Incidents involving fleeing: 18
Incidents involving mental illness: 7
Male incidents: 42 female incidents: 2
Racial demographics of state incidents: Racial Demographics Info: 
% American Indian and Alaska Native percent: 21.95 count: 9
% Asian American percent: 4.88 count: 2
% Black/African American percent: 7.32 count: 3
% Hispanic or Latinx count: 0
% Native Hawaiian and Other Pacific Islander count: 0
% Two or More Races count: 0
% White (inclusive) count: 0
% White (nonHispanic) percent: 65.85 count: 27
total Racial Demographic Count: 41
------------
State Info: AL
```

Grading
-----------------------
(50) tests passed (GS)<br>
(20) reasonable data designs<br>
(20) reasonable aggregation computation<br>
(10) reasonable sorting and reporting<br>


Acknowledgements
================

Spring`21 vesion: Zoë Wood.  Thank you to JO and BZF for assistance with the data exploration project and the cleaned Washington Post data.

