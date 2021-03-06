---
layout: lab
num: lab03	
ready: true
desc: "Using STL to aggregate data and query"
assigned: 2021-04-21
due: 2021-04-28 23:59
github_org_url: https://github.com/ucsb-cs32-s21
---

Goals
=====
<p>Learning objectives. At the end of this lab, students should be able to:</p>

<ul>
  <li>read and understand base C++ code (related to reading data from CSV file (all lab01))</li>
  <li>Use STL hashmaps to aggregate ‘county’ level data to ‘state’ data (including computing the average of the county data)</li>
  <li>Design and implement a C++ class representing state demographic data</li>
  <li>Utilize data aggregated into a hashmap to answer questions about the data (e.g. state with the youngest population)</li>
  <li>practice using a testing framework, including writing additional tests</li>
</ul>


Orientation
============
<p>In lab01, we developed code to read in county demographic data (age and education).  This week, our goal is to examine that data and be able to asnwer questions about regions in the USA.  For example, which region has the youngest population? Later in the quarter we will combine other datasets and be able to expand our queries.  We will also be adding one more piece of data related to the population below the poverty line.</p>

<p>The first step is deciding at what regional level we want to look at our data.  With over three thousand counties, we want to consider larger regions (by grouping counties).  There are lots of ways to understand regional data, but for this week we will look at state level data. Thus, one of the first tasks is to start aggregating county data together into states.</p>

<p>Once we have the data aggregated together, we will use various methods to identify extremes in the data (minimums and maximums) of various demographic fields.  <em>Although you have choices about the core tasks, you will need to wrap your solution in a class that we will use for testing.</em></p>

<p>This week’s lab is a bit different in that you will have choices about how to solve the primary aspects of the problem and then you will need
to implement a very specific class to help with testing.  Part of your lab grade will depend upon passing tests and another portion of the grade
depends on your code being reviewed by one of the teaching assistants or instructor.</p>

<p>In general, C++ has many tools to solve various aspects of this problem, it is just important that you
understand the tools you are using in your solution.  You can implement a solution to each of these tasks with the material that
has already been discussed in lecture.  Make sure you understand your solution as you will/may be asked to discuss your solution.</p>


Modality
============
This is a pair lab.  You may choose to work alone or with another student.  When working in a pair, please always follow good pair programming methodologies.  For example, see: https://gds.blog.gov.uk/2018/02/06/how-to-pair-program-effectively-in-6-steps/. In general, set aside time to work together and share your screen to share the work and learning.  

You will need to identify you partner (pair) in your submission (add a header to your main with both your names!).  The remaining labs will also be optional pair labs and you will be asked to only partner with the same person TWICE.


Tasks
============

Step 0: Getting Started - think about the problem
-----------------------

<h3 id="starting-from-your-code-last-week">Starting from your code from Lab01</h3>
<p>There are various ways to tackle this problem.  To start, make sure you understand the problem.  Given county level data, we want to average all
the county data for a given state together and then be able to query the maximums and minimums of any of the data fields. See below note about averaging
percentages and guidelines to make sure are averaging correctly.</p>

<p>There are some clear cut tasks, but the order and exact implementation is somewhat up to you, with the exception of the <b>dataAQ class</b>, for which you <em>must</em> implement the specified functions for use in testing.</p>

<p>In general, to solve this problem, we must aggregate county data into states.  This means having an implementation to collect all the counties for a 
given state <b>and</b> combine the county’s demographic data to state level data.  For this assignment, to combine the data, we will add up the appropirate county data in our data set for its associated state and report both counts and percentages for the state.</p>

<p>Download all the new files from: <ahref="https://github.com/ucsb-cs32-s21/Lab03-STARTER">https://github.com/ucsb-cs32-s21/Lab03-STARTER</a>
  Note that some of the files are blank, but you need to use these files (for naming convention for testing).
You will need all your finished code (including demogData.h/cpp and tddFuncs.h and .cpp) from Lab01</p>. *The current STARTER code has the starter code for Lab01, which is missing key aspects that you implmented in Lab01 - so you need to combine any new files and all your code from lab01 into one 
folder.* (You will not need testDemog1.cpp or testDemog2.cpp)

<p>Recall that when we think about a problem, one of the first tasks is to consider the ‘data’ associated with that problem (and then closely related, to consider the data structures 
we can use to build up necessary data relationships).  There are multiple valid solutions here, but for this lab we do expect to see solutions to the following general tasks. 
  You can tackle them in whatever order makes sense to you, but we will be looking for these aspects in your solution.</p>

<p>Regardless of exactly how you solve the following tasks, you must support the specified queries as a part of the dataAQ class.  Make sure you understand exactly how your solution will be tested before you dive in too deep.</p>

<p>Do create a new github repo for this weeks lab.  We will be looking at your code via github.</p>

A note about averaging percentages of populations
-----------------------
As mentioned in lab01, we can not average our percentages because the counties have different numbers of residents.  When averaging for the 
state, you will need to use the *count* data per data field and the total population of the counties.  

In your code, when transforming the county percentages to counts, represent the counts as whole numbers and use round to convert from any decimal valued number to a whole number.  This is because a decision was made upstream from our application about the precision of the percentages, thus we will sometimes generate decimal valued numbers, however, the number of people (count) of a given population in a county should be a whole number (i.e. 123 people makes sense, while 122.7 people is not as sensible).  And remember to watch out for integer division. 

Then when designing your state data, also store a total state population and think about how to aggregate the county data 
(for example, during aggregation compute total states counts which can be converted to percentages of the total state population, 
after all county data has been aggregated together).

Task 0:
-----------------------
Consider any re-designs you may want to make to demogData to support how we need to total data for states.
Add the data from the CSV file for the percentage of the population below the poverty line.  This data should be added to demogData.h/cpp and any necessary modifications to parse.cpp.

Task 1 and 2: Representing 'state' data
-----------------------
<h3 id="design-and-implement-a-class-to-represent-state-data">Design and Implement a class to represent ‘state’ data</h3>
<p>Ultimately, we will want to conduct simple data analysis on state level data (i.e. which state has the most people with Bachelor’s degrees), etc. 
Design a class to represent state level demographic data.  Again, there are multiple valid solutions here.  Design a solution that makes sense to you.</p>

<p><b>At this point we ask that you do not use inheritence or polymorphism</b> - that will come in future weeks. Designing a solution without them will help motivate their use in later labs.</p>

<p>The state data should have the same demographic information that the county data has, that is age, education, and poverty level.  State data could have any additional
  data to represent that it is aggregate. But, yes, this does mean you will have 
two classes that are very similar but represent different regional zones (as mentioned above, we will revisit this design as we expand our data project).</p>

<p>This class should be implemented in the empty provided files demogState.h and demogState.cpp.</p>

<h3 id="create-and-propogate-data-into-a-hashmap-to-aggregate-county-data-to-state-data"></h3>
  We will be using the dataAQ class to aggregate and query our state data.  Take a look at the header file and member function stubs.  It is here that you will
  create and propagate data into a hashmap to aggregate county data to state data.  (For example, see the declaration of a dataAQ in main and the function call used once the data has been read in from csv file to *createStateData*
<p>Use an STL hashmap in order to associate any county data with it’s state (i.e. recall our demogData class has a string which is the 
  name of the state where that county is located).  Again you have choices here.  Do what makes sense for your solution.
</p>

<p>Depending on the order you tackle these tasks, don’t forget that one task is to combine the demographic data for all counties into state level demographic data.  
  

<h2 id="task-3-use-data-represenation-stl-hashmap-to-be-able-to-answer-queries-about-data">Task 3: Use data representation (STL hashmap) to be able to answer queries about data</h2>

<p>Once you have a colletion of state level data, we should be able to identify extremums (maximum and minimums) for any of the data fields (or combination of data fields).</p>

<p>Your solution should be general, i.e. we should be able to ask for you to be able to find extremes of <b>any</b> of the data fields (and you should
expect we will do this during your code review).</p>

<h2 id="task-4-testing---implement-the-dataaq-class-exactly-as-specified-for-testing">Task 4: Testing - implement the dataAQ class exactly as specified for testing</h2>
<h3 id="specific-cases-that-must-match-output-eg-state-with-the-youngest-population">specific cases that must match output (e.g. state with the youngest population)</h3>

<p>Work on filling in the specified methods in dataAQ.cpp.  See testStates.cpp for example of how this class will be used.  Again, the exact implementation is up to you, but your dataAQ class must support the following methods:</p>


```
//data aggregator and query for testing<br />
class dataAQ {
  public:
    dataAQ();
    //function to aggregate the data - this CAN and SHOULD vary per student - depends on how they map
    void createStateData(std::vector< shared_ptr<demogData> > theData); (*)
    //return the name of the state with the largest population under age 5
    string youngestPop();
    //return the name of the state with the largest population under age 18
    string teenPop();
    //return the name of the state with the largest population over age 65
    string wisePop();
    //return the name of the state with the largest population who did not finish high school
    string underServeHS();
    //return the name of the state with the largest population who completed college
    string collegeGrads();
    //return the name of the state with the largest population below the poverty line
    string belowPoverty(); 

    //getter given a state name return a pointer to demogState data
    shared_ptr<demogState> getStateData(string stateName) { /*fix this*/  return nullptr; }
    
    //must implement output per aggregate data
    friend std::ostream& operator<<(std::ostream &out, const dataAQ &allStateData);

    //additional methods AND data to support above methods.  You are allowed for data to be public
    ...
 };
```
  
<p>Again, see testStates.cpp for the use of the dataAQ class to test your implementation.</p>

<p> Note that we are computing the ranking on percentages of populations not total populations.  That is we are treating each state as equal, so even though
  California has a larger number of people under the age of 5 than Utah, we rank Utah as the state with the largest pre-school need because it is the state with the highest percentage of its population 5 and under.

<p>You are encouraged to write additional test cases for each of the required queries in dataAQ.</p>

<p>The output for dataProj should include a complete version of the following (your code would fill in for <b>BLANK</b>):</p>

```
*** the state that needs the most pre-schools**
State Info: UT
Number of Counties: 29
Population info: 
(over 65): 10.03% and total: 295146
(under 18): 30.71% and total: 903830
(under 5): 8.58% and total: 252378
Education info: 
(Bachelor or more): 30.54% and total: 898886
(high school or more): 91.01% and total: 2678412
persons below poverty: 12.67% and total: 372832
Total population: 2942902
*** the state that needs the most high schools**
State Info: BLANK
Number of Counties: BLANK
Population info: 
(over 65): BLANKand total: BLANK
(under 18): BLANK and total: BLANK
(under 5): BLANK and total: BLANK
Education info: 
(Bachelor or more): BLANK and total: BLANK
(high school or more): BLANK and total: BLANK
persons below poverty: BLANK and total: BLANK
Total population: BLANK
*** the state that needs the most vaccines**
State Info: BLANK
Number of Counties: BLANK
Population info: 
(over 65): BLANKand total: BLANK
(under 18): BLANK and total: BLANK
(under 5): BLANK and total: BLANK
Education info: 
(Bachelor or more): BLANK and total: BLANK
(high school or more): BLANK and total: BLANK
persons below poverty: BLANK and total: BLANK
Total population: BLANK
*** the state that needs the most help with education**
State Info: BLANK
Number of Counties: BLANK
Population info: 
(over 65): BLANKand total: BLANK
(under 18): BLANK and total: BLANK
(under 5): BLANK and total: BLANK
Education info: 
(Bachelor or more): BLANK and total: BLANK
(high school or more): BLANK and total: BLANK
persons below poverty: BLANK and total: BLANK
Total population: BLANK
*** the state with most college grads**
State Info: BLANK
Number of Counties: BLANK
Population info: 
(over 65): BLANKand total: BLANK
(under 18): BLANK and total: BLANK
(under 5): BLANK and total: BLANK
Education info: 
(Bachelor or more): BLANK and total: BLANK
(high school or more): BLANK and total: BLANK
persons below poverty: BLANK and total: BLANK
Total population: BLANK
*** the state with most population below the poverty line**
State Info: BLANK
Number of Counties: BLANK
Population info: 
(over 65): BLANKand total: BLANK
(under 18): BLANK and total: BLANK
(under 5): BLANK and total: BLANK
Education info: 
(Bachelor or more): BLANK and total: BLANK
(high school or more): BLANK and total: BLANK
persons below poverty: BLANK and total: BLANK
Total population: BLANK
```


For clarity, the questions in main, refer to the queries in dataAQ (i.e. 'most' refers to a ranking in proportion to the state's whole population, not
total count).  Thus:<br>
-the state that needs the most pre-schools: should be the state with the largest percentage of its population under age 5<br>
-the state that needs the most high schools: should be the state with the largest population under age 18<br>
-the state that needs the most vaccines: should be the state with the largest population over age 65<br>
-the state that needs the most help with education: should be the state with the largest population who did not finish high school<br>
-the state with most college grads: should be the state with the largest population who completed college<br>
-the state with largest percent of the population below the poverty line: should be the state with the largest population who live below the poverty line<br>


Grading
-----------------------
(70) tests passed (GS)<br>
(10) reasonable state data design<br>
(10) reasonable aggregation computation<br>
(10) reasonable reporting of mins and max in dataAQ<br>


Acknowledgements
================

Winter `21 vesion: Zoë Wood.  Thank you to the original CORGIS crew for their work sharing this data (https://corgis-edu.github.io/corgis/) and to Aaron Keen for curriuclum review. Editing, autograder and general support to thanks to: AMR, SDM, QH, AR, BL
