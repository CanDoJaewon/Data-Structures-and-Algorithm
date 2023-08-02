# Recursive Algorithm
> A recursive algorithm is an algorithm that breaks the problem into smaller subproblems and applies the algorithm itself to solve the smaller subproblems.
Because a problem cannot be endlessly divided into smaller subproblems, a recursive algorithm must have a base case: A case where a recursive algorithm completes without applying itself to a smaller subproblem.
>

### Fibonacci numbers
> The Fibonacci sequence is a numerical sequence where each term is the sum of the previous 2 terms in the sequence, except the first 2 terms, which are 0 and 1.
> A recursive function can be used to calculate a Fibonacci number: A term in the Fibonacci sequence.
>
> ### Example code

```
FibonacciNumber(termIndex) {
   if (termIndex == 0)
      return 0
   else if (termIndex == 1)
      return 1
   else
      return FibonacciNumber(termIndex - 1) + FibonacciNumber(termIndex - 2)
}
```
