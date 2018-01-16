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





