# [Simple Fun #53: Combs](https://www.codewars.com/kata/58898b50b832f8046a0000ec)


## Strategy (Through Simulation)
- Try all possible positions
- Among all the positions that the combs can be combined togehter, remember the shortest combined length


### Algorithm

#### 1. Swap comb1 and comb2 if comb2 is longer (ensure length of comb1 >= length of comb2)

#### 2. Normalization

Suppose 
```
  comb1 = "*.*..***.*" (length L1)
  comb2 = "**.*"       (length L2)
```

To make comparing comb1 and comb 2 easier, prepend and append `"????"` (of length L2) to comb1.

Result of normalization
```
  comb1 = "????*.*..***.*????"
  comb2 = "**.*"
```

#### 3. Slide comb2 across comb1 and check if they can be combined
```
Let minLen = L1 + L2

for startIndex = 0 to L1 + L2
  Let s1 = comb1.substr(startIndex, L2)
  Let s2 = comb2

  Let extraLength = number of '?' in s1

  Check if comb1 and comb2 can be combined together
    Note: s1 and s2 cannot be combined together if they have '*' at the same position

  if (s1 and s2 can be combined)
    minLen = min(minLen, L1 + extraLength)

```

`minLen` is the answer.

