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
-  Use polymorphism 
-  Use inheritance to design types (without redundancy) to aggregate data to correct regional level (or aggregate/combine data for a designated criteria)
-  Compare aggregated data


Orientation
============
At this point, we have a healthy amount of code (most of your lab04 solutions are over 1K lines of code -- which is still a very small software project, but 
is growing in complexity).  Assuming we may want to add yet another data source to build up more information in our software, it is worth taking a moment now
to reflect on the code we have and how to *simplify* that code *or* more importantly for this week's lab, if you need to aggregate data based on varied criteria (i.e. state or all data of a given type or value - i.e. aggregate all counties with percentage of the population at varied thresholds).  The `spirit of the problem' for this assignment is the use of inheritance.

Good questions to consider are: <br>
-Where is there redundancy in my code?<br>
-What data is repeated or very similar? (that could potentially be simplified)<br>
-Where are there unique differences that must be preserved.
-How can we use polymorphism to increase functionality in our code?

There are many ways we could re-write our current project, however, we will ask you to mostly follow a specific re-structuring, but we hope that this 
process allows you to explore the tools of OO (inheritance and polymorphism) and in general to think about design.

One aspect motivating this re-structuring is to simplify parse.cpp. Specifically, there are two functions that do almost the same thing:
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

In addition to the above redundancy, there is likewise a large amount of redundancy in the state level representation of county level demographic data and state level demographic data (convince yourself this is less true for police shooting data).

Our goal is to use a powerful idea from OO programming, inheritance and polymorphism, to rethink our data types (demogData and psData) and consider what they
have in common and/or very similar *and* whether that commonality can be lifted into a new *parent* type unifying their representation.  

Specifically,
we will introduce several new data types to represent relationships in our data (to reduce redundant code AND to enhance our ability to aggreagate data based on varied criteria).  Beginning with the introduction of *regiondata* as a more abstract concept, of which both police shooting data and demographic data are examples of *region data*.

Introducing these new types and using inheritance to codify the relationship between data, will allow us to simplify our code, 
and ultimately make it easier to aaggregate data and for future considerations, add any other new data that likewise is associated with a region or place!  

This will involve moving around much of the code you have.  Work slowly and use git to keep track of prior versions.

The below figure represents the hierarchy we will all be following:
![](lab05.jpg)

Very skeleton base code to fill in:

Modality
============
This is a pair lab.  You may choose to work alone or with another student.  When working in a pair, please always follow good pair programming methodologies.  In general, set aside time to work together and share your screen to share the work and learning.  

You will need to identify you partner (pair) in your submission (add a header to your main with both your names!).  The remaining labs will also be optional pair labs and you will be asked to only partner with the same person TWICE.

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

A note about regionData, for the first few tasks, region data just needs a singular state value, you will need to revisit this when you get to step 3 in task 1.  Start with a single string and then re-write when you pass all prior tests.

Task 1 - Use the new data types
============
Once this is complete, you will then need to tackle:

1) modify parse.cpp to only have one function that reads in csv data into a vector of placeData
```
std::vector<shared_ptr<regionData>> read_csv(std::string filename, typeFlag fileType);
```
In main.cpp, instead of vectors of police shooting and demographic data, create two vector of regionData and call read_csv (pass the appropriate type and in read_csv, depending upon the type, call the correct readCSVLine).  *Modify the constructor to call the correct constructor for the appropriate type.*. Note we are still using two separate vectors but their type in main and when passed to the function should both be regionData.

2) modify dataAQ.h/.cpp and main.cp to use these new data types.  Carefully think about which type of the data various operations need to be.  Try to make
your code as general as possible.  Test that your code works as expected in that it can produce the same output as lab04.  There are updated autograders for the same tests as lab04 but using the new type that you should make sure you can pass once you have the re-write complete.

3) Now write the new method in dataAQ to aggregate either data using some data valued criteria.  Please name the method:
```
    void createComboDemogDataKey(std::vector<shared_ptr<demogData> >& theData);
    void createComboPoliceDataKey(std::vector<shared_ptr<psData> >& theData);
```
These methods would sometimes be used instead of:
```
    void createComboDemogData(std::vector<shared_ptr<demogData> >& theData);
    void createComboPoliceData(std::vector<shared_ptr<psData> >& theData);
```
And will aggregate into your map using a specific key function.  For example:
```
string makeKeyExample(shared_ptr<demogData> theData) {

  string theKey = "Key";

  if (theData->getBelowPoverty() < 10) {
    theKey += "BelowPovLessTenPer";
  } else if (theData->getBelowPoverty() < 20) {
    theKey += "BelowPovLessTwentyPer";
  } else if (theData->getBelowPoverty() < 30) {
    theKey += "BelowPovLessThirtyPer";
  } else {
    theKey += "BelowPovAboveThirtyPer";
  }

  return theKey;
}
```
Stay tuned for specifics on which key to use for psData.  When using this key to aggregate data, example results for printing all data would look like.
```
Combo Demographic Info: key: KeyBelowPovAboveThirtyPer
Combo Info: AK, AL, AR, AZ, GA, ID, IL, KY, LA, MI, MS, MT, NC, ND, NM, OH, SC, SD, TN, TX, VA, WA, WI, WV, total states: 24
Number of Counties: 117 County Demographics Info: comboData, many
Population info: 
(over 65): 12.31% and total: 508433
(under 18): 27.12% and total: 1120039
(under 5): 7.73% and total: 319328
Education info: 
(Bachelor or more): 17.60% and total: 726966
(high school or more): 71.44% and total: 2950441
persons below poverty: 33.95% and total: 1402079
Total population: 4129981
Racial Demographics Info: 
% American Indian and Alaska Native percent: 7.53 count: 310799
% Asian American percent: 1.15 count: 47561
% Black/African American percent: 18.45 count: 762136
% Hispanic or Latinx percent: 40.51 count: 1672996
% Native Hawaiian and Other Pacific Islander percent: 0.06 count: 2453
% Two or More Races percent: 1.13 count: 46721
% White (inclusive) percent: 71.66 count: 2959502
% White (nonHispanic) percent: 32.41 count: 1338572
total Racial Demographic Count: 4129981
key: KeyBelowPovLessTenPer
Combo Info: -
Number of Counties: 431 County Demographics Info: comboData, many
Population info: 
(over 65): - and total: -
(under 18): - and total: -
(under 5): - and total: -
Education info: 
(Bachelor or more): - and total: -
(high school or more): - and total: -
persons below poverty: - and total: -
Total population: -
Racial Demographics Info: 
% American Indian and Alaska Native percent: - count: -
% Asian American percent:-
% Black/African American percent: -
% Hispanic or Latinx percent: -
% Native Hawaiian and Other Pacific Islander percent: -
% Two or More Races percent: -
% White (inclusive) percent: -
% White (nonHispanic) percent: -
total Racial Demographic Count: -
...
```
Note for this kind of aggregate, you need to keep track of more than one state in region (and not keep duplicates) - use a std::set to accomplish this.

-----

    
Grading
================
(70) autograder tests passed (GS):   <br>
(30) code review of various aspects



    
Acknowledgements
================

Spring`21 vesion: Zoë Wood.  Thank you to JO and BZF for assistance with the data exploration project and the cleaned Washington Post data.


