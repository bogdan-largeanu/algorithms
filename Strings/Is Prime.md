# Problem 

link: https://www.structy.net/problems/is-prime

```MD
Write a function, is_prime, that takes in a number as an argument. The function should return a boolean indicating whether or not the given number is prime.

A prime number is a number that is only divisible by two distinct numbers: 1 and itself.

For example, 7 is a prime because it is only divisible by 1 and 7. For example, 6 is not a prime because it is divisible by 1, 2, 3, and 6.

You can assume that the input number is a positive integer.

test_00:
is_prime(2) # -> True
test_01:
is_prime(3) # -> True
test_02:
is_prime(4) # -> False
test_03:
is_prime(5) # -> True
test_04:
is_prime(6) # -> False
test_05:
is_prime(7) # -> True
test_06:
is_prime(8) # -> False
test_07:
is_prime(25) # -> False
test_08:
is_prime(31) # -> True
test_09:
is_prime(2017) # -> True
test_10:
is_prime(2048) # -> False
test_11:
is_prime(1) # -> False
test_12:
is_prime(713) # -> False
```


## Solution

Summary: 
Solution 1: We iterate numbers 1 to n, and check if division has any numbers left 

Solution 2: We calculate the square root and only check division as above till that number. We also add a +1 to deal with python one off range


```python

from math import sqrt, floor

def is_prime(n):
  if n < 2:
      return False
  for i in range(2, floor(sqrt(n)+1)):
    isDivisible = (n%i) == 0
    if isDivisible:
      return False
  return True 
               
```