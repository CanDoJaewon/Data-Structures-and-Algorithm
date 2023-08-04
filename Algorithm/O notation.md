# Big O Notation
> It is a mathematical way of describing how a function (running time of an algorithm) generally behaves in relation to the input size.
> In Big O notation, all functions that have the same growth rate (as determined by the highest order term of the function) are characterized using the same Big O notation.
> In essence, all functions that have the same growth rate are considered equivalent in Big O notation.


### Big O notation of composite functions
The following rules are used to determine the Big O notation of composite functions: c denotes a constant
Rules for determining Big O notation of composite functions.
Composite function	Big O notation
c · O(f(N))         	O(f(N))
c + O(f(N))          	O(f(N))
g(N) · O(f(N))	      O(g(N) · f(N))
g(N) + O(f(N))	      O(g(N) + f(N))

### Common Big O complexities
Many commonly used algorithms have running time functions that belong to one of a handful of growth functions. 
These common Big O notations are summarized in the following table. 
The table shows the Big O notation, the common word used to describe algorithms that belong to that notation, and an example with source code. 
Clearly, the best algorithm is one that has constant time complexity. Unfortunately, not all problems can be solved using constant complexity algorithms. 
In fact, in many cases, computer scientists have proven that certain types of problems can only be solved using quadratic or exponential algorithms.

### Worst-case algorithm analysis
The worst-case runtime of an algorithm is the runtime complexity for an input that results in the longest execution. 
Other runtime analyses include best-case runtime and average-case runtime. 
Determining the average-case runtime requires knowledge of the statistical properties of the expected data inputs.




