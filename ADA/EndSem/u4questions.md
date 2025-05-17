## 
- The eccentricity of a vertex v is the maximum distance from v to any other vertex
- the center of a graph is the vertex (or vertices) with minimum eccentricity

## Explain the time and space complexity of Floyd Warshall's algorithm.

- Dijas = V.ElogV = V^3logV.
- Floyd Warshall =  v^3.
 space c = v^2
<!-- space c = (nm)*(n+1) -->

## limitations of dynamic programming (DP):

1. High Memory Consumption
DP often uses large 2D/3D tables (e.g., dp[n][w]), which can consume a lot of memory.
This is especially problematic for problems involving large input sizes or dimensions.
Example: In 0/1 Knapsack, space complexity is O(nW), which is infeasible if W is very large.

2. Overlapping Subproblems Must Exist
DP is only applicable when a problem has overlapping subproblems and optimal substructure.
If these properties are missing, DP gives no advantage over other methods.

3. Not Always Intuitive
Identifying the recursive relation and optimal substructure can be difficult.
Designing the correct state representation requires experience and insight.

4. Performance Can Still Be Slow
Even with memoization, problems with large state spaces (e.g., DP on trees or graphs) may still take considerable time.
Time complexity can be polynomial, but for large n, that’s still slow.

5. Space Optimization Not Always Easy
While some DP problems allow space optimization (e.g., using two rows instead of a full table), not all problems can be easily reduced in space.

6. Redundant Computation (If Not Carefully Done)
In top-down (memoization), recursive stack overhead may cause performance degradation if memoization is not properly implemented.

7. Not Suitable for All Problems
Problems without optimal substructure, such as those requiring decisions based on future outcomes, are unsuitable for DP.
    