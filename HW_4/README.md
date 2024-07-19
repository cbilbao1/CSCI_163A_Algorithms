# CSCI_163A_Algorithms
# Homework 4

*NOTE: This file stores the analysis for each problem*
*CODE DONE IN C++*

# *Q1: Design and analyze asymptotically a divide-conquer algorithm for the following problem:*
*input: an array A[lo..hi] of real numbers;*

*output: the sum of elements of A[lo..hi].*
```
int sum (int[] myArray)
{
	//Base case, 1 element in array
	if (myArray.size() == 1)
	{
		//Return the only element as the total net sum
		return myArray[0];
	} else	// Recursive case
	{
		//We will split the array in half
		if (myArray.size() % 2 == 0) // Array size is even, can be evenly divided in half
		{
			//int sum = 0;
			//We are going to have 2 partitions of the array, each half of the original
			int array1[myArray.size() / 2];
			int array2[myArray.size() / 2];
			//Copy the corresponding elements to each array
			for (int i = 0; i <= myArray.size() - 1; ++i)
			{
				if (i =< (myArray.size() / 2) - 1)	// First half of array
				{
					array1[i] = myArray[i];
				} else	// Second half of array
				{
					array2[i] = myArray[i];
				}
			}
			int sum1 = sum(array1);
			int sum2 = sum(array2);
			return sum1 + sum2;
		} else If (myArray.size() % 2 != 0) // Array size is odd
		{
			//Int sum = 0;
			//We are going to have 2 partitions of the array, each half of the original
			int array1[myArray.size() / 2];
			int array2[myArray.size() / 2];
			//Copy the corresponding elements to each array
			for (int i = 0; i <= myArray.size() - 1; ++i)
			{
				if (i =< (myArray.size() / 2) - 1)	// First half of array
				{
					array1[i] = myArray[i];
				} else	// Second half of array
				{
					if (i != (myArray.size() / 2))	// Skip the middle pivot
					{
						array2[i] = myArray[i];
					}
				}
			}
			int sum1 = sum(array1);
			int sum3 = myArray[(myArray.size() / 2)];	// Middle pivot
			int sum2 = sum(array2);
			return sum1 + sum2 + sum3;
		}
	}
}
```
Analysis: I will be analyzing the amount of integer comparisons
M(1) = 1
M(n)	= 2 + 1 + (i = 0Σn - 1)(3) + 2M(n / 2), for n > 1
	= 2 + 1 + (n - 1 - 0 + 1)(3) + 2M(n / 2)
	= 2 + 1 + 3n + 2M(n / 2) = 2M(n / 2) + (3n + 3)
Using the master theorem, a = 2, b = 2, c = 1, and d = 1. So, a ? bd → 2 ? 21 → 2 = 2 → a = bd, which means that M(n) ∈ Θ(nd (lg n)) → M(n) ∈ Θ(n (lg n))
Side note: M(n) = 2 + [(i = 0En - 1)(2) + 1]     + 1 + (i = 0En - 1)(3), for n > 1	[] means the part in even case, didn’t account for recursive calls (mistake), not final answer

# *Q2: Design and analyze asymptotically an O(lgN) divide-conquer algorithm for the following problem:*
*input: a nonnegative integer N;*

*output: 3N.*
```
int multiply (unsigned int N)
{
	//Base case
	if (N == 1)
	{
		return 3;
	} else	// Recursive case
	{
		//We will split the product segment in half
		if (N % 2 == 0) // N is even, can be evenly divided in half
		{
			//Int product = 1;
			//We are going to have 2 partitions of the product, each half of the original
			int product1 = multiply(N / 2);
			int product2 = multiply(N / 2);
			return product1 * product2;
		} else if (N % 2 != 0) // N is odd
		{
			//int product = 1;
			//We are going to have 2 partitions of the product, each half of the original
			int product1 = multiply(N / 2);
			int product3 = 3;	// Middle term in the product
			int product2 = multiply(N / 2);
			return product1 * product2 * product3;
		}
	}
}
```
Analysis: I will be analyzing the amount of multiplications, disregarding the mod.
M(1) = 0
M(n)	= 2M(n / 2) + 2, for n > 1
Using the master theorem, a = 2, b = 2, c = 0, and d = 0. So, a ? bd → 2 ? 20 → 2 > 1 → a > bd, which means that M(n) ∈ Θ(nlogba) → M(n) ∈ Θ(nlog22)
Fix #2: Reduce to only 1 recursive call / Possible! This should be analysis


*Second Attempt At #2*
```
int multiply (unsigned int N)
{
	//Base case
	if (N == 1)
	{
		return 3;
	} else	// Recursive case
	{
		//We will split the product segment in half
		if (N % 2 == 0) // N is even, can be evenly divided in half
		{
			//Int product = 1;
			//We are going to have 2 partitions of the product, each half of the original
			int product1 = multiply(N / 2);
			//Instead of doing another recursive call, we know product2 = product1
			int product2 = product1;
			return product1 * product2;
		} else if (N % 2 != 0) // N is odd
		{
			//Int product = 1;
			//We are going to have 2 partitions of the product, each half of the original
			int product1 = multiply(N / 2);
			int product3 = 3;	// Middle term in the product
			//Instead of doing another recursive call, we know product2 = product1
			int product2 = product1;
			return product1 * product2 * product3;
		}
	}
}
```
M(1) = 0
M(n)	= M(n / 2) + 3, for n > 1
Using the master theorem, a = 1, b = 2, c = 0, and d = 0. So, a ? bd → 1 ? 20 → 1 = 1 → a = bd, which means that M(n) ∈ Θ(nd (lg n)) → M(n) ∈ Θ(n0 (lg n)) → M(n) ∈ Θ(lg n)

# *Q3: Design and analyze asymptotically an O(nlgn) divide-conquer algorithm for the following problem (do not call a sorting algorithm):*
*input: an array A[lo..hi] of n real numbers;*

*output: the smallest difference (in absolute value) between two elements in A[lo..hi].*
```
int difference (float[] myArray)
{
	//Base case, 1 element in array
	if (myArray.size() == 1)
	{
		return myArray[0];
	} else	// Recursive case
	{
		//We will split the array in half
		if (myArray.size() % 2 == 0) // Array size is even, can be evenly divided in half
		{
			//The smallest difference in the bridges cases
			float bridgeDifference = 0;
			//We are going to have 2 partitions of the array, each half of the original
			float array1[myArray.size() / 2];
			float array2[myArray.size() / 2];
			//Copy the corresponding elements to each array
			for (int i = 0; i <= myArray.size() - 1; ++i)
			{
				if (i =< (myArray.size() / 2) - 1)	// First half of array
				{
					array1[i] = myArray[i];
				} else	// Second half of array
				{
					array2[i] = myArray[i];
				}
			}
			float difference1 = difference(array1);
			float difference2 = difference(array2);
			//Initialize the bridgesDifference to start doing comparisons
			bridgesDifference = array1[0] - array2[0];
			//This simulates an absolute value, flips sign
			if (difference1 < 0)
			{
				difference1 *= -1;
			}
			if (difference2 < 0)
			{
				difference2 *= -1;
			}
			if (bridgesDifference < 0)
			{
				bridgesDifference *= -1;
			}
			//This compares all of the values between subarrays, the bridges
			for (int i = 0; i <= myArray.size() - 1; ++i)
			{
				//You only need to compare 7 values in the bridge
				for (int j = 0; j <= 7; ++j)
				{
					//Current difference beats bridgeDifference, update
					if (bridgeDifference > array1[i] - myArray[i + j])
					{
						bridgeDifference = myArray[i] - myArray[i + j];
					}
					if (bridgesDifference < 0)
					{
						bridgesDifference *= -1;
					}
				}
			}
			if (difference1 <= difference2)
			{
				if (difference1 <= bridgesDifference)
				{
					return difference1;
				} else
				{
					return bridgesDifference;
				}
			} else
			{
				if (difference2 <= bridgesDifference)
				{
					return difference2;
				} else
				{
					return bridgesDifference;
				}
			}
		} else if (myArray.size() % 2 != 0) // Array size is odd
		{
			//The smallest difference in the bridges cases
			float bridgeDifference = 0;
			//We are going to have 2 partitions of the array, each half of the original
			float array1[myArray.size() / 2];
			float array2[myArray.size() / 2];
			//Copy the corresponding elements to each array
			for (int i = 0; i <= myArray.size() - 1; ++i)
			{
				if (i =< (myArray.size() / 2) - 1)	// First half of array
				{
					array1[i] = myArray[i];
				} else	// Second half of array
				{
					if (i != (myArray.size() / 2))	// Skip the middle pivot
					{
						array2[i] = myArray[i];
					}
				}
			}
			float difference1 = difference(array1);
			float difference2 = difference(array2);
			//Initialize the bridgesDifference to start doing comparisons
			bridgesDifference = array1[0] - array2[0];
			//Int sum1 = sum(array1);
			float pivDifference = myArray[(myArray.size() / 2)];	// Middle pivot
			//Int sum2 = sum(array2);
			//This simulates an absolute value, flips sign
			if (difference1 < 0)
			{
				difference1 *= -1;
			}
			if (difference2 < 0)
			{
				difference2 *= -1;
			}
			if (pivDifference < 0)
			{
				pivDifference *= -1;
			}
			if (bridgesDifference < 0)
			{
				bridgesDifference *= -1;
			}
			//This compares all of the values between subarrays, the bridges
			for (int i = 0; i <= myArray.size() - 1; ++i)
			{
				//You only need to compare 7 values in the bridge
				for (int j = 0; j <= 7; ++j)
				{
					//Current difference beats bridgeDifference, update
					if (bridgeDifference > array1[i] - myArray[i + j])
					{
						bridgeDifference = myArray[i] - myArray[i + j];
					}
					if (bridgesDifference < 0)
					{
						bridgesDifference *= -1;
					}
				}
			}
			if (difference1 <= difference2)
			{
				if (difference1 <= bridgesDifference)
				{
					return difference1;
				} else if (bridgesDifference < difference1)
				{
					if (bridgesDifference < pivDifference)
					{
						return bridgesDifference;
					} else
					{
						return pivDifference;
					}
				}
			} else
			{
				if (difference2 <= bridgesDifference)
				{
					return difference2;
				} else if (bridgesDifference < difference2)
				{
					if (bridgesDifference < pivDifference)
					{
						return bridgesDifference;
					} else
					{
						return pivDifference;
					}
				}
			}
		}
	}
}
```
Analysis: I will be analyzing the amount of comparisons
M(1) = 1
M(n)	= 1 + 1 +  [1 + ((i = 0Σn - 1)(2) + 1) + 2M(n) + 4 + (Θ(n)) + 4]
	= 1 + 1 +  [1 + ((n - 1 - 0 + 1)(2) + 1) + 2M(n) + 4 + (Θ(n)) + 4]
	= 3 + (2n + 1) + 2M(n) + 4 + (Θ(n)) + 4]
	= 2M(n / 2) + 2n + 12 + Θ(n) = 2M(n / 2) + Θ(n)
Using the master theorem, a = 2, b = 2, c = 1, and d = 1. So, a ? bd → 2 ? 21 → 2 = 2 → a = bd, which means that M(n) ∈ Θ(nd (lg n)) → M(n) ∈ Θ(n1 (lg n)) → M(n) ∈ Θ(n (lg n))
