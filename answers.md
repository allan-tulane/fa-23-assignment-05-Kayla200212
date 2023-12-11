# CMPS 2200 Assignment 5
## Answers

**Name:**__kayla willis_______________________






- **1a.**
(log_d(dn-n+1))-1
each level will have d^i nodes (at level i), meaning that we have a geometric series where the maximum depth would be d^k<=n and the sum of the series can be found to be (d^(k+1)-1)/(d-1)<=n. when solved:
d^(k+1)-1<=n(d-1)
d^(k+1)<=nd-d+1
k+1<=log_d(nd-d+1)
k<=log_d(nd-d+1)-1

- **1b.**
an insert would have O(log_d(n)) while a delete-min would have O(d*log_d(n))
the actual deletion or insertion (respectively) would have a constant time of O(1) but the shifting of the tree to adjust to the change would have the worst case runtimes above. the worst case of the insertion is such because the maximum would be comparing the new node with every parent and switching it upwards to the maximum of becoming the new index of 0. the deletion though has to analyze which child should be promoted to replace the one deleted which in the worst case would be having to go through each child node (d nodes) as well as the swapping with the parents as done in the insertion case, hence it being more costly.

- **1c.**
we would need to combine the work of the delete-min and insertion functions in order to find the bound, but separately:
delete-min: O(|E|log_d(|V|)). As above, the work will be proportional to the height of the heap with |V| vertices (log_d(|V|)) and constrained by the |E| edges. 
insertion: O((|V|d)log_d(|V|)). Work is still proportional to the height (log_d(|V|)) but constrained by both the children d and the vertices themselves |V|.
Total: O(|E|log_d(|V|)) + O((|V|d)log_d(|V|)) => O((|V|d+|E|)log_d|V|)

- **1d.**
we can rearrange the equivalence in terms of |E| and set the work equal to O(|E|) to solve for d. |V| = |E|^(1/(1+\epsilon))

O(|E|^(1/(1+\epsilon))d+|E|)log_d|E|^(1/(1+\epsilon))) = O(|E|)
log_d|E|^(1/(1+\epsilon)) = (1/1+\epsilon)log_d(|E|)
(|E|^(1/(1+\epsilon))d/(1+\epsilon)log_d(|E|)) = |E|
|E|^(1/(1+\epsilon))d + |E| = |E|(1+\epsilon)
|E|^(1/(1+\epsilon))d = |E|(1+\epsilon)
|E|^(1/(1+\epsilon))d = |E|*(1+\epsilon)-|E|
d = |E|\epsilon / |E|^(1/1+\epsilon)


- **2a.**
i dont entirely understand how to solve this question. i know that we will make a nxnxn matrix according to the vertices on the graph relating 0,1,2 to i,j,k. we would have to find the minimum combination of these

- **2b.**
APSP(i,j,2) is the minimum APSP(i,j,1). the shortest path from i to j using 0,1,2 pictured would be either the same as 0,1 or found from i to 2 and back using only vertices 0,1

- **2c.**
the optimal substructure property is that APSP(i,j,k) is the minimum of APSP(i,j,k-1), APSP(i,k,k-1), and APSP(k,j,k-1) because of the linked nature of the graph. the shortest path i to j using 0,1,k is found by using vertices 0,1,k-k following the pattern given of 0,1,n-1

- **2d.**
using memoization we would compute nxnxn problems from scratch because we have 0,1,2 and i,j,k creating a 3x3 matrix of the vertices. thus the work would be O(n^3) because of the matrix of entries being the entire cause of the work computation

- **2e.**
the work of johnsons algorithm is  O(|V|^2 * log(|V|+|V||E|)) so in a case with a dense graph our algorithm would be better but in the case of a sparse graph the johnsons algorithm would be better. 


- **3a.**
no, the solution to MST won't always be the same to the MMET. the MST goal is minimizing the overall sum of all edges in the tree while the MMET in this question would be tasked with minimizing the max value of each individual edge. the processes are not the same so the solution will sometimes, but not always, be the same. in a tree with some low edge weights and some high edge weights, the MST will go for a path that has the lowest cost which may include some high edge weights, while the MMET will go for the lowest edge every time which could end up being more costly. they have a similar overall goal as functions but with distinctly different processes to accomplish it.

- **3b.**
prim's algorithm and kruskal's algorithm were two that we learned were the optimal solutions for MST and could be chosen based on what type of graph would be analyzed. A tree with the next lowest weight would be one where there is the most minimal difference, such as only one edge being replaced that has a slightly higher weight than the original.
-find the optimal solution to the MST using kruskal's without creating any loops. find the optimal weight.
-for each edge in the optimal MST, remove it and calculate the new optimal MST.
-after finding each new MST select the one which had the smallest difference in total weight from the actual optimal MST.

- **3c.**
work of kruskals algorithm: O(|E|log|V|)
remove edge and find new MST: O(|E|*|E|log|V|)
comparing distances: O(1)
total: O(|E|log|V|)+O(|E|*|E|log|V|)
thus the total would be close to O(|E|*|E|log|V|)