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
   public static double calculateColumnTotal(Values2D data, int column) {
1. ParamChecks.nullNotPermitted(data, "data");
2. double total = 0.0;
3. int rowCount = data.getRowCount();
4. for (int r = 0; r < rowCount; r++) {
5. Number n = data.getValue(r, column);
6. if (n != null) {
7. total += n.doubleValue();}}
8. return total;}
```

1. Def = {∅}, Use = {data}
2. Def = {total}, Use = {∅}
3. Def = {rowcount}, Use = {data}
4. Def = {r}, Use = {rowcount,r}
5. Def = {n}, Use = {r,column}
6. Def = {∅}, Use = {n}
7. Def = {total}, Use = {n}
8. Def = {∅}, Use = {total}

### Range.scale

```
   public static Range scale(Range base, double factor) {
1. ParamChecks.nullNotPermitted(base, "base");
2. if (factor < 0) {
3. throw new IllegalArgumentException("Negative 'factor' argument.");}
4. return new Range(base.getLowerBound() * factor, base.getUpperBound() * factor);}
```

1. Def = {∅}, Use = {base}
2. Def = {∅}, Use = {factor}
3. Def = {∅}, Use = {∅}
4. Def = {∅}, Use = {factor,base}

## Def-Use Pairs Per Variable

(Using the DFGs from above)

### DataUtilities.calculateColumnTotal

data: Def = {∅}, Use = {1, 4, 7}
total: Def = {3,9}, Use = {9,11}
rowcount: Def = {4}, Use = {6}
r: Def = {5,10}, Use = {6,7,10}
n: Def = {7}, Use = {8,9}
column: Def = {∅}, Use = {7}

### Range.scale

base: Def = {∅}, Use = {1,5}
factor: Def = {∅}, Use = {3,5}

## Test Case Def-Use Pair Coverage Analysis

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
