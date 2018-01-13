Answer 1
--------
We know that there is not any solution to Fermat's Last Theorem and it is proved by Andrew Wiles in 1995[1]. However, we can still try to find a solution and fail.

To avoid infinite loops, let (a,b,c,N) ∈ Z+ and (a,b,c) < N

**Pseudocode** 
```C
FIND-FERMAT(k)
a=b=c=1
N=1000
while (a^k + b^k != c^k) && a<N 
 c = c+1
  if c == N
    b = b+1
    if b == N
      a = a+1
      b = a
    c = b
if a!=N
 print "There is a solution for " + a, b ,c
else
 print "No solution for given k value in range of 1 to" + N
```

**Explaination:**
Above pseudocode take k as an input. Then exhaustively searchs all possible values for a,b,c<N and stops either when it finds a solution or runs out of inputs. 

**Why this algorithm is correct?**

We use loop invariants to help us understand why an algorithm is correct. We must show three things about a loop invariant: Initialization, Maintenance, Termination

In above pseudo code Loop Invariant is `(a^k + b^k != c^k) && a<N` <br/>
**Initialization**: It is true prior to the first iteration of the loop. `(1^k + 1^k != 1^k) && 1<N`<br/>
**Maintenance**: For every iteration of the loop, we know that if there were a triple integer(a,b,c) that satisfies the equation loop would stop.<br/>
**Termination**: Finally, we examine the results when loop stops. If we are out of the loop and `a!=N` , this means we have a solution for (a,b,c)'s current values. However, if we are out of the loop and `a!=N`, this means algorithm tried every possible integer triplets and couldn't find a solution for given k value in range of 1 to N.<br/>

**Python Implementation**

Below is a Python3 implementation of the above pseudo-code. If you change the value k to 2, you can see algortihm terminates when it finds a solution at (3,4,5). But for k>3 there is not any solution.
```python
k = 3
N = 1000
a=b=c=1
while (pow(a,k) + pow(b,k) != pow(c,k)) and a<N:
	c = c+1
	if c == N:
		b = b+1
		if b == N:
			a = a+1
			b=a
		c=b
	print(a,b,c)
if(a!=N):
	print ("There is a solution for ", a, b, c)
else:
	print ("No solution for given k value in range of 1 to ", N)
```


[1]A. Wiles, "Modular elliptic curves and Fermat's last theorem," Ann. Math., 141:3 (1995) 443--551.





