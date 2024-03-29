# Homework 5
Ramaseshan Parthasarathy, Ashwin Sethi

## Problem 1
![](img/p1_horner.gif "horner")

## Problem 2

### Part A
![](img/p2a.gif "mono") 

### Part B
![](img/p2b1.gif "lag")  
![](img/p2b2.gif "lag2")  
![](img/p2b3.gif "lag3")

### Part C
![](img/p2c.gif "newt")

## Problem 3

### Part A
![](img/p3a1.gif "monomial")  
![](img/p3a2.gif "monomial2")

### Part B
![](img/p3b1.gif "lagrange1")  
![](img/p3b2.gif "lagrange2")  
![](img/p3b3.gif "lagrange3")  
![](img/p3b4.gif "lagrange4")

### Part C

#### Triangular Matrix
![](img/p3ca1.gif "newton-one-one")  
![](img/p3ca2.gif "newton-one-two")  
![](img/p3ca3.gif "newton-one-three")  
![](img/p3ca4.gif "newton-one-four")  
![](img/p3ca5.gif "newton-one-five")

#### Incremental Interpolation
![](img/p3cb1.gif "newton-two-one")  
![](img/p3cb2.gif "newton-two-two")  
![](img/p3cb3.gif "newton-two-three")  
![](img/p3cb4.gif "newton-two-four")  
![](img/p3cb5.gif "newton-two-five")

#### Divided Differences
![](img/p3cc1.gif "newton-three-one")  
![](img/p3cc2.gif "newton-three-two")  
![](img/p3cc3.gif "newton-three-three") 

## Problem 4

### Part A
![](img/p4a1.gif "four-one")    
![](img/p4a2.gif "four-two")  
![](img/p4a3.gif "four-three")

### Part B
![](img/p4b.gif "lag-four")    

## Problem 5 (Extra Credit)

```python
import numpy as np

def add(arg1, arg2): #helper method to add lists
    array = []
    for i in range(len(arg2)): #arg1's size must be <= arg2's size
        if i >= len(arg1):
            array.append(arg2[i])
        else:
            array.append(arg1[i] + arg2[i])
    return array

def flip(arr): #flips array
    return arr[::-1]

def valueOf(coefficients, value):
    n = len(coefficients)
    if n == 1:
        return coefficients[0] #base case
    return coefficients[0] + value * valueOf(coefficients[1:], value)

def derive(coefficients, derivative):
    n = len(coefficients)
    if n == 1: #base case
        return [0] * (len(derivative))
    derivative.append(coefficients[n-1])
    return add(np.copy(derivative), derive(coefficients[:n-1], derivative))

def extraCredit(coefficients, x):
    value = valueOf(coefficients, x)
    derivative = flip(derive(coefficients, []))
    derivativeValue = valueOf(derivative, x)
    return value, derivativeValue, derivative
def main():
    f1 = [2, 3, 5, 4] # f(x) = 2 + 3x + 5x^2 + 4x^3
    x = 3
    v1, dv1, d1 = extraCredit(f1, x)
    print('Value f1 = ', v1)
    print('Derivative f1 = ', d1)
    print('Derivative Value @ x = 3 = ', dv1)

    f2 = [9, -10, 0, -5, 0, 2] # f(x) = 9 - 10x - 5x^3 + 2x^5
    v2, dv2, d2 = extraCredit(f2, x)
    print('Value f2 = ', v2)
    print('Derivative f2 = ', d2)
    print('Derivative Value @ x = 3 = ', dv2)

    f3 = [24, 12, -8, 5, 4] # f(x) = 24 + 12x - 8x^2 + 5x^3 + 4x^4
    v3, dv3, d3 = extraCredit(f3, x)
    print('Value f3 = ', v3)
    print('Derivative f3 = ', d3)
    print('Derivative Value @ x = 3 = ', dv3)
main()
```
The program uses a recurrence relation to evaluate a polynomial f(x) at x = x<sub>0</sub>. The results of evaluation at x = 3 are shown below:  \
![](img/p5ec.png "extra") 

