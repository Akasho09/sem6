## 
- sort by w/kg.
- use algo.
The 0/1 Knapsack Problem is known to be `NP-hard`, and the greedy approach doesn't always guarantee an optimal solution. However, in this specific case, the greedy approach yields the optimal solution because the total weight of all items (16) is less than the knapsack capacity (20). Therefore, all items can be included, achieving the maximum possible value.

Conclusion: In this scenario, the greedy approach provides an optimal solution for the 0/1 Knapsack problem. However, this is not always the case for all instances of the problem.


## 
int rodCutting(int price[], int n) {
    int dp[n+1];
    dp[0] = 0;
    for (int i = 1; i <= n; ++i) {
        int max_val = INT_MIN;
        for (int j = 0; j < i; ++j) max_val = max(max_val, price[j] + dp[i - j - 1]);
        dp[i] = max_val;
    }
    return dp[n];
}


