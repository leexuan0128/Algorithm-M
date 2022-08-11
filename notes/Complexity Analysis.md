## Definition  

### Time Complexity
The time complexity is a function that qualitatively describes the running time of the algorithm. In software development, time complexity is to facilitate developers to estimate the running time for a program operation.

So how to estimate the running time of the program. Usually, the number of operating units of the algorithm is estimated to represent the time of the program consumption. The time of the running of each unit of the default CPU is the same.

Assuming the size of the algorithm is n, then the number of operating units is expressed by function f(n). As the data scale N increases, the growth rate of algorithm execution time is the same as the growth rate of f(n). The gradual complexity of the algorithm is referred to as time complexity, which is recorded as O(f(n)).

## What is the O?  
The big O is used to represent an upper bound trend, when used as an upper bound on the worst-case running time of the algorithm, that is, on the running time of any data input. What the time complexity of the algorithm is is just a general case.  

## Differences in data size  
Because big O is the time complexity when the magnitude of data exceeds a point and the magnitude of data is very large, this amount of data is the amount of data in which the constant coefficient has no decisive role.  

Therefore, the time complexity we mentioned is omitted by the constant number of the number, because in general, the default data is sufficient. Based on this fact, the complexity of the algorithm time given is shown below:

$O(1) < O(logn) < O(n) < O(n^2) < O(n^3) < O(2^n)$  

### Space Complexity
Space Complexity S(n) is a measure of how much memory an algorithm uses during operation, denoted by S(n) = O(F(n))  

We still use big O to represent the Space Complexity of the program, which gives a prior estimate of how much memory the program will need to run.
