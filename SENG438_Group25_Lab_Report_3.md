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

[3 Test Cases Developed](#test-cases-developed)
* [3.1 Range](#range)
* [3.2 DataUtilities](#datautilities)

[4 Division of Effort and Lessons Learned From Teamwork](#division-of-effort-and-lessons-learned-from-teamwork)

[5 Difficulties Encountered, Challenges Overcome, and Lessons Learned](#difficulties-encountered-challenges-overcome-and-lessons-learned)

[6 Comments and Feedback on The Lab Assignment](#comments-and-feedback-on-the-lab-assignment)

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

### Range.scale

| Variable | Node Defined | DCU | DPU              |
| -------- | ------------ | --- | ---------------- |
| base     | 1            | {6} | {(2, 3), (2, 4)} |
| factor   | 1            | {6} | {(4, 5), (4, 6)} |
| total    |              | 2   | 4                |

<hr>

# 3 Detailed Description of Testing Strategy

## Roles



## Testing Strategy

### Introduction
The following test plan is designed to create new unit tests for the Range class and
DataUtilities class. Specifically, the creation of unit tests will be utilized to increase
the code coverage of Range and DataUtilities. The purpose of this testing is to help interpret how much of the source is tested and to assess the quality of the test suite. New unit tests will be generated by the understanding the requirements (derived from the JavaDocs description of each memthod) for each method and creating tests solely based on requirements that were not covered by the initial test cases created in Assignment 2, by looking at the source code. The plan will identify the methods intended to be tested, test determination procedures and division of work in the team, and the partitions created.

### Test Determination Procedures and Team Work Division
To develop the unit tests that will be used to increase coverage and thoroughly test the Range class and DataUtilities class, the group will employ the use of peer-programming. As such, the group will divide into pairs, where one pair will focus on the development of test cases for the Range class and the other will focus on the development of test cases for the DataUtilities test cases. Prior to splitting into pairs, each member of the group will read through the JavaDocs of the varoius methods of the two classes and discuss what exactly each method should be doing. After splitting into pairs, each pair will take as long as they require to examine the initial test cases created in Assignment #2, to further identify what edge cases, equivalence classes, invalid input tests, and functionalities of the tested methods was covered.

Due to statement, branch, and method coverages being the reported coverage metrics, the group will initially focus on writing unit tests to increase the line coverage of the test suite. Furthermore, IntelliJ provides information regarding what lines are covered, by marking the lines green and read for covered and uncovered respectively. Using this tool unit test will be produced until the line coverage is a minimum of 90%. Increasing the line coverage is focused on first because it reports on the execution footprint of testing which lines of code were executed to complete the tests. Therefore, in writing test cases to improve the line coverage, more lines of code within the methods will be executed and marked green. These lines of code could potentially be branch paths the code can take after a decision statement which would contently increase the branch coverage of the test suite.

After each group achieves a minimum line coverage of 90%, they will check the branch coverage to inspect if the minimum coverage is attained. If the minimum coverage of 70% is not reached at this point further unit tests are created so that each one of the possible branches from each decision point is executed at least once and thereby ensuring that all reachable code is executed. If the minimum coverage is still not reached, additional test cases will be required to validate all the branches in the code making sure that no branch leads to abnormal behavior. Upon obtaining the minimum percentages for line and branch coverage, each will group will check the method coverage to verify if its minimum percentage is achieved. In the case that the minimum percentage for method coverage is not achieved, each group will design unit tests for methods that were not explored by using the red highlights of code provided by IntelliJ. Unit tests for unused methods within the class the group is writing tests for will be generated until a minimum of 60% method coverage is accomplished.

<hr>

# 4 A high level description of five selected test cases you have designed using coverage information, and how they have increased code coverage



<hr>

# 5 A detailed report of the coverage achieved of each class and method (a screen shot from the code cover results in green and red color would suffice)

## DataUtilites

|           | Coverage | Covered | Missed | Total |
| --------- | -------- | ------- | ------ | ----- |
| Statement | 100%     | 80      | 0      | 80    |
| Branches  | 89.6%    | 43      | 5      | 48    |
| Methods   | 100%     | 10      | 0      | 10    |

## Range

|           | Coverage | Covered | Missed | Total |
| --------- | -------- | ------- | ------ | ----- |
| Statement | 92.2%    | 95      | 8      | 103   |
| Branches  | 79.2%    | 57      | 15     | 72    |
| Methods   | 100%     | 23      | 0      | 23    |

<hr>

# 6 Pros and Cons of coverage tools used and Metrics you report

## Pros

- EclEmma is already implemented in Eclipse
- EclEmma can run many coverage types such as Line, Branch,
- EclEmma is an established and respected coverage tool with it being one of the most popular
- Helps identifies parts of the code that are not tested per metric by highlighting lines red and green

## Cons
- EclEmma is outdated and isn't managed actively anymore
<hr>

# 7 A comparison on the advantages and disadvantages of requirements-based test generation and coverage-based test generation.

## Advantages
The advantages of requirements-based test generation ensures that the software code does what its supposed to do. Ensures the testing of the code meets the expectations of outputs and expected results defined in the requirements meaning the correctness of certain functionalities is ensured. Requirements based testing is also a popular strategy and tool in popular software development life cycle patterns such as Agile. Requirements based testing has the advantage of also being well-defined and time-boxed meaning testing can be easier to plan due to clear requirements in the system. 

The advantages of coverage-based test generation is that it ensures 100% coverage of all requirements of the system due to the emphasis on covering all areas of the code. This type of testing also helps to extend the testing of software to areas of code that may have gone untested, thus increasing the quality of the software.

## Disadvantages
The disadvantages of requirements-based testing can be the missing of important parts of software quality. For instance, requirements may be too brief and can cause key parts of the software to go uncaptured and or not specific enough.

A disadvantage of coverage-based test generation is that no apparent strategy in the structure of the testing can lead to time wasted or long periods of time dedicated to testing less important areas of code to ensure 100% coverage. The quality of tests can also be lower since the lack of structure as to the plan when testing can lead to less "effective" tests.

<hr>

# 8 A discussion on how the team work/effort was divided and managed

The team work was done as a group of 4 with all group members participating in the idenifying of methods of the code that needed to be tested to increase coverage. Group members took part in the writing of new test cases to increase branch, line, and method coverage of the tests on the classes DataUtilities and Range. The general formatting of the test cases were thought of as a group along with the splitting of each test into general partitions. The lessons learned from the teamwork in this lab were the importance of having an organized approach to developing test cases to be more efficient as a group. Furthermore, this lab allowed us to utilize peer programming in an efficient way, partnered with simultaneous group programming to complete the coding in the least amount of time possible.

<hr>

# 9 Any difficulties encountered, challenges overcome, and lessons learned from performing the lab

Difficulties encountered in this lab were the clarity in some of the DU-Pair calculations as well as the use of EclEmma and it being the first test code coverage tool any group member had used before. The discovery of the different coverage options such as line, branch, and method took a while to figure out through the use of the tool and help of TA's.  The creation of DU-pairs and data flow graphs required a lot of correcting and backtracking to ensure we had the correct structure. One of the challenges that the group encountered was when implementing the test cases into JUnit methods, only one member could code at a time to avoid conflicts in GitHub. To overcome this, the group decided to use Replit which allowed all members of the group to simultaneously code, increasing productivity significantly. Another challenge that the group encountered was the creation of too many test cases per method, which would lead to duplicate test domains. The way the group overcame the challenge was by going through all of the test cases that were created on paper, and deciding which ones were redundant and thus should be discarded after discussing possible duplicates. Through this assignment, the group learned the specifics of coverage-based testing techniques and applying the terminology associated with it. Furthermore, this assignment served to further familiarize the group members with JUnit testing and good approaches to take when developing tests, such as splitting them up by coverage specific tests such as branch coverage. Branch coverage was exspecially tricky as each if statement or boolean return value had to be covered going every way possible to ensure allb ranches were included to reach the 70% requirement.

<hr>

# 10 Comments/feedback on the lab itself

This lab allowed us to better understand how to create unit tests, perform JUnit testing, and work with coverage-based testing techniques in a collaborative environment. Overall, it taught us how to work effectively as a team and use each other's strengths to achieve a common goal. A suggestion for the future would be to provide a brief explanation of how to use EclEmma at the minimum and the selecting of different coverage type tests for the asked for coverage types.
