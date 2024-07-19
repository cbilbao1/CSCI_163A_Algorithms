# CSCI_163A_Algorithms
# Homework 3

*NOTE: This file stores the analysis for each problem*

# *Q1: Design and analyze a brute-force algorithm for the following problem:*
*input: a positive integer N;*
*output: the sum 1^4 + 2^4 + ⋯ + N^4.*

A1: Code done with C++
We can see that the first term is 1 4, which is N 4 where N = 1. So, the base case has N = 1.
```
int bruteSum (unsigned int N)
  {
	  //sum initialized
	  sum = 0;
	  //The term initialized, to be easier to see
	  term = 0;
	  for (unsigned int i = 1; i <= N; ++i)
    {
	    //Updates the current term, which is i to the power of 4
	    term = i * i * i * i;	// Not using any external functions, is just i 4
	    //Adds the current term to the overall sum
      sum += Term;
    }
    //Returns the sum
    return sum;
    }
```
Analysis: I will be analyzing only the number of multiplication operations for worst case analysis. The for loop turns into a summation. There are three multiplication operations in one line of the for loop.
The for loop runs at i = 1 to i <= N. So, it becomes i = 1Σn (3) = 3(i = 1Σn (1)) = 3(n - 1 + 1) = 3n
