# [Simple Fun #196: Counterfeit Dollar](https://www.codewars.com/kata/58c61a1e8a452631c5000003)

## Strategy 1 (Through simulation)
- Test all 24 possible coin configurations against the weighting result
- If exactly one coin configuration can satisfy the weighting result, then we have the answer.

### Algorithm
```
  Let coinConfigs = all possible coin configurations // 24 of them
     // 12 different coins, 1 of them is light => 12 different configurations 
     // 12 different coins, 1 of them is heavy => 12 different configurations

  Let satisfied = []       // Store all configurations that satisfy the weighting result
  for each config in coinConfigs
     if (canSatisfy(config, weighting result))
        satisifed.push(config)
  
  if (satisfied.length == 1) {
    // We have a solution
  }
```




## Strategy 2 (By iduction)
- Determine whether a coin is `normal`, `light`, or `heavy` based on the clue provided by the weighting results
- If we can identify exactly one coin as either `light` or `heavy` and all the others as `normal`, then we can determine the answer.

### Algorithm
```
  Initially, set all coins to "unknown" weight

  For each weighting result (left, right, outcome)
    if (outcome is "even")
       // All coins on the scales are normal
       Set all coins on the scales to "normal" weight
    
    if (outcome is "up")
       // All coins not on the scales are normal
       Set all coins NOT on the scales to "normal" weight

       // The coins of the left are either normal or heavy
       Update the weight of each coin on the left in the following way:
         if (the coin weight is "unknown") 
            Set its weight to "heavy"

        if (the coin weight is "light") // previously identified as "light"
            Set its weight to "normal"  // Only a normal coin could be previously identified with a different weight

        // No change needed if the coin weight is "normal" or "heavy"

    if (outcome is "down")
        // "down" is just opposite of "up", so we can use a similar approach to update the weight.

  Let normalCount = # of coins with "normal" weight
  Let counterfeit = the coin with a different weight (its weight can be "heavy", "light", or "unkwown")
  if (normalCount == 11 AND weight of the counterfeit is not "unknown") {
     // We have a solution
  }

```


