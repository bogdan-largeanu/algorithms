# Problem min change
url: https://www.structy.net/problems/min-change

```

Write a function min_change that takes in an amount and a list of coins. The function should return the minimum number of coins required to create the amount. You may use each coin as many times as necessary.

If it is not possible to create the amount, then return -1.

test_00
min_change(8, [1, 5, 4, 12]) # -> 2, because 4+4 is the minimum coins possible
test_01
min_change(13, [1, 9, 5, 14, 30]) # -> 5
test_02
min_change(23, [2, 5, 7]) # -> 4
test_03
min_change(102, [1, 5, 10, 25]) # -> 6
test_04
min_change(200, [1, 5, 10, 25]) # -> 8
test_05
min_change(2017, [4, 2, 10]) # -> -1
test_06
min_change(271, [10, 8, 265, 24]) # -> -1
test_07
min_change(0, [4, 2, 10]) # -> 0
test_08
min_change(0, []) # -> 0
```


# Solution
Summary: From amount, reduce recursive the value of every coin and add 1 to the count of coins used.
Store the count of coins used and amount in a memo dict to avoid recalculating them again.

Time Complexity O(c ^ a)
Space : O(a)

```python
# Time Complexity O(c ^ a)
# Space : O(a)

def min_change(amount, coins):
  result = _min_change(amount,coins,{})
  if result == float("inf"):
    return -1
  
  return result


def _min_change(amount,coins,memo):
  if amount in memo:
    return memo[amount]
  if amount < 0:
    return float("inf")
  
  if amount == 0:
    return 0
  
  min_coins = float("inf")
  
  for coin in coins:
    count = 1 + _min_change(amount-coin,coins,memo)
    if count < min_coins:
      min_coins = count
  
  memo[amount] = min_coins
  return memo[amount]
  

```