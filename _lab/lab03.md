---
layout: lab
num: lab03	
ready: false
desc: "New types with operator overload and predicates (for sorting)"
assigned: 2021-01-27 
due: 2021-02-03 23:59
github_org_url: https://github.com/ucsb-cs32-w21
---

Goals
=====

Learning objectives. At the end of this lab, students should be able to:

- read example C++ code and understand the data representations used in the base code
- design and implment a new class to represent state region hospital data
- design, implement and use a new data representation (for a hospital `rating'), including implementing operator overload to aggregate and compare ratings
- aggregate city hospital data to state region hosptial data
- implement various compare predicates to sort state hospital data and state demographic data on various data fields *for example, list the top 5 states with the highest rated hospitals and print out the demographic data for this state or list the 5 states with the highest median income and the associated states hospital rating information

Orientation
============
In order to expand the questions/queries about the US data we have been working with, we will be adding additional data from CORGIS.
Specifically, we will be adding hospital data: https://corgis-edu.github.io/corgis/csv/hospitals/

Like before, take a look at the full list of data at the above link.  There are lots of intersting statistics, but to keep things simple, we will be working 
with just a subset of this data, related to hospital 'Rating'.  Specifically, in addition to identifying information about a hospital 
(Name, city, state, and type), we will look  at:<br>
Rating.Overall: Integer: Overall rating between 1 and 5 stars, with 5 stars being the highest rating; -1 represents no rating. 	<br>
Rating.Mortality: String: 'Above', 'Same', 'Below', or 'Unknown' comparison to national hospital mortality <br>
...
Rating.Readmission: String: 'Above', 'Same', 'Below', or 'Unknown' comparison to national hospital safety 	<br>

As our focus this week is not class design, I have provided you with a partial class to represent hospital data.  Please take a look at:
'HospitalData.h/cpp' - very similar to lab01, this includes some of the basics, but you need to add the final three peices of data (overall rating,
mortality rating and readmission rating *note for now we are skipping safety rating).

One of the interesting aspects of hospital data is that 'rating' is represented both numerically and as a word (or string in CS), depending upon the category.  
This makes our job of aggregating data more complex. 

This will be one of your first tasks, to create a data type for hosptial rating, that can be used as either numeric data or as a string.  Building this
type and its supporting operators is one of your key activities this lab (as you need to think about edge cases).  This task is described in detail below.

Next, take a moment and consider at what regional level hospital data resides, then consider the
problem that if we want to correlate hospital data with demographic data, how can we do this.  This will be one of your second challenges (which is very much
like your lab02).

Note that the hospital data from CORGIS is stored in a csv file: hosptials.csv
To support reading in this data, there is a new parse.cpp and parse.h, which reads in this new data (it is incomplete until you design the rating data type). 
*Note that if you look carefully at parse.cpp you will
see that there is a good deal of redundancy in the functions for reading hospital data or demographic data.  
This is something we will strive to fix next week.  

Task 1
============
Decide if you want to work with your lab02 code or from the starter code (either is fine, just know that if you work with your lab02 code you will want to integrate
some of the updated and new files in the starter code).  At this point the code will not run until you aggregate the hospital data to the state level (very much like you did in lab02.  

Like in Lab02, this will involve creating the state level hospital data class (fill in stateHosp.h and stateHosp.cpp).  Write the necessary code in dataAQ.h to
support the aggregation. Your goal is to get the code to compile without the full hospital data, just aggregate and count how many hospitals there are for each state (to test your data structure choices).  Right now hospitals only have identifying information (Name, city, state, and type as given to you). 
For now your state data should not include name and type.  Think about why (how do we aggregate names? how could we aggregate types)? 
What other designs might make sense.

As with lab02, there are many correct solutions.  I recommend using a hashmap of statenames to state hospital data.  We won't be able to fully aggregate the data until you build up your 'rating' class, but get the code to work at this point so you can feel confident about what needs to happen next.  

This task is very remniscent of lab02.  It isn't meant to be boring, but an opportunity to practice the same skills again.

Task 2
============
Now, what gets interesting about aggregating hospital data is their ratings (and specifically the challenge of aggregating those ratings).
Design and implement a 'rating' class that will allow our program the represent and aggregate both the numeric and string valued representation of hospital ratings.

To accomplish this, you need to think about your design.  A rating needs to simultaneously have a numeric and string rating.  One way to acccomplish some of
the tasks we want when aggregating the data is by overloading mathematical operators.  Specifically, think about the mathematical operators that will need to compute an average rating for the various hospital ratings we have identified.

Task 3
============
DRAFT (need to decide on these)
Similar to in lab02, we want to now compare the data in various ways.  We will do this via writing predicates and using some of the built in C++ algorithms, such as max_element and min_element and sort().

Specificaly, you will need to add support to dataAQ to support the following queries.

```
    string LowHospRating();
    string HighHospRating();
    string HighMortHospRating();
    string HighReadmitHospRating();
```

Once you have identified a state with these values, you need to then print that state's demographic data.  For example:

The state with the highest hospital readmission rating is: ID
State Hospital info: ID
  Number of hospitals: 42
  overall rating: 3.72
  mortality rating: same
  readmission rating: above

Demographic data for that state is:
State Info: ID
Number of Counties: 44
Population info: 
(over 65): 17.1659
(under 18): 25.3705
(under 5): 25.3705
Education info: 
(Bachelor or more): 20.25
(high school or more): 86.2159

------
50 points autograding
50 point code review
