# [Simple Fun #53: Combs](https://www.codewars.com/kata/58898b50b832f8046a0000ec)


## Strategy (Through Simulation)
- Try all possible positions
- Among all the positions that the combs can be combined togehter, remember the shortest combined length


### Algorithm

Given `comb1` and `comb2`. 
Let `L1` and `L2` be the length of comb1 and comb2 respectively.

#### 1. Preprocessing (to make comparing comb1 and comb2 easier)

- **Prepend** and **append** a string of length `L2` consisting entirely of the character `'?'` (that serves as a special marker).

For example, if 
```
  comb1 = "*.*..***.*" 
  comb2 = "**.*"       
```
then we convert `comb1` to
```
  comb1 = "????*.*..***.*????"
  comb2 = "**.*"
```
so that when we slide `comb2` across `comb1` to check if they can be combined, we always have `L2` characters to compare.

#### 2. Slide comb2 across comb1 and check if they can be combined
```
Let minLen = L1 + L2

for startIndex = 0 to L1 + L2 - 1
  Let s1 = comb1.substr(startIndex, L2)
  Let s2 = comb2

  Let extraLength = number of '?' in s1

  Check if s1 and s2 can be combined
  Note: s1 and s2 cannot be combined if they both have a '*' at the same position in any index.

  if (s1 and s2 can be combined)
    minLen = min(minLen, L1 + extraLength)

```

`minLen` is the answer.

