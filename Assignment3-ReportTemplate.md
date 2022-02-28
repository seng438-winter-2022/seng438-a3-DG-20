**SENG 438 - Software Testing, Reliability, and Quality**

**Lab. Report #3 – Code Coverage, Adequacy Criteria and Test Case Correlation**

| Group \#:      | 25    |
| -------------- | --- |
| Curtis Silva |     |
| Divyansh Goyal               |     |
| Gurpartap Sohi               |     |
| Liam Parmar               |     |

(Note that some labs require individual reports while others require one report
for each group. Please see each lab document for details.)

# 1 Introduction

Text…

# 2 Manual data-flow coverage calculations for X and Y methods

## 2.1 Methods of Which Coverage Will Be Calculated
1. DataUtilities.calculateColumnTotal(Values2D data, int column)
2. Range.scale(Range base, double factor)

## 2.2 Data Flow Graphs

### DataUtilities.calculateColumnTotal

![DataUtilities](https://user-images.githubusercontent.com/58268240/156028338-542d9018-4a2e-47b0-925a-b491df863053.png?style=centerme)

### Range.scale

![Range](https://user-images.githubusercontent.com/58268240/156028404-079b91f8-7901-4baf-80ac-9bb45bf5fa24.png?style=centerme)

## 2.3 Def-Use Sets Per Statement

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

## 2.4 Def-Use Pairs Per Variable

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

## 2.5 Test Case Def-Use Pair Coverage Analysis





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
