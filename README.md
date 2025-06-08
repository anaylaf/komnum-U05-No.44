- Name : Almira Nayla Felisitha
- NRP : 5025241014
- Class : IUP
- Group : U05

# Number 44
 Integrasikan persamaan f(x,y) = 4x⁴ - 12x² dari X0 = 2 sampai X3 = 11 dengan ukuran step h = 3 dengan menggunakan metoda Euler [Cari nilai error nya juga]  
 Diketahui: 
| i | Xi | f(Xi) |
| - | -- | ---- |
| 0 | 2 | -6.4 |
| 1 | 5 | 2 |
| 2 | 8 | 24.166 |
| 3 | 11 | 123.517 |

# Code
## 1. Import
```
import numpy as np
import math
```
It imports the NumPy library and the math module to perform numerical calculations.

## 2. Initialize
```
h = 3
n = 4
xi_values = np.arange(2, 12, h)

for i in range(0, n):
    print("x" + str(i) + ": " + str(xi_values[i]))

# print(x_values)
```
-   Defines:
    * Step size h = 3
    * Number of steps n = 4
-   Generates xi_values: [2, 5, 8, 11] (x values at each step)

Result :
```  
x0: 2  
x1: 5  
x2: 8  
x3: 11  
```

# Real Solution
```
# real y values (using the normal integral method):
def real_f(x):
  return np.round((4*(x**5)/5) - (4*(x**3)), 2)

f_real = real_f(xi_values) 

for i in range(0, n):
    print("Real f(" + str(i) + "): " + str(f_real[i]))

# print(y_real)
```
- This function calculates the exact solution of some differential equation.
- Formula: f(x) = (4x⁵/5) - 4x³.
- Then it evaluates this function at all xi_values.
 
Results : 
``` 
Real f(0): -6.4  
Real f(1): 2000.0  
Real f(2): 24166.4  
Real f(3): 123516.8  
```

# Function Derivative
```
# f(x, y) values
def y(x):
  return np.round((4*(x**4))-(12*(x**2)), 2)

yi_values = y(xi_values)

for i in range(0, n):
    print("y" + str(i) + ": " + str(yi_values[i]))
```
- This function represents the derivative f'(x) or dy/dx.
- This is used in Euler's method to approximate the next value.

Results
```
y0: 16
y1: 2200
y2: 15616
y3: 57112
```

# Euler Method Calculation
```
# euler method
euler_y = np.zeros(4)

# initialize y0 to the real value of y0
euler_y[0] = f_real[0]

for i in range(0, n-1):
  euler_y[i+1] = euler_y[i] + (h*yi_values[i])

for i in range(0, n):
  print("euler y" + str(i) + ": " + str(euler_y[i]))
```
- Initializes an array euler_y for Euler's results.
- Sets initial condition y0 to the real value of f(x0).

Result : 
``` 
euler y0: -6.4  
euler y1: 41.6  
euler y2: 6641.6  
euler y3: 53489.6  
```

# Error Calculation
```
# errors = (abs(euler_y-f_real))/f_real*100

def error(i):
  return abs(((euler_y[i]-f_real[i]))/f_real[i]*100)
# errors = np.where(np.abs(f_real) > 1e-8,
#                   np.abs(euler_y - f_real) / np.abs(f_real) * 100,
#                   0)

errors = [round(error(i), 2) for i in range(n)]
errors[0] = "-"

print("Initial conditions:")
print("h = 3")
print("n = 4")
print("x0 = 2 to x3=11\n")
print("if f'(x) = 4x^4 - 12x^2, find the values of f(x) using the Euler method")

print("\n")

print("Results:")
print("i  x  Euler y  Exact y  Error")
print("------------------------------------------------------")

for i in range(0, n):
  print(f"{i}  {xi_values[i]}  {euler_y[i]}      {f_real[i]}     {errors[i]}")
``` 
- Calculates and displays the error percentage between Euler's approximation and the real solution at each step to evaluate the accuracy of the Euler method.

Results:
```
Initial conditions:
h = 3
n = 4
x0 = 2 to x3=11

if f'(x) = 4x^4 - 12x^2, find the values of f(x) using the Euler method


Results:
i  x  Euler y  Exact y  Error
------------------------------------------------------
0  2  -6.4      -6.4     -
1  5  41.6      2000.0     97.92
2  8  6641.6      24166.4     72.52
3  11  53489.6      123516.8     56.69
```
