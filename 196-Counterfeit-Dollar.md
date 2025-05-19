# [Simple Fun #196: Counterfeit Dollar](https://www.codewars.com/kata/58c61a1e8a452631c5000003)

## Strategy
- Determine whether a coin is `normal`, `light`, or `heavy` based on the clue provided by the weighting results
- If we can identify exactly one coin as either `light` or `heavy` and all the others as `normal`, then we can determine the answer.

### Scenario
Among coins A, B, C, D, E, F, the weighting results are `["AB EF up", "AB CD even", "AE BF down"]`

Note: To simplify the illustration, we use 6 coins and comparing 2 groups of 2 coins in each test.

### Overview of the Approach

```
Initial states                        Final states
A: { light, normal,  }                          A: { normal }
B: uncertain  --------------------->  B: { normal }
C: uncertain      Update states       C: { normal }
D: uncertain      in each step        D: { normal }
E: uncertain                          E: { light }
F: uncertain                          F: { normal }
```
- Initially, we do not know if a coin is `light`, `normal`, or `heavy` (so I denote such state as `uncertain`): 
- In each step, we update the states based on the clue given in the weighting result.
- At the end, find the answer from the final states of the coins.
  - In this example, we can determine "E is the counterfeit coin and it is light".

## The Approach

Initially, the coin states are
```
A: uncertain
B: uncertain
C: uncertain
D: uncertain
E: uncertain
F: uncertain
```

### 1st Result: `"AB EF up"`
The outcome is "up".

#### Implication #1 
**The coins that are NOT on the scale are normal.**
  - C and D are normal. 

After updating the coin states, we now have
```
A: uncertain
B: uncertain
C: normal
D: normal
E: uncertain
F: uncertain
```

#### Implication #2
Each coin on the left is either `heavy` or `normal`.
A and B are either `heavy
If a coin

Because `"AB"` cannot be `light`, we can eliminate `light` from A and B.

Each coin on the right is either `light` or `normal` (it cannot be `heavy`).
Because `"EF"` cannot be `heavy`, we can eliminate `heavy` from E and F.

After updating the coin states, we have
```
A: { normal, heavy }  <-- 'light' removed
B: { normal, heavy }  <-- 'light' removed
C: { normal }
D: { normal } 
E: { light, normal }  <-- 'heavy' removed 
F: { light, normal }  <-- 'heavy' removed
```

### 2nd Result `"AB CD even"`
**The outcome is "even" implies the coins on the scale are normal.**

A, B, C, D are normal.

After updating the coin states, we have
```
A: { normal }         <-- 
B: { normal } 
C: { normal }
D: { normal } 
E: { light, normal }
F: { light, normal }
```

### 3rd Result `AE BF down`
"down" is just opposite of "up".

#### Implication #1 
**The coins that are NOT on the scale are normal.**
  - C and D are normal. 

We have already recorded C and D as normal previously, so the coin states remains unchanged
```
A: { normal }
B: { normal } 
C: { normal }
D: { normal } 
E: { light, normal }
F: { light, normal }
```

#### Implication #2
**Each coin on the right (`"BF"`) cannot be `light`**, so we can eliminate `light` from B and F.

**Each coin on the left (`"AE"`) cannot be `heavy`**, so we can eliminate `heavy` from A and E.

After updating the coin states, we have
```
A: { normal }          <-- No 'light' need to be removed
B: { normal }          <-- No 'light` need to be removed
C: { normal }
D: { normal } 
E: { light, normal }   <-- No 'heavy' need to be remove
F: { normal }          <- 'light' removed
```

### 2nd Result: `"ABCD EFKL up"`

The outcome is "up".

#### Implication #1 
One of the coins on the scale is a counterfeit. So the **coins that are NOT on the scale are normal**. 

That means, `"GHIJ"` are normal and we can update the coin table accordingly:

```
A: { normal }
B: { normal }
C: { normal }
D: { normal }
E: { normal }
F: { normal }
G: { normal }
H: { normal }
I: { normal }
J: { normal }
K: { light, normal, heavy }
L: { light, normal, heavy }
```

#### Implication #2
Each coin on the left (`"ABCD"`) is either `heavy` or `normal`.
Each coin on the right (`"EFKL"`) is either `light` or `normal`.

`ABCD` and `EF` were known to be normal already, so we don't have to change their weight.

For `KL`, we now have more specific info, so we update their status accordingly.

```
A: { normal }
B: { normal }
C: { normal }
D: { normal }
E: { normal }
F: { normal }
G: { normal }
H: { normal }
I: { normal }
J: { normal }
K: { light, normal }    // K is light or normal (cannot be heavy)
L: { light, normal }    // L is light or normal (cannot be heavy) 
```

### 3rd Result: `"ABCL DEFK down"`

The outcome is "down" (which is just opposite of `up`).

#### Implication #1 
One of the coins on the scale is a counterfeit. So the **coins that are NOT on the scale are normal**. 

That means, `"GHIJ"` are normal, and we can update the coin table accordingly. 

In this example, the table will remain unchanged after this update.

#### Implication #2
Each coin on the left (`"ABCL"`) is either `light` or `normal`.
Each coin on the right (`"DEFK"`) is either `heavy` or `normal`.


`ABC` and `DEF` were known to be normal already, so we don't have to change their weight.

`L` was known to be either `light` or `normal`. The new info is the same info. (Noting to update)

`K` was known to be either `light` or `normal`. The new info says it is either `heavy` or `normal`. That means `K` has to be normal.

For `KL`, we now have more specific info, so we update their status accordingly.

```
A: { normal }
B: { normal }
C: { normal }
D: { normal }
E: { normal }
F: { normal }
G: { normal }
H: { normal }
I: { normal }
J: { normal }
K: { light, normal }    // K is light or normal (cannot be heavy)
L: { light, normal }    // L is light or normal (cannot be heavy) 
```



Initialization:

Coins start with an unknown status.

Each weighing updates the status of the coins involved.

If the scale is even:

All coins on both sides are normal.

If the scale is unbalanced:

All unused coins must be normal.

The imbalance lets us infer whether a side might contain the light or heavy counterfeit.

Final deduction:

Only one coin should be identified as counterfeit (not normal).

If multiple possibilities remain, return "???".

