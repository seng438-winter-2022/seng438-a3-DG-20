**SENG 438 - Software Testing, Reliability, and Quality**

**Lab. Report #3 – Code Coverage, Adequacy Criteria and Test Case Correlation**

| Group \#:      | 25    |
| -------------- | --- |
| Curtis Silva |     |
| Divyansh Goyal               |     |
| Gurpartap Sohi               |     |
| Liam Parmar               |     |

<hr>

**Table of Contents**

[1 Introduction](#introduction)

[2 Data-Flow Coverage Calculations for DataUtilities.calculateColumnTotal and Range.scale](#data-flow-coverage-calculations-for-datautilitiescalculatecolumntotal-and-rangescale)
* [2.1 Methods of Which Coverage Will Be Calculated](#methods-of-which-coverage-will-be-calculated)
* [2.2 Data Flow Graphs](#data-flow-graphs)
* [2.3 Def-Use Sets Per Statement](#def-use-sets-per-statement)
* [2.4 Def-Use Pairs Per Variable](#def-use-pairs-per-variable)
* [2.5 Test Case Def-Use Pair Coverage Analysis](#test-case-def-use-pair-coverage-analysis)
* [2.6 Def-Use Pair Coverage Calculation](#def-use-pair-coverage-calculation)

[3 Detailed Description of Testing Strategy](#detailed-description-of-testing-strategy)
* [3.1 Testing Strategy](#testing-strategy)

[4 High Level Description of Five Selected Test Cases and Their Contribution to Coverage](#high-level-description-of-five-selected-test-cases-and-their-contribution-to-coverage)

[5 New Coverage Achieved with Further Test Cases Added](#new-coverage-achieved-with-further-test-cases-added)
* [5.1 DataUtilites](#datautilites)
* [5.2 Range](#range)

[6 Pros and Cons of EclEmma](#pros-and-cons-of-eclEmma)
* [6.1 Pros](#pros)
* [6.2 Cons](#cons)

[7 Advantages and Disadvantages of Requirements-Based Test Generation and Coverage-Based Test Generation](#advantages-and-disadvantages-of-requirements-based-test-generation-and-coverage-based-test-generation)

[8 How Work was Divided/Shared](#how-work-was-dividedshared)

[9 Difficulties Encountered, Challenges Overcame, and Lessons Learned](#difficulties-encountered-challenges-overcame-and-lessons-learned)

[10 Comments/Feedback](#commentsfeedback)

<hr>

# Introduction



<hr>

# Data-Flow Coverage Calculations for DataUtilities.calculateColumnTotal and Range.scale

## Methods of Which Coverage Will Be Calculated
1. DataUtilities.calculateColumnTotal(Values2D data, int column)
2. Range.scale(Range base, double factor)

## Data Flow Graphs

### DataUtilities.calculateColumnTotal

![Untitled Diagram](https://user-images.githubusercontent.com/58268240/156315675-64417059-c2d7-42a5-9cdd-eabc2b5be21c.png?style=centerme)

### Range.scale

![Untitled Diagram (1)](https://user-images.githubusercontent.com/58268240/156315949-8e2b2654-8f61-4598-91c8-efe98e44487d.png?style=centerme)


## Def-Use Sets Per Statement

### DataUtilities.calculateColumnTotal

```
1. public static double calculateColumnTotal(Values2D data, int column) {
2. ParamChecks.nullNotPermitted(data, "data");
3. double total = 0.0;
4. int rowCount = data.getRowCount();
5. for (int r = 0; r < rowCount; r++) {
6. Number n = data.getValue(r, column);
7. if (n != null) {
8. total += n.doubleValue();}}
9. return total;}
```

1. Def = {data, column}, Use = {∅}
2. Def = {∅}, Use = {data}
3. Def = {total}, Use = {∅}
4. Def = {rowcount}, Use = {data}
5. Def = {r}, Use = {rowcount,r}
6. Def = {n}, Use = {r,column}
7. Def = {∅}, Use = {n}
8. Def = {total}, Use = {n}
9. Def = {∅}, Use = {total}

### Range.scale

```
1. public static Range scale(Range base, double factor) {
2. ParamChecks.nullNotPermitted(base, "base");
3. if (factor < 0) {
4. throw new IllegalArgumentException("Negative 'factor' argument.");}
5. return new Range(base.getLowerBound() * factor, base.getUpperBound() * factor);}
```

1. Def = {base, factor}, Use = {∅}
2. Def = {∅}, Use = {base}
3. Def = {∅}, Use = {factor}
4. Def = {∅}, Use = {∅}
5. Def = {∅}, Use = {factor,base}

## Def-Use Pairs Per Variable

(Using the DFGs from above)

### DataUtilities.calculateColumnTotal

- data: Def = {1}, Use = {2, 5, 8}
- total: Def = {4,10}, Use = {10,12}
- rowcount: Def = {5}, Use = {7}
- r: Def = {6,11}, Use = {7,8,11}
- n: Def = {8}, Use = {9,10}
- column: Def = {1}, Use = {8}

### Range.scale

- base: Def = {1}, Use = {2,6}
- factor: Def = {1}, Use = {4,6}

## Test Case Def-Use Pair Coverage Analysis

### DataUtilities.calculateColumnTotal

Test Case Method: calculateColumnTotalForNullDataTest
Def-Use Pairs Covered: (1, 2).
- data: Def = {1}, Use = {2}
- total: Def = {∅}, Use = {∅}
- rowcount: Def = {∅}, Use = {∅}
- r: Def = {∅}, Use = {∅}
- n: Def = {∅}, Use = {∅}
- column: Def = {1}, Use = {∅}

Test Case Method: calculateColumnTotalValidDataRealTest
Def-Use Pairs Covered: (1, 2), (1, 5), (1, 8), (4, 10), (10, 10), (10, 12), (5, 7), (6, 7), (6, 8), (6, 11), (11, 7), (11, 8), (11, 11), (8, 9), (8, 10), (1, 8).
- data: Def = {1}, Use = {2, 5, 8}
- total: Def = {4,10}, Use = {10,12}
- rowcount: Def = {5}, Use = {7}
- r: Def = {6,11}, Use = {7,8,11}
- n: Def = {8}, Use = {9,10}
- column: Def = {1}, Use = {8}

Test Case Method: calculateColumnTotalValidDataExtraTest
Def-Use Pairs Covered: (1, 2), (1, 5), (1, 8), (4, 10), (10, 10), (10, 12), (5, 7), (6, 7), (6, 8), (6, 11), (11, 7), (11, 8), (11, 11), (8, 9), (8, 10), (1, 8).
- data: Def = {1}, Use = {2, 5, 8}
- total: Def = {4,10}, Use = {10,12}
- rowcount: Def = {5}, Use = {7}
- r: Def = {6,11}, Use = {7,8,11}
- n: Def = {8}, Use = {9,10}
- column: Def = {1}, Use = {8}

Test Case Method: calculateColumnTotalUnderAcceptableColTest
Def-Use Pairs Covered: (1, 2), (1, 5), (5, 7), (6, 7).
- data: Def = {1}, Use = {2, 5}
- total: Def = {4}, Use = {∅}
- rowcount: Def = {5}, Use = {7}
- r: Def = {6}, Use = {7}
- n: Def = {∅}, Use = {∅}
- column: Def = {1}, Use = {∅}

Test Case Method: calculateColumnTotalOverAcceptableColTest
Def-Use Pairs Covered: (1, 2), (1, 5), (5, 7), (6, 7).
- data: Def = {1}, Use = {2, 5}
- total: Def = {4}, Use = {∅}
- rowcount: Def = {5}, Use = {7}
- r: Def = {6}, Use = {7}
- n: Def = {∅}, Use = {∅}
- column: Def = {1}, Use = {∅}

Test Case Method: calculateColumnTotalBoundaryTest
Def-Use Pairs Covered: (1, 2), (1, 5), (1, 8), (4, 10), (10, 10), (10, 12), (5, 7), (6, 7), (6, 8), (6, 11), (11, 7), (11, 8), (11, 11), (8, 9), (8, 10), (1, 8).
- data: Def = {1}, Use = {2, 5, 8}
- total: Def = {4,10}, Use = {10,12}
- rowcount: Def = {5}, Use = {7}
- r: Def = {6,11}, Use = {7,8,11}
- n: Def = {8}, Use = {9,10}
- column: Def = {1}, Use = {8}

### Range.scale

Test Case Method: scaleNullRangeNegativeFactorTest
Def-Use Pairs Covered: (1, 2).
- base: Def = {1}, Use = {2}
- factor: Def = {1}, Use = {∅}

Test Case Method: scaleValidRangeNegativeFactorTest
Def-Use Pairs Covered: (1, 2), (1, 4).
- base: Def = {1}, Use = {2}
- factor: Def = {1}, Use = {4}

Test Case Method: scaleNullRangeValidFactorTest
Def-Use Pairs Covered: (1, 2).
- base: Def = {1}, Use = {2}
- factor: Def = {1}, Use = {∅}

Test Case Method: scaleValidRangeValidFactorTest
Def-Use Pairs Covered: (1, 2), (1, 5), (1, 4), (1, 6).
- base: Def = {1}, Use = {2,5}
- factor: Def = {1}, Use = {4,6}

Test Case Method: scaleFactorZeroTest
Def-Use Pairs Covered: (1, 2), (1, 5), (1, 4), (1, 6).
- base: Def = {1}, Use = {2,5}
- factor: Def = {1}, Use = {4,6}

## Def-Use Pair Coverage Calculation

### DataUtilities.calculateColumnTotal

The test cases called calculateColumnTotalValidDataRealTest, calculateColumnTotalValidDataExtraTest, calculateColumnTotalBoundaryTest utilize all 16 possible def-use pairs (listed above) within the function. As such, the Def-Use Pair Coverage is 100% for the developed test cases.

### Range.scale

The test cases called scaleValidRangeValidFactorTest and scaleFactorZeroTest utilize all four possible def-use pairs (listed above) within the function. As such, the Def-Use Pair Coverage is 100% for the developed test cases.

### DCU and DPU Tables

#### DataUtilities.calculateColumnTotal

| Variable | Node Defined | DCU      | DPU                |
| -------- | ------------ | -------- | ------------------ |
| data     | 1            | {5, 8}   | {(2, 3), (2, 4)}   |
| column   | 1            | {8}      | { }                |
| total    | 4            | {10, 12} | { }                |
| total    | 10           | {10, 12} | { }                |
| rowCount | 5            | { }      | {(7, 8), (7, 12)}  |
| r        | 6            | {8, 11}  | {(7, 8), (7, 12)}  |
| r        | 11           | {8, 11}  | {(7, 8), (7, 12)}  |
| n        | 8            | {10}     | {(9, 10), (9, 11)} |
| total    |              | 12       | 10                 |

#### Range.scale

| Variable | Node Defined | DCU | DPU              |
| -------- | ------------ | --- | ---------------- |
| base     | 1            | {6} | {(2, 3), (2, 4)} |
| factor   | 1            | {6} | {(4, 5), (4, 6)} |
| total    |              | 2   | 4                |

<hr>

# Detailed Description of Testing Strategy

## Testing Strategy

### Introduction
The following test plan is designed to create new unit tests for the Range class and
DataUtilities class. Specifically, the creation of unit tests will be utilized to increase
the code coverage of Range and DataUtilities. The purpose of this testing is to help interpret how much of the source is tested and to assess the quality of the test suite. New unit tests will be generated by the understanding the requirements (derived from the JavaDocs description of each memthod) for each method and creating tests solely based on requirements that were not covered by the initial test cases created in Assignment 2, by looking at the source code. The plan will identify the methods intended to be tested, test determination procedures and division of work in the team, and the partitions created.

### Test Determination Procedures and Team Work Division
To develop the unit tests that will be used to increase coverage and thoroughly test the Range class and DataUtilities class, the group will employ the use of peer-programming. As such, the group will divide into pairs, where one pair will focus on the development of test cases for the Range class and the other will focus on the development of test cases for the DataUtilities test cases. Prior to splitting into pairs, each member of the group will read through the JavaDocs of the various methods of the two classes and discuss what exactly each method should be doing. After splitting into pairs, each pair will take as long as they require to examine the initial test cases created in Assignment #2, to further identify what edge cases, equivalence classes, invalid input tests, and functionalities of the tested methods were already covered.

Due to statement, branch, and method coverages being the reported coverage metrics, the group will initially focus on writing unit tests to increase the statement coverage of the test suite for the class that they are responsible for. Furthermore, Eclipse provides information regarding what lines are covered, by marking the lines green and red for covered and uncovered respectively. Using this coverage tool, unit tests will be produced until the statement coverage is a minimum of 90%. Increasing the statement coverage is focused on first because it reports on the execution footprint of testing which lines of code were executed to complete the tests. Therefore, in writing test cases to improve the line coverage, more lines of code within the methods will be executed and marked green. This would also lead to an increase of the method coverage in the class. These lines of code could potentially be branch paths the code can take after a decision statement which would also increase the branch coverage of the test suite.

After each group achieves a minimum statement coverage of 90%, they will check the branch coverage to inspect if the minimum coverage is attained. If the minimum coverage of 70% is not reached at this point further unit tests are created so that the coverage requirement is satisfied. Upon obtaining the minimum percentages for statement and branch coverage, each group will check the method coverage to verify if its minimum percentage is achieved. In the case that the minimum percentage for method coverage is not achieved, each group will design unit tests for methods that were not explored by using the red highlights of code provided by Eclipse's EclEmma coverage tool. Unit tests for unused methods within the class the group is writing tests for will be generated until a minimum of 60% method coverage is accomplished.

Finally, after each pair has completed developing test cases for their assigned class, the group came together as a whole and evaluated each test case individually and removed redundant or invalid test cases.

<hr>

# High Level Description of Five Selected Test Cases and Their Contribution to Coverage



<hr>

# New Coverage Achieved with Further Test Cases Added

## DataUtilites

|           | Coverage | Covered | Missed | Total |
| --------- | -------- | ------- | ------ | ----- |
| Statement | 100%     | 80      | 0      | 80    |
| Branches  | 89.6%    | 43      | 5      | 48    |
| Methods   | 100%     | 10      | 0      | 10    |

### Statement Coverage Screenshot:
![image](https://user-images.githubusercontent.com/58268240/156859874-00c97e97-4680-470c-a49d-3955c71f696e.png?style=centerme)


### Branch Coverage Screenshot: 
![image](https://user-images.githubusercontent.com/58268240/156859856-40d5cc93-10ff-4628-92cd-c29662903ed2.png?style=centerme)


### Method Coverage Screenshot:
![image](https://user-images.githubusercontent.com/58268240/156859834-7af6c09f-feb2-467c-9ac3-50e40a0aac37.png?style=centerme)

## Range

|           | Coverage | Covered | Missed | Total |
| --------- | -------- | ------- | ------ | ----- |
| Statement | 92.2%    | 95      | 8      | 103   |
| Branches  | 79.2%    | 57      | 15     | 72    |
| Methods   | 100%     | 23      | 0      | 23    |

### Statement Coverage Screenshot:
![image](https://user-images.githubusercontent.com/58268240/156859781-3cae90c7-64ac-4aaf-9442-a974110bea29.png)


### Branch Coverage Screenshot: 
![image](https://user-images.githubusercontent.com/58268240/156859763-35612d6f-a985-4cd8-854a-f66ba2617333.png)


### Method Coverage Screenshot:
![image](https://user-images.githubusercontent.com/58268240/156859802-ce2cb12e-76e4-4a48-a1f8-04a6fd8cf376.png)

<hr>

# Pros and Cons of EclEmma

## Pros

- EclEmma is already implemented in Eclipse.
- EclEmma can run many coverage types such as Line, Branch, and Method.
- EclEmma is an established and respected coverage tool with it being one of the most popular ones.
- Helps identifies parts of the code that are not tested per metric by highlighting lines red and green.
- Provides feedback regarding how many branches are covered and missed for each decision.
- EclEmma provides specific statistics regarding number of covered and missed metrics, rather than just a coverage percentage.

## Cons
- EclEmma is outdated and isn't managed actively anymore.
- It does not identify which particular branch path has been covered and which has not been covered.
- It does not support condition coverage, and thus the group was required to report on method coverage instead.

<hr>

# Advantages and Disadvantages of Requirements-Based Test Generation and Coverage-Based Test Generation

## Advantages

The advantages of requirements-based test generation ensures that the software code does what its supposed to do. Ensures the testing of the code meets the expectations of outputs and expected results defined in the requirements meaning the correctness of certain functionalities is ensured. Requirements based testing is also a popular strategy and tool in popular software development life cycle patterns such as Agile. Requirements based testing has the advantage of also being well-defined and time-boxed meaning testing can be easier to plan due to clear requirements in the system. Another benefit of requirements-based test generation is that the tester does not need to spend time analyzing the source code and thus does not need to be entirely familiar with the system beforehand.

The advantages of coverage-based test generation is that it ensures 100% coverage of all requirements of the system due to the emphasis on covering all areas of the code. This type of testing also helps to extend the testing of software to areas of code that may have gone untested, thus increasing the quality of the software. Furthermore, this type of test generation focuses on the code itself, which leads to the discovery of more bugs if the tester is technically inclined and has a good grasp of the system under test (SUT).

## Disadvantages

The disadvantages of requirements-based testing can be the missing of important parts of software quality. For instance, requirements may be too brief and can cause key parts of the software to go uncaptured and/or not specific enough. Another disadvantage of requirement-based test generation is that it is strongly reliant on the descriptions of the functions and methods, and as such, if the requirements are unclear, the tester can create incorrect tests, which may lead to inefficiencies. Since the tester does not view the source code, they have no way of ensuring that they have covered every branch and possibilities, which could lead to them missing the discovery of certain bugs.

A disadvantage of coverage-based test generation is that a lack of apparent requirements of the system under test can lead to time wasted or long periods of time dedicated to testing less important areas of code to ensure 100% coverage. The quality of tests can also be lower since the lack of structure as to the plan when testing can lead to less "effective" tests. This type of test generation requires the tester to first spend time analyzing the source code and determining which branches, methods, and statements exist, and then determine test cases to cover them all. This could take much longer than simply testing the important requirements of the SUT.

<hr>

# How Work was Divided/Shared

The team work was done in pairs with all group members participating in the identifying of methods of the code that needed to be tested to increase coverage. Group members took part in the writing of new test cases to increase branch, statement, and method coverage of the tests on the classes DataUtilities and Range in pairs. Within each pair, one individual was responsible for identifying the missing coverage reasons, whereas the other used that knowledge to write test cases and run the EclEmma coverage tool to verify that the minimum coverage requirements were met. After this was finished, the group came together and checked over the other pair's developed test cases. The lessons learned from the teamwork in this lab were the importance of having an organized approach to developing test cases to be more efficient as a group. Furthermore, this lab allowed us to utilize peer programming in an efficient way, partnered with simultaneous group programming to complete the coding in the least amount of time possible.

<hr>

# Difficulties Encountered, Challenges Overcame, and Lessons Learned

Difficulties encountered in this lab were the clarity in some of the DU-Pair calculations as well as the use of EclEmma and it being the first test code coverage tool any group member had used before. The discovery of the different coverage options such as line, branch, and method took a while to figure out through the use of the tool and help of TA's.  The creation of DU-pairs and data flow graphs required a lot of correcting and backtracking to ensure we had the correct structure. One of the challenges that the group encountered was when implementing the test cases into JUnit methods, only one member could code at a time to avoid conflicts in GitHub. To overcome this, the group decided to use Replit which allowed all members of the group to simultaneously code, increasing productivity significantly. Another challenge that the group encountered was the creation of too many test cases per method, which would lead to duplicate test domains. The way the group overcame the challenge was by going through all of the test cases that were created on paper, and deciding which ones were redundant and thus should be discarded after discussing possible duplicates. Through this assignment, the group learned the specifics of coverage-based testing techniques and applying the terminology associated with it. Furthermore, this assignment served to further familiarize the group members with JUnit testing and good approaches to take when developing tests, such as splitting them up by coverage specific tests such as branch coverage. Branch coverage was exspecially tricky as each if statement or boolean return value had to be covered going every way possible to ensure allb ranches were included to reach the 70% requirement.

<hr>

# Comments/Feedback

This lab allowed us to better understand how to create unit tests, perform JUnit testing, and work with coverage-based testing techniques in a collaborative environment. Overall, it taught us how to work effectively as a team and use each other's strengths to achieve a common goal. A suggestion for the future would be to provide a brief explanation of how to use EclEmma at the minimum and the selecting of different coverage type tests for the asked for coverage types.
