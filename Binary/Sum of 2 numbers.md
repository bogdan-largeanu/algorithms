[Leetcode Example Sum of 2 numbers without using + operator ](https://leetcode.com/problems/sum-of-two-integers/)

## In order to do sum of 2 numbers without arithmetic operator or build in functions we need to leverage bit operations. 

Let's take 2 examples 1 and 3. Converting them in binary we get:  

`1 = "01"`
`3 = "11"`


There are 3 bit operations. 

Operation: AND -> a) 1 & 1 => 1  b) 1 & 0 => 0 c) 0^0 => 0
Operation: OR -> a) 1 | 0 => 1 b) 1 | 1 => 1 c) 0|0 => 0
Operation: Xor -> a) 1 ^ 0 => 1 b) 1 ^ 1 => 0 c) 0^0 => 0 

To calculate the sum of 2 numbers we can try to use first XOR.
You will notice XOR removes the 1 when two bits are positive, so we need to carry them over, same way in 6+6 we cary over 1 to generate 12.
Example XOR: `01^ 01 = 00`. What We actually want is `10`.

In order to do that we need to find the carry. We can do that using the `AND operator`. 

`01 & 11 => 01 `

Now we need to repeat this until carry becomes 0. With the order being carry first, then xor.


Atention! 
We will store the carry in `b` after we do the first xor and and (since we got is values already processed)
We will store the xor in `a`

Taking the following values:
a = 2 = binary 10 
b = 2 = binary 10

Until carry/b is 0 we do:

```python
While b != 0:
//    Step 1 carry:
     carry = a & b
     
//    Step 2 Xor :
     a = a ^ b 

//    Step 3 Shift Carry by 1 
     b = carry << 1
//Step 4 return the sum stored in a     
return a 
 
```
Let's see what happens inside 

Iteration 1:
```
a = 10, b=10 //in binary format
While b != 0:
//    Step 1 carry:
     carry = a & b // 10
//    Step 2 Xor :
     a = a ^ b // 00
//    Step 3 Shift Carry by 1 
     b = carry << 1  // 100
```

Iteration 2:
```
a = 00, b=100 //in binary format
While b != 0:
//    Step 1 carry:
     carry = a & b // 000
//    Step 2 Xor :
     a = a ^ b // 100
//    Step 3 Shift Carry by 1 
     b = carry << 1  // 0000 (new 0 added but it means nothing since is still 0)
return a // 100 which is 4 in base 10(normal numbers)
```



If you want to test the code here's a python version 
```python3

def Bitwise_add(a,b):
    
    while b != 0:
        print(f'a: {bin(a)} b:{bin(b)}')
        carry = a&b # Carry value is calculated 
        a = a^b # Sum value is calculated and stored in a
        b = carry<<1 # The carry value is shifted towards left by a bit
        print(f'a^b: {bin(a)} | carry: {bin(carry)} | carry<<1: {bin(b)} ')

    return a # returns the final sum
    
sum = Bitwise_add(2,2)

print(f'sum is : {sum}')
```