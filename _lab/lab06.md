---
layout: lab
num: lab06
ready: false
desc: "Visitor Design Patern - Part 1 and 2"
assigned: 2021-05-13
due: 2021-05-20 23:59
github_org_url: https://github.com/ucsb-cs32-w21
---

Goals
=====

This is a two part lab.  This first half is meant to be a a very simple first pass at looking at the visitor pattern.  The purpose is to practice the pattern and associated techology, while the second half of the lab explores the concepts in more detail with larger code revisions.  Learning objectives. At the end of this lab, students should be able to:

-  Implement the visitor design pattern (part 1) for the exisiting code to support a simple visitors pattern to create a combined report for data
- Use helper functions to compute various statistics for collections (mean, standard dev. and correlation coefficient)(including a basic understanding the use of modern C++ standard algorithms used in the stats tools provided)
- Use helper code to gather data from our exisiting classes into vectors (understand and use function pointer and function objects).
- Understand the basic ideas of these statistics and write test cases to confirm the provided tool works as expected (including understanding when to use population)
- Implement the visitor design pattern (part 2) to combine raw data to state and county level (re-design)
- Use your code to answer questions about the data (specifically focused on computing correlation coefficients for various pairs of data values)

Modality
============
This is a pair lab.  You may choose to work alone or with another student.  When working in a pair, please always follow good pair programming methodologies.  For example, see: https://gds.blog.gov.uk/2018/02/06/how-to-pair-program-effectively-in-6-steps/. In general, set aside time to work togther and share your screen to share the work and learning.  

You will need to identify you partner (pair) in your submission (add a header to your main with both your names!).  The remaining labs will also be optional pair labs and you will be asked to only partner with the same person twice.

Orientation
============
At this point, we have a fairly complex program to read in regional data (demographic and hospital) and aggreagate that data to various levels (county and state).  
For this week, we will introduce minor changes as an introduction to the visitor pattern.  This first pass is intended a very simple addition with minimal changes to our code (and the next lab will explore the concepts in more detail with larger code revisions). 

With OO programming, there are some design patterns that can be used 'to solve recurring design problems to design flexible and reusable object-oriented software, that is, objects that are easier to implement, change, test, and reuse' (https://en.wikipedia.org/wiki/Design_Patterns).  This is a rich topic which is difficult to explore in a short time.  To get a taste for the design patterns we will explore integrating the visitor design pattern into our exisiting code.  This first pass will be very simple (and not take full advantage of this pattern), and we will do further revisions next week.

For this week, the goal is to make minor modifications to use the visitor pattern to print a report combining demographic and hospital data for specified data.  You could accomplish this without the visitor pattern, but our goal is to practice this pattern.

We have considered extremums of the data and sorted the data and to understand the data, we can use some statistical methods to report information about the data.
Specifically, you are provided with code to compute the mean, standard deviation and correlation coefficient for vectors of data.  You are also provided with a tool to gather data from pur aggregated data into vectors for ease of use when computing statistics.  Note that computing the correlation coefficient between two variables can indicate whether there is a relationship between those data variables.
For a basic explanation see: https://www.statisticshowto.com/probability-and-statistics/correlation-coefficient-formula/

You are provided with implementations of these statistical tools that use modern standard algorithms (accumulate, inner_product, for_each and llambdas).  You should be able to read the provided code and understand how to identify the iterators and llambdas and basic functionality.  You will be asked to fill in an associated worksheet to demonstrate this knowledge. You will also be asked to write test cases to make sure these tools are behaving as expected.

In addition to this new statistical tool (stats.h/cpp), the heart of this lab is to extend our basic understanding of the visitor pattern to re-design our code to create two new visitors that allow us to combine the raw data into either state level regions or county level regions that can then be compared using the statistical tool.  This redesign will completely remove dataAQ and encapsulate the computation needed to aggregate data for the different types.  The primary task of this lab is to re-design our code and use the visitor pattern to separate the algorithm to aggregate regional data into concrete visitor algorithms.

Once you have completed the re-design, you can use the additional new tools (statTool.h/cpp and statGatherer.h) to gather vectors of the data (at various regional levels) and compare the correlation coefficient of various data pairings.  You will need to use these tools to fill out a works sheet with specific information.

Steps
============
Introduce and modify the following classes as follows to support printing a combined report, using the visitors pattern.
1) Create a visitor class to be used as an interface.  This should only define pure virtual methods to visit the two types: hospitalData and demogData
2) Modify placeData to also include a pure virtual function (so that derived classes can accept a visitor):
```
    //Lab05 anything that is place data must accept a visitor (aka must be visitable)
    virtual void accept(class Visitor &v) = 0;
```
3) Implement the accept method for hospitalData and demogData.  It should just call visit on the visitor for the given type.
4) Define a visitorReport class that implements the visit method for each of the two types.  For this week's lab, the visit method just prints a subset of each type's data (match example data)
5) Modify dataAQ.h to add a method to print a report of the data for any state that meets a given criteria.  You must implement this by creating a visitorReport and calling accept with this visitor on a collection of demogData and hospitalData that meets the given criteria. (You may create the selection first then call accept on all values in the collection.  The first report to create is for state data for any state with a percentage of the population below the poverty line above a threshold (stay tuned for additional reports):
```
void dataAQ::stateReport(double thresh);
```
There are new files (including the stats functions and example test cases) that can be found here: https://github.com/ucsb-cs32-w21/Lab06-STARTER
Start by adding your files from lab05 to a new lab06 directory and add these new files as well and try to compile.  Resolve any compilation issues and complete this first task before moving on. Note for the statTool and statGatherer you may need to wait until you're redesign is complete.

One of your first tasks is to make sure you understand and validate the new statistical functions provided to you in stats.h/cpp.  Looking at the base code, read through the code and answer the questions at: Lab06-worksheet (see gauchospace).  

In addition, when given a new tool or set of code, it is always good to make sure you understand the tool and validate the tool is behaving as expected.  
In particular, since our data represents population information represented as both counts and percentages, we need to make sure we use the right data with each of the tools.  In general, for the mean, you need to use the demographic counts (and pass in the total population) for the various regions.  *The mean for any given demographic data should be the same at both a county and state level.*

As a first test that stats.h/cpp is working as expected, edit testStats1.cpp and uncomment the final asserts.  You will need to find an online statistical calculator or use an external method to  compute what the correct values should be and then test the tool to make sure it is working as expected. *Additional tests will be added to test your understanding of the percent vs count.


Tasks - step two *Redesign *
============

The heart of this lab is to redesign the way we create aggregate data.  
First, we will take advantage of the shared type 'placeData' and create one large shared vector of raw data:
```
    std::vector<shared_ptr<placeData>> pileOfData;
```

Re-write read_csv in parse.cpp to take in a reference to a vector of place data, so that you can add onto the one vector of data:
```
   //read in the hospital data
    read_csv(pileOfData, "hospitals.csv", HOSPITAL);
   
    //read in the demographic data
    read_csv(pileOfData, "county_demographics.csv", DEMOG); 
```

Now that we have one big pile of data, we will use the visitor design pattern to create two new visitors that we can use on the big pile of data to 
do the correct aggregation computation for the two different types of data (hospital and demog).  For example, once you are done, the code in testStatsData1.cpp should be able to work, which just loops through the pile of data and calls accept with the two different visitor types:
```
  //create a visitor to combine the state data
  visitorCombineState theStates;
  //use visitor pattern to be able to aggregate
  for (const auto &obj : pileOfData) {
        obj->accept((visitorCombineState&)theStates);
  }
  visitorCombineCounty theCounties("simple_uscities.csv");
  //use visitor pattern to be able to aggregate
  for (const auto &obj : pileOfData) {
        obj->accept((visitorCombineCounty&)theCounties);
  }
```
You will need to implement these two new classes
```
class visitorCombineCounty : public Visitor
class visitorCombineState : public Visitor 
```
As their name suggests these visitors will combine data into either state level data or county level data.  Your job is to write these classes and their associated methods.  
You will want to move the hashmaps that represent the aggregate data into these visitors, but not make the data public. So for example, for the visitorCombineState, it should include:
```
    private:
    	//state maps
        std::map<string, comboDemogData*> allStateDemogData;
        std::map<string, comboHospitalData*> allStateHospData;
```
Along with getter methods returning the appropriate types needed to access this data named:
```
stateDmap()
stateDmapEntry(string stateN) 
stateHmap() const
stateHmapEntry(string stateN) 
````
Note that for county data, we need to be able to create vectors of data for matching counties, so think about what you will need to do for demogData, to organize the counties in a way that you can pair the data with the associated aggregate hospital data.  For county data, you will also need to use the city->county map. Thus the complete data for visitorCombineCounty would include:
```
    private:
        //map for county hospital data
        std::map<string, comboHospitalData*> allCountyHData;
        //map for county name to demog data
        std::map<string, comboDemogData*> allCountyDData;

        //helper map to create aggregates from city -> county
        std::map<string, string> cityToCounty;
```
This visitor can and should include any method to read in the city -> county map and getters for the county data similar to the visitorCombineState (again with appropriate return types specified:
```
countyDmap() 
countyDmapEntry(string countyN)
countyHmap() 
countyHmapEntry(string countyN)
```

Tasks - step three compute statistics using the aggregate data
============
Once we have the aggregate data at the county and state level, we want to make vectors of specific data members to compute interesting statistics.  

To help with this task, you can use statTool.h/cpp and statGatherer.h. 
statGather.h defines functors that operate at either the county or the state level.  The included methods can be used to fill in vectors with data using function pointers.
These methods, in turn call the appropriate
stats method depending on if the data is only dmeographic (population) or if it is mixed demographic and hospital (sample).

```
/*
helper parent functor to simplify stats gathering - the role of this functor is to gather data
into two arrays.
Takes in:
 -a regional level (county or state) visitor
 -vectors to fill in
 -varying number of function pointers for the class methods to use to fill in data
 */
class statGatherer {
  public:
    //function to gather mixed data (demographic and hospital)
    virtual void gatherPerStats(Visitor* Regions, vector<double> &XPer, vector<double> &YPer, 
                double (demogData::*f1)() const, double (comboHospitalData::*f2)() const) = 0;
    //function to gather two demog datas
    virtual void gatherPerStats(Visitor* Regions, vector<double> &XPer, vector<double> &YPer, 
                double (demogData::*f1)() const, double (demogData::*f2)() const) = 0;
    //function to gather two demog datas (percentages and counts - for accuracy with populations)
    virtual int gatherBothStats(Visitor* Regions, vector<double> &XPer, vector<double> &YPer,
                                    vector<double> &XCount, vector<double> &Ycount,
                                    double (demogData::*f1)() const, double (demogData::*f2)() const,
                                    int (demogData::*f3)() const, int (demogData::*f4)() const) = 0;
};

```

See the code in statTool that uses these functors to fill in vectors and then call the appropriate stat functions on the data and print them out.  The example, main.cpp has two example calls (showing the instantiation of the functor and passing function pointers to class member getter functions).  You can use this example 
to EXTEND main.cpp in orer to fill in the required work sheet for this lab.

In addition, testStatsData1.cpp as an example of directly filling in data, but in general, using the model shown in main.cpp using statTool and statGatherer will make it easier for you to fill in the worksheet.  Expect additional test cases.

Grading
============
(20) worksheet<br>
(30) autograder (3 tests - youmust provide the complete testStats1.cpp) <br>
(50) working code + code review (using visitor pattern as specified)<br>
