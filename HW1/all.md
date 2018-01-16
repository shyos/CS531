Answer 1
--------
We know that there is not any solution to Fermat's Last Theorem and it is proved by Andrew Wiles in 1995[1]. However, we can still try to find a solution and fail.

To avoid infinite loops, let (a,b,c,N) ∈ Z+ 

**Pseudocode** 
```C
FIND-FERMAT(k)
a=b=c=1
while (a^k + b^k != c^k) 
 if a equals b and b equals c
  c=c+1
  a=b=1
 else if a equals b
  b=b+1
  a=1
 else
  a=a+1

print "There is a solution for " + a, b ,c

```

**Explaination:**
Above pseudocode takes k as an input. Then exhaustively searchs all possible values for a,b,c and stops when it finds a solution. It tries all possible (a,b)<=c pairs for c value. Then increaments c and then tries all (a,b)<=c values for new c value. It continues until it finds a solution or when program crashes at a physical limit. 

**Why this algorithm is correct?**

We use loop invariants to help us understand why an algorithm is correct. We must show three things about a loop invariant: Initialization, Maintenance, Termination

In above pseudo code Loop Invariant is `(a^k + b^k != c^k)` <br/>
**Initialization**: It is true prior to the first iteration of the loop. `(1^k + 1^k != 1^k)`<br/>
**Maintenance**: For every iteration of the loop, we know that if there were a integer(a,b,c) triplet that satisfies the equation loop would stop.<br/>
**Termination**: Finally, we examine the results when loop stops. If loop stops at some point, this means algorithm tried every possible integer triplets and find a solution for given k value.<br/>

**Python Implementation**

Below is a Python3 implementation of the above pseudo-code. If you change the value k to 2, you can see algortihm terminates when it finds a solution at (3,4,5). But for k>3 there is not any solution. Feel free to try!

```python
k = 3
a=b=c=1
while (pow(a,k) + pow(b,k) != pow(c,k)) :
 if a == b and b == c :
  c=c+1
  a=b=1
 elif a == b :
  b=b+1
  a=1
 else :
  a=a+1

print "There is a solution for ", a, b, c

```


[1]A. Wiles, "Modular elliptic curves and Fermat's last theorem," Ann. Math., 141:3 (1995) 443--551.






## Answer 2 ##
I would say him 2 things: <br/>
1- Make sure of the correctness of base cases and give minimum number of base cases as possible.<br/>
2- Make sure you can prove your algorithm recursively such as T(n) with T(n-1) and T(n-1) from T(n-2) and so on.

## Answer 3 ##

Let A denote Given Set, k denote Target-Sum value and i denote current index value for function

**Part 0**<br/>
Below  is the trivial S=|1| case. It basically returns if there is a value in the input set which equals to k.
```Csharp
Subset-Sum-Size1(A,k,i=1)
if i > A.length
	return false
if k == A[i]
	return true
return Subset-Sum-Size1(A,k,i+1)
```
**Part A** - O(n^2) algorithm
Using Part 0, below is the S=|2| case. 
```Csharp
Subset-Sum-Size2(A,k,i)
if i > A.length
	return false
return Subset-Sum-Size2(A,k,i+1) or Subset-Sum-Size1(A,k-a,i+1)
```
**Part B** - Proof of Part A
Since we are using Part 0 for the Part A of the algorithm. First we need to show that algorithm in Part 0 is true. <br/>
Initilization(base case): For a given set A, index starts from first element of the set A as i=1. It checks if there is a i'th value in set A, and if there is it checks whether A[i] is equal to sum value k.<br/>
Maintenance: At each iteration algorithm increases index value and checks base cases. <br/>
Termination: If i reaches a value that bigger than length of the set A, then this means algorithm reached to end of the set and could not find a solution. However, if algorithm finds an A[i]=k equation the it terminates with a found solution.

Now knowing Part 0 algortihm is correct and terminates with right value, we can prove Part A algorithm. <br/>
Initilization(base case): For a given set A, index starts from first element of the set A as i=1. It checks if there is a i'th value in set A.<br/>
Maintenance: At each iteration algorithm increases index value and checks base cases. Then it runs algorithm both Part A and Part 0 for the i+1 value. <br/>
Termination: If i reaches a value that bigger than length of the set A, then this means algorithm reached to end of the set and could not find a solution. However, if Part 0 of the 	maintenance returns a true value, then this means there is a solution for S=|2|

**Part C** - O(n^x) algorithm for case S=|X|
Below is the S=|x| case. At this part we just merge Part A and Part 0 and then put an X value to find solutions for only S=|x| not S<=|x| and we count each step and reduce x accordingly. We know the algorithm for F(1) and F(2), thus we can recursivley check F(n-1) for F(n), F(n-2) for F(n-1) .... F(1) for F(2).

```Csharp
Subset-Sum-SizeX(A,k,i,x)
if i > A.length
	return false
if k == A[i] and x == 1
	return true
return Subset-Sum-SizeX(A,k,i+1,x) or Subset-Sum-SizeX(A,k-a,i+1,x-1)
```
**Part D** = O(nlogn) algorithm for S=|2| <br/>
To achieve this, we need given set A as sorted at start. This will reduce our search time for the j in i+j=k equation.

```Csharp
MergeSort(A) // This take O(nlogn) in worst case and gives us a sorted array.
Subset-Sum-SizeX(A,k,i,2)
if i > A.length
	return false
if k == A[i] and x == 1
	return true
return Subset-Sum-SizeX(A,k,i+1,x) or BinarySearch(A,k-a,i+1,x-1)
```
**Part E** Proof of Part D<br/>
Since we can sort an array in O(nlogn) time with MergeSort, first step is trivial. Then we start our algorithm. However to reduce O(n^2) to O(nlogn) for Subset Algorithm, we need change our style to finding j value in i+j=k. Since we have a sorted set A now, we can use BinarySearch to find j. Binary search terminates in O(logn). Since we run BinarySearch n times and we know that, algorithm was correct from Part B, we can say that our algorithm terminates with correct output in O(nlogn)
