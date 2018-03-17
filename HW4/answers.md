## Answers

### 1 Finding Intersection of Two Sets

To solve this in `O(n)`.

Step 1: Define an array K of size k. Set all indexes of K to 0.
Step 2: Iterate i through A and increase `K[A[i]]` by 1.
Step 3: Iterate j through B and increase `K[B[i]]` by 1.
Step 4: Iterate c through K and if `K[c]=2` add c to arraylist C.     

### 2 Odds are even

`Sum of All Degrees(T) = Sum of Even Degrees(A) + Sum of Odd Degrees(B)`

In an undirected graph sum of all degrees equals to `2*(Number of Edges)` which is an even number. Sum of even degrees is also an even number. Hence, `T-A = B(Sum of Odd Degrees)` must be an even number.

### 3 Number of friends at a party

Assume that there is a party where the `N` is the number of people that are present in the party. Let `d.i` to be the degree of an individual which represent the number of people `i'th` person knows at that party.

We need to find if there is a j where `i!=j and d.i=d.j`

Since there are `N` people, a degree value can be a value in range of `0 to N-1`. Which is `N` possible numbers for `N` nodes. However, in a graph we can't have both `0` and `N-1` degreed nodes at the same time. That leaves us with `N-1` options for `N` nodes. From Pigeonhole Principle, we can see that at least two nodes must have same degree value.

### 4 Understanding search trees

Assume `G` has an edge `E` between nodes `A` and `B` that is not belong to `T`.
In DFS this is possible when there is a direct edge between `Node A`  with its ancestor `Node B`. However, if there is such an edge, then in its BFS tree, distance between `Node A` and `Node B` must be 1(Node B is parent of Node A).

Since both trees cannot be the same with such a condition. We can see that there cannot be such an edge `E`.

### 5 An application in wireless networks

Suppose there is a graph `G` with `N` nodes which is not connected thus `G` has two connected components `G1` and `G2`.

Since all nodes have at least degree of `n/2`. `G1` and `G2` must have at least `(n/2)+1` nodes. Since they are not connected, total node number should be `Nodes(G1)+Nodes(G2) = (n/2 + 1) + (n/2 + 1) = n+2` which is a contradiction since we stated that `G` has `N` nodes at the start.

Thus, `G` must be connected and the claim is true.

### 6 An application in robotics

Without reading hint, I had zero idea for the algorithm. With the help of the hint below is my algorithm that runs in O(n^3).

- **Step 1:** Define `H` with every pair of `(u,v)` where distance between `u` and `v` is greater than `r`.To achieve this, run BFS for every node `n` in `G`. BFS gives us the shortest paths between nodes. If a `Node u` has a distance greater than `r` to `Node v`, add `(u,v)` pair to `H` as a node.

- **Step 2:** Define a path from each `(u1,v1)` node to `(u1,v2)` or `(u2,v1)` if such nodes exist in `H`. This means, if there is an edge `(u1,u2)` in `G` and if both `(u1,v1)` and `(u2,v1)` exists in `H`, we add an edge to `H` from node `(u1,v1)` to `(u2,v1)`. Same applies for the other way around, if there is an edge `(v1,v2)` in `G` and if both `(u1,v1)` and `(u1,v2)` exists in `H`, we add an edge to `H` from node `(u1,v1)` to `(u1,v2)`.

- **Step 3:** Now we have all possible configurations(location pairs) for the robots and all possible schedule steps(as edges) that they can use. We apply a BFS that starts from `(a,b)` node and try to find a path to `(c,d)` node on graph `H`.

**Running Time**

- **Step 1:** BFS on Step 1 takes `O(n+m)` time where m can be at most `n*(n-1)`. For `n` nodes it takes `O(n^2+nm) = O(n^2+n^3) = O(n^3)`

- **Step 2:** There can be at most `n^2` (u,v) pairs in `H`, each can have `2*n` possible next node. Thus this step takes `O(n^2 * 2n) = O(n^3)`

- **Step 3:** BFS takes `O(m+n)` where n is `n^2` and m is `n^3`. Thus this step takes `O(n^2+n^3)` = `O(n^3)` time.

In total it takes `O(n^3)` time.
