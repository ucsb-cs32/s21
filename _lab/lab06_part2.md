---
layout: lab
num: lab06
ready: true
desc: "Visitor Design Patern - Part 2"
assigned: 2021-05-20
due: 2021-05-27 23:59
github_org_url: https://github.com/ucsb-cs32-s21
---

Goals
=====

This is a two part lab.  This second half of the lab explores the concepts in more detail with larger code revisions.  Learning objectives. At the end of this lab, students should be able to:

- Use helper functions to compute various statistics for collections (mean, standard dev. and correlation coefficient)(including a basic understanding the use of modern C++ standard algorithms used in the stats tools provided)
- Use helper code to gather data from our exisiting classes into vectors (understand and use function pointer and function objects).
- Understand the basic ideas of these statistics and write test cases to confirm the provided tool works as expected (including understanding when to use population)
- Implement the visitor design pattern (part 2) to combine raw data to aggregated data
- Use your code to answer questions about the data (specifically focused on computing correlation coefficients for various pairs of data values)

Modality
============
This is a pair lab.  You may choose to work alone or with the same person you worked with part 1.

Orientation - part 2
============
For part 2, we have considered extremums of the data and sorted the data and to understand the data, we can use some statistical methods to report information about the data.
Specifically, you are provided with code to compute the mean, standard deviation and correlation coefficient for vectors of data.  You are also provided with a tool to gather data from our aggregated data into vectors for ease of use when computing statistics.  Note that computing the correlation coefficient between two variables can indicate whether there is a relationship between those data variables.
For a basic explanation see: https://www.statisticshowto.com/probability-and-statistics/correlation-coefficient-formula/

You are provided with implementations of these statistical tools that use modern standard algorithms (accumulate, inner_product, for_each and llambdas).  You should be able to read the provided code and understand how to identify the iterators and llambdas and basic functionality.  You will be asked to fill in an associated worksheet to demonstrate this knowledge. You will also be asked to write test cases to make sure these tools are behaving as expected.

In addition to this new statistical tool (stats.h/cpp), the heart of this lab is to extend our basic understanding of the visitor pattern to re-design our code to create new visitors that are redesign of our code to combine the raw data into aggregate levels that can then be compared using the statistical tool.  This redesign will completely remove dataAQ and encapsulate the computation needed to aggregate data for the different types.  The primary task of this lab is to re-design our code and use the visitor pattern to separate the algorithm to aggregated data into concrete visitor algorithms.

Once you have completed the re-design, you can use the additional new tools (stats.h/cpp and statTool.h/cpp) to gather vectors of the data (at various regional levels) and compare the correlation coefficient of various data pairings.  You will need to use these tools to fill out a works sheet with specific information.

Set up tasks for part 2 
============
There are new files (including the stats functions and example test cases) that can be found here: 
https://github.com/ucsb-cs32-s21/lab06-part2-STARTER-ADDFILES

Start by adding your files from *part 1* to a new lab06 directory and add these new files as well and try to compile.  Resolve any compilation issues as you complete your re-design. 

One of your first tasks is to make sure you understand and validate the new statistical functions provided to you in stats.h/cpp.  Looking at the base code, read through the code and answer the questions at: Lab06-worksheet (see gauchospace).  

In addition, when given a new tool or set of code, it is always good to make sure you understand the tool and validate the tool is behaving as expected.  
In particular, since our data represents population information represented as both counts and percentages, we need to make sure we use the right data with each of the tools.  In general, for the mean, you need to use the demographic counts (and pass in the total population) for the various regions.  *The mean for any given demographic data should be the same at both a county and state level.*

As a first test that stats.h/cpp is working as expected, edit testStats1.cpp and uncomment the final asserts.  You will need to find an online statistical calculator or use an external method to  compute what the correct values should be and then test the tool to make sure it is working as expected. *Additional tests will be added to test your understanding of the percent vs count.


Redesign tasks for part 2 
============

The heart of this lab is to redesign the way we create aggregate data.  
First, we will take advantage of the shared type 'regionData' and create one large shared vector of raw data:
```
    std::vector<shared_ptr<regionData>> pileOfData;
```

Re-write read_csv in parse.cpp to take in a reference to a vector of region data, so that you can add onto the one vector of data:
```
   //read in the police data
    read_csv(pileOfData, "police_shootings_cleaned.csv", POLICE)
   
    //read in the demographic data
    read_csv(pileOfData, "county_demographics.csv", DEMOG); 
```

Now that we have one big pile of data, we will use the visitor design pattern to create new visitors that we can use on the big pile of data to 
do the correct aggregation computation for the two different types of data (police shootings and demog data) at various regional levels (or keyed).  

Specifically, you will introduce a new class derived from visitor called visitorCombine.  (See added files for structure).  This class should store the aggregated data and allow access to it.

From this class, you will write three concrete visitors: visitorCombineCounty, visitorCombineState, visitorCombineKey each which appropriately aggregate the data.
```
class visitorCombineState : public visitorCombine 
class visitorCombineKey : public visitorCombine 
class visitorCombineKey: public visitorCombine 

```

As their name suggests these visitors will combine data into either state level data or criteria based data.  Your job is to write these classes and their associated methods.  
You will want to move the hashmaps that represent the aggregate data into the visitorCombine class, but not make the data public. 
Along with getter methods returning the appropriate types needed to access this data named:
```
    shared_ptr<demogCombo> getComboDemogData(string regionName) {  } //fill in
    shared_ptr<psCombo> getComboPoliceData(string regionName) {  } //fill in

	std::map<string, shared_ptr<demogCombo> >& getComboDemog()  {  } //fill in
    std::map<string, shared_ptr<psCombo> > & getComboPolice() {  } //fill in

````

Note that for county data, we need to be able to create vectors of data for matching counties, so think about what you will need to do for demogData, to organize the counties in a way that you can pair the data with the associated poilce shooting data.  

Once you are done, the code in statsTool.cpp should be able to work, which just loops through the pile of data and calls accept with the different visitor types:
```
void statTool::createStateData(std::vector<shared_ptr<regionData>>& theData, Visitor& theStates) {

   //use visitor pattern to be able to aggregate
    for (const auto &obj : theData) {
        obj->accept((visitorCombineState&)theStates);
    }
}
```
Likewise for the other methods.

Note that when working with the visitor pattern and smart pointers, you likely want to look into:
```
std::enable_shared_from_this
```
See https://en.cppreference.com/w/cpp/memory/enable_shared_from_this for more information (or the lecture slides).


Stats Tasks for part 2
============
Once we have the aggregate data at various levels, we want to make vectors of specific data members to compute interesting statistics.  

To help with this task, you can use statTool.h/cpp. These methods, call the appropriate
stats method depending on if the data is only dmeographic (population) or if it is mixed demographic and police shooting (sample).

In statTool.cpp you are provided with implementations for the following:
```
/*
/* call visitor pattern to create state data */
  static void createStateData(std::vector<shared_ptr<regionData> >& theData, Visitor& theStates);

  /* call visitor pattern to create county data */
  static  void createCountyData(std::vector<shared_ptr<regionData> >& theData, Visitor& theCounties);
  
  /* call visitor pattern to create aggregate data using a specific criteria */
  static  void createKeyData(std::vector<shared_ptr<regionData> >& theData, Visitor& theAggregator);

  /* helper functions to fill in arrays based on funciton pointers  - on mix*/
  static void gatherCountStats(visitorCombine* theAggregate, vector<double> &XPer, vector<double> &YPer, 
                int (demogCombo::*f1)() const, int (psCombo::*f2)() const);

  /* helper functions to fill in arrays based on funciton pointers  - on police hsooting only*/
  static void gatherCountStats(visitorCombine* theAggregate, vector<double> &XPer, vector<double> &YPer, 
                int (psCombo::*f1)() const, int (psCombo::*f2)() const);

  /* helper functions to fill in arrays based on funciton pointers  - on demog percentages*/
  static void gatherPerStats(visitorCombine*  theAggregate, vector<double> &XPer, vector<double> &YPer, 
                        double (demogCombo::*f1)() const, double (demogCombo::*f2)() const);

  /* percents and counts on demog */
  static int gatherBothStats(visitorCombine*  theAggregate, vector<double> &XPer, vector<double> &YPer,
                                    vector<double> &XCount, vector<double> &Ycount,
                                    double (demogCombo::*f1)() const, double (demogCombo::*f2)() const,
                                    int (demogCombo::*f3)() const, int (demogCombo::*f4)() const);
  
  /* compute statistics for demographic data for a given region expects, 
  the region and function pointers for the methods to fill in - mix ps and demog */
  static void computeStatsMixRegionData(visitorCombine*  theRegions, 
        int (demogCombo::*f1)() const, int (psCombo::*f2)() const);

  /* compute statistics for demographic data for a given region expects, 
  the region and function pointers for the methods to fill in - two demog fields */
  static void computeStatsDemogRegionData(visitorCombine*  theRegions, 
                                double  (demogCombo::*f1)()const, double(demogCombo::*f2)() const,
                                int (demogCombo::*f3)() const, int (demogCombo::*f4)() const);

  /* compute statistics for demographic data for a given region expects, 
  the region and function pointers for the methods to fill in - two police shooting fields */
  static void computeStatsPSData(visitorCombine*  theRegions, 
                                int (psCombo::*f1)()const, int (psCombo::*f2)() const);

```

See the code in statTool that uses these functors to fill in vectors and then call the appropriate stat functions on the data and print them out.  An example of code that could be used in main.cpp to invoke these functions for a specific data field would be:
```
 //create a visitor to combine the state data
    visitorCombineState theStates;
    statTool::createStateData(pileOfData, theStates);
    theStates.printAllCombo(&demogData::getBelowPovertyCount, &psCombo::getNumberOfCases);

    //create a visitor to combine the county data
    visitorCombineCounty theCounties;
    statTool::createCountyData(pileOfData, theCounties);
    theCounties.printAllCombo(&demogData::getBelowPovertyCount, &psCombo::getNumberOfCases);

    //Do stats work here
    cout << "State data Pop under 5 and BA up: " << endl;
    statTool::computeStatsDemogRegionData(&theStates, &demogData::getpopUnder5, &demogData::getBAup,
        &demogData::getpopUnder5Count, &demogData::getBAupCount);
    cout << "County data Pop under 5 and BA up: " << endl;
    statTool::computeStatsDemogRegionData(&theCounties, &demogData::getpopUnder5, &demogData::getBAup,
        &demogData::getpopUnder5Count, &demogData::getBAupCount);
```

In addition, testStatsData1.cpp as an example of directly filling in data, but in general, using the model shown in main.cpp using statTool will make it easier for you to fill in the worksheet.  Expect additional test cases.

Grading
============
(40) worksheet<br>
(60) autograder (3 tests - youmust provide the complete testStats1.cpp) <br>
(50) working code + code review (using visitor pattern as specified)<br>
