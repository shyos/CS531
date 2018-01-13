## Answer 3 ##

Let A denote Given Set, S denote Subset, k denote Target-Sum value and P denote the All Possible Subsets

```Csharp
Subset-Sum-Size1(A,k,i=1)
if i > A.length
	return false
if k == A[i]
	return true
return Subset-Sum-Size1(A,k,i+1)
```

```Csharp
Subset-Sum-Size2(A,k,i)
if i > A.length
	return false
return Subset-Sum-Size2(A,k,i+1) or Subset-Sum-Size1(A,k-a,i+1)
```


```Csharp
Subset-Sum-Size2(A,k)
P = {}
foreach a in A
	S = {}
	if k-a > 0
		S.add(a)
		A.remove(a)
		if (b = Subset-Sum-Size1(A,k-a)) != null
			S.add(b)
			P.add(S)
		A.add(a)
return P
```

