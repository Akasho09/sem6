## DP

It is particularly effective when a problem exhibits two key properties:

1. Optimal Substructure: The main problem can be broken down into smaller subproblems, and the optimal solution to the main problem can be constructed from the optimal solutions to these subproblems.
2. Overlapping Subproblems: Subproblems are often solved repeatedly, resulting in redundant calculations. Dynamic programming stores the solutions to these subproblems to save computational effort.

> eg :  Fibonacci series using Top Down memoization.

    if (n <= 1) {

        return n;

    }

    else{

        if (F[n]!=-1){

            retunr F[n];

        }

        else {

        return F[n] = fibonacci(n-1) + fibonacci(n-2)

        }

    }

- Top-Down (Memoization) – Recursion + DP

```cpp
int fib(int n, vector<int>& dp) {
    if (n <= 1) return n;
    if (dp[n] != -1) return dp[n];

    return dp[n] = fib(n - 1, dp) + fib(n - 2, dp);
}
```

- Bottom-Up (Tabulation)

```cpp
int fibonacci(int n) {
    if (n <= 1) return n;

    vector<int> dp(n + 1);
    dp[0] = 0;
    dp[1] = 1;

    for (int i = 2; i <= n; i++)
        dp[i] = dp[i - 1] + dp[i - 2];

    return dp[n];
}
```

- OPTIMIZEED 

```cpp
int fibonacci(int n) {
    if (n <= 1) return n;

    int prev2 = 0, prev1 = 1;
    for (int i = 2; i <= n; i++) {
        int current = prev1 + prev2;
        prev2 = prev1;
        prev1 = current;
    }

    return prev1;
}
```

##  0/1 Knapsack 

- Bottom up. bcz answer at bottom.
- (n+1)(w+1) table.
- call fns.
- check above if present then dont include.

![alt text](<Screenshot 2025-04-06 at 12.21.47 PM.png>)

## LCS 

## Top Down

- O(mn) complexity.
- m==0 or n==0 => termination cond.
- if X[m]==Y[n] ==> 1+LCS(n-1.m-1).
- else 

max {

    LCS(n,m-1) , 

    LCS(n-1,m)

}.

- (m+1)(n+1) table.
- 0 all first row and col
- each entry is max of last row and top col.
- if macth +1. 
- to get substring if its above ==> dont include . 
- move to left and above both.

![alt text](<Screenshot 2025-04-06 at 12.33.56 PM.png>)

## matrix chain multiplication

![alt text](<Screenshot 2025-04-07 at 12.31.07 AM.png>)

- k table give parenthesis 
- search for 1-4 , then new big parenthesis like 2-3(row 2) or 1-3(row 1).


