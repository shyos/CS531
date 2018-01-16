
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

**Part C** - O(n^x) algorithm
Below is the S=|x| case. At this part we just merge Part A and Part 0. Now, we are not directly checking every P(1)| value for each P(n=2) (was n=2 in previous part), instead we check P(n-1) for P(n)
```Csharp
Subset-Sum-SizeX(A,k,i)
if i > A.length
	return false
if k == A[i]
	return true
return Subset-Sum-Size2(A,k,i+1) or Subset-Sum-Size2(A,k-a,i+1)
```

