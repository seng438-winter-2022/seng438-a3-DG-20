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

Text…

<hr>

# Data-Flow Coverage Calculations for DataUtilities.calculateColumnTotal and Range.scale

## Methods of Which Coverage Will Be Calculated
1. DataUtilities.calculateColumnTotal(Values2D data, int column)
2. Range.scale(Range base, double factor)

## Data Flow Graphs

### DataUtilities.calculateColumnTotal

![DataUtilities](https://user-images.githubusercontent.com/58268240/156028338-542d9018-4a2e-47b0-925a-b491df863053.png?style=centerme)

### Range.scale

![Range](https://user-images.githubusercontent.com/58268240/156028404-079b91f8-7901-4baf-80ac-9bb45bf5fa24.png?style=centerme)

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




<hr>


# 3 A detailed description of the testing strategy for the new unit test

Text…

# 4 A high level description of five selected test cases you have designed using coverage information, and how they have increased code coverage

Text…

# 5 A detailed report of the coverage achieved of each class and method (a screen shot from the code cover results in green and red color would suffice)

Text…

# 6 Pros and Cons of coverage tools used and Metrics you report

Text…

# 7 A comparison on the advantages and disadvantages of requirements-based test generation and coverage-based test generation.

Text…

# 8 A discussion on how the team work/effort was divided and managed

Text…

# 9 Any difficulties encountered, challenges overcome, and lessons learned from performing the lab

Text…

# 10 Comments/feedback on the lab itself

Text…
