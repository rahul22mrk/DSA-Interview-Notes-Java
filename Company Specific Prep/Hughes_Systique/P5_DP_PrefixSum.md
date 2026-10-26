# Priority 5: Prefix Sum + DP
```
Yahan do reported patterns relevant hain: Longest Subarray with Zero Sum aur Knapsack.
```

## Questions:
```
1. Longest Subarray with Zero Sum
2. Subarray Sum Equals K
3. 0/1 Knapsack
4. Climbing Stairs
5. House Robber
```

```
Resources:
- LeetCode 560 — Subarray Sum Equals K
- GeeksforGeeks — 0/1 Knapsack
```

1. Longest Subarray with Zero Sum
```

```

```java

```

```java

```

```java

```

2. Subarray Sum Equals K
```
https://takeuforward.org/practice/dsa/count-subarrays-with-given-sum
```

```java
public int subarraySum(int[] nums, int k) {
        int n = nums.length;
        // Number of subarrays
        int cnt = 0;
 
        // starting index i
        for (int i = 0; i < n; i++) {
            // ending index j
            for (int j = i; j < n; j++) {
 
                // calculate the sum of subarray [i...j]
                int sum = 0;
                for (int K = i; K <= j; K++)
                    sum += nums[K];
 
                // Increase the count if sum == k:
                if (sum == k)
                    cnt++;
            }
        }
        return cnt;
    }
Time Complexity: O(N3), where N is the size of the array. We are using three nested loops here. Though all loops are not running exactly N times, the time complexity will be approximately O(N3).

Space Complexity: O(1), as we are not using any extra space.
```

```java
public int subarraySum(int[] nums, int k) {
        int n = nums.length;
        // Number of subarrays
        int count = 0;
 
        // starting index
        for (int startIndex = 0; startIndex < n; startIndex++) {
            int currentSum = 0;
            // ending index
            for (int endIndex = startIndex; endIndex < n; endIndex++) {
                // calculate the sum of subarray [startIndex...endIndex]
                // sum of [startIndex..endIndex-1] + nums[endIndex]
                currentSum += nums[endIndex];
 
                // Increase the count if currentSum == k:
                if (currentSum == k)
                    count++;
            }
        }
        return count;
    }
Time Complexity: O(N2), where N is the size of the array. We are using two nested loops here, each running for approximately N times. Therefore, the time complexity will be approximately O(N2).

Space Complexity: O(1), as we are not using any extra space to solve this problem.
```

```java
public int subarraySum(int[] nums, int k) {
        int n = nums.length;
        HashMap<Integer, Integer> prefixSumMap = new HashMap<>();
        int currentPrefixSum = 0, subarrayCount = 0;
 
        // Setting 0 in the map.
        prefixSumMap.put(0, 1);
        for (int i = 0; i < n; i++) {
            // Add current element to the prefix sum:
            currentPrefixSum += nums[i];
 
            /* Calculate the value to remove
            (currentPrefixSum - k)*/
            int sumToRemove = currentPrefixSum - k;
 
            /* Add the number of subarrays 
            with the sum to be removed*/
            subarrayCount += prefixSumMap.getOrDefault(sumToRemove, 0);
 
            /*Update the count of current
            prefix sum in the map*/
            prefixSumMap.put(currentPrefixSum, prefixSumMap.getOrDefault(currentPrefixSum, 0) + 1);
        }
        return subarrayCount;
    }
Time Complexity: O(N) or O(NxlogN) depending on the map data structure used, where N is the size of the array. For example, if we use an unordered_map in C++, the time complexity will be O(N), but if we use a map, the time complexity will be O(NxlogN). The minimum complexity is O(N) as we are using a single loop to traverse the array.

Space Complexity: O(N) as we are using a map data structure.
```

3. 0/1 Knapsack
```
https://takeuforward.org/practice/dsa/0-and-1-knapsack
https://www.geeksforgeeks.org/problems/0-1-knapsack-problem0945/1
```

```java
// Function to solve the 0/1 Knapsack problem with arrays
    private int func(int[] wt, int[] val, int ind, int W, int[][] dp) {
        /* Base case: If there are no items left
        or the knapsack has no capacity, return 0 */
        if (ind < 0 || W == 0) {
            return 0;
        }
 
        /* If the result for this state is
        already calculated, return it */
        if (dp[ind][W] != -1) {
            return dp[ind][W];
        }
 
        /* Calculate the maximum value by either
        excluding the current item or including it */
        int notTaken = func(wt, val, ind - 1, W, dp);
        int taken = 0;
 
        /* Check if the current item can be included
        without exceeding the knapsack's capacity */
        if (wt[ind] <= W) {
            taken = val[ind] + func(wt, val, ind - 1, W - wt[ind], dp);
        }
 
        // Store the result in the DP table and return
        dp[ind][W] = Math.max(notTaken, taken);
        return dp[ind][W];
    }
 
    public int knapsack01(int[] wt, int[] val, int n, int W) { 
        // Initialize DP table with -1
        int[][] dp = new int[n][W + 1];
        for (int[] row : dp) {
            Arrays.fill(row, -1);
        }
        return func(wt, val, n - 1, W, dp);
    }
Time Complexity: O(N*W),
Space Complexity:O(N*W) + O(N),
```

```java
public int knapsack01(int[] wt, int[] val, int n, int W) {
        /* Declare a 2D DP table with dimensions
        n x W+1 and initialize it with zeros*/
        int[][] dp = new int[n][W + 1];
 
        /* Base condition: Fill in the first 
        row for the weight of the first item*/
        for (int i = wt[0]; i <= W; i++) {
            dp[0][i] = val[0];
        }
 
        // Fill in DP table using a bottom-up approach
        for (int ind = 1; ind < n; ind++) {
            for (int cap = 0; cap <= W; cap++) {
                /* Calculate the maximum value by either
                excluding the current item or including it*/
                int notTaken = dp[ind - 1][cap];
                int taken = Integer.MIN_VALUE;
 
                /* Check if the current item can be included
                without exceeding the knapsack's capacity*/
                if (wt[ind] <= cap) {
                    taken = val[ind] + dp[ind - 1][cap - wt[ind]];
                }
 
                // Update the DP table
                dp[ind][cap] = Math.max(notTaken, taken);
            }
        }
 
        // The final result is in the last cell
        return dp[n - 1][W];
    }
Time Complexity: O(N*W), where N is the size of the array. As two nested loops are used for the calculations.
Space Complexity:O(N*W), As a 2D array of size N*W is used.
```

```java
 public int knapsack01(int[] wt, int[] val, int n, int W) {
        /* Initialize a vector 'prev' to represent 
        the previous row of the DP table*/
        int[] prev = new int[W + 1];
 
        /* Base condition: Fill in 'prev' 
        for the weight of the first item*/
        for (int i = wt[0]; i <= W; i++) {
            prev[i] = val[0];
        }
 
        // Fill in the table using a bottom-up approach
        for (int ind = 1; ind < n; ind++) {
            for (int cap = W; cap >= 0; cap--) {
                /* Calculate the maximum value by either 
                excluding the current item or including it*/
                int notTaken = prev[cap];
                int taken = Integer.MIN_VALUE;
 
                /* Check if the current item can be included 
                without exceeding the knapsack's capacity*/
                if (wt[ind] <= cap) {
                    taken = val[ind] + prev[cap - wt[ind]];
                }
 
                // Update 'prev' for the current capacity
                prev[cap] = Math.max(notTaken, taken);
            }
        }
 
        /* The final result is in the
        last cell of the 'prev' vector*/
        return prev[W];
    }
 Time Complexity: O(N*W), where N is the size of the array. As two nested loops are used for the calculations.

Space Complexity:O(W), We are using an external array of size ‘W+1’ to store only one row.
```

4. Climbing Stairs
```
https://leetcode.com/problems/climbing-stairs/description/
https://takeuforward.org/practice/dsa/climbing-stairs
```

```java
// Memoization approach:
private int func(int n, int dp[]){
        //Base condition
        if (n <= 1) {
            return 1;
        }
        
        //Check if the subproblem is already solved
        if (dp[n] != -1) {
            return dp[n];
        }
        
        //Return the calculated value
        return dp[n] = func(n-1, dp) + func(n-2, dp);
    }
    // Function to count total ways to reach nth stair
    public int climbStairs(int n) {
        int[] dp = new int[n+1];
        
        // Initialize dp array with -1
        Arrays.fill(dp, -1);
        
        // Return the calculated value
        return dp[n] = func(n, dp);
    }
Time Complexity: O(N)
Space Complexity:O(N)+O(N)
```

```java
// Tabulation approach:
public int climbStairs(int n) {
        // Declare dp array of size n+1
        int[] dp = new int[n + 1];
 
        // Insert the values of base conditions
        dp[0] = 1;
        dp[1] = 1;
 
        // Iterate and update every index of dp array
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
 
        // Return the answer
        return dp[n];
    }
Time Complexity: O(N)
Space Complexity:O(N)
```

```java
//Space Optimization:
public int climbStairs(int n) {
        /*Initialize two variables to 
        store previous results*/
        int prev2 = 1;
        int prev = 1;
        
        //Iterate and update the variables
        for (int i = 2; i <= n; i++) {
            int cur_i = prev2 + prev;
            prev2 = prev;
            prev = cur_i;
        }
        //Return the answer as prev
        return prev;
    }
Time Complexity: O(N)
Space Complexity:O(1)
```

5. House Robber
```
https://leetcode.com/problems/house-robber/description/
https://takeuforward.org/practice/dsa/house-robber
```
```
Leetcode style
```

```java
class Solution {
    int dp[]=new int[101];
    public int rob(int[] nums) {
        Arrays.fill(dp,-1);
        return solve(nums,0,nums.length);
        
    }

    private int solve(int[] nums,int i,int n){
        if(i>=n){
            return 0;
        }

        if(dp[i]!=-1){
            return dp[i];
        }

        int steal = nums[i]+solve(nums,i+2,n);
        int skip = solve(nums,i+1,n);
        return dp[i]=Math.max(steal,skip);
    }
}
```
```java
class Solution {
    public int rob(int[] nums) {
        int prev = nums[0];
        int prev2 = 0;

        for(int i=1; i<nums.length; i++){
            int pick = nums[i];
            if(i>1){
                pick += prev2;
            }

            int notPick = prev;

            int curr = Math.max(pick, notPick);
            prev2 = prev;
            prev = curr;
        }
        return prev;
        
    }

}
```
```
circular condition
```
```java
class Solution {
    public int houseRobber(int[] money) {
        int n = money.length;

        if (n == 1) {
            return money[0];
        }

        int[] dp1 = new int[n];
        Arrays.fill(dp1, -1);

        int[] dp2 = new int[n];
        Arrays.fill(dp2, -1);

        return Math.max(
            solve(money, 0, n - 2, dp1),
            solve(money, 1, n - 1, dp2)
        );
    }

    private int solve(int[] money, int start, int end, int[] dp) {
        if (start > end) {
            return 0;
        }

        if (dp[start] != -1) {
            return dp[start];
        }

        int taken = money[start] + solve(money, start + 2, end, dp);
        int notTaken = solve(money, start + 1, end, dp);

        return dp[start] = Math.max(taken, notTaken);
    }
}
```

```java
private int func(int ind, int[] arr, int[] dp) {
        // Base cases
        if (ind == 0)
            return arr[ind];
        if (ind < 0)
            return 0;
 
        // If dp[ind] already has a value, return it
        if (dp[ind] != -1) {
            return dp[ind];
        }
 
        // Choosing the current element
        int pick = arr[ind] + func(ind - 2, arr, dp);
 
        // Skipping the current element
        int nonPick = func(ind - 1, arr, dp);
 
        /* Store the result in dp 
        array and return the maximum*/
        return dp[ind] = Math.max(pick, nonPick);
    }
 
    // Function to find the maximum money robber can rob
    public int houseRobber(int[] money) {
        int n = money.length;
        if (n == 0)
            return 0;
        if (n == 1)
            return money[0];
 
        int[] arr1 = new int[n - 1];
        int[] arr2 = new int[n - 1];
 
        // Populate arr1 and arr2
        for (int i = 0; i < n; i++) {
            if (i != n - 1)
                arr1[i] = money[i];
            if (i != 0)
                arr2[i - 1] = money[i];
        }
 
        // Initialize the dp arrays with -1
        int[] dp1 = new int[n];
        Arrays.fill(dp1, -1);
        int ans1 = func(arr1.length - 1, arr1, dp1);
 
        int[] dp2 = new int[n];
        Arrays.fill(dp2, -1);
        int ans2 = func(arr2.length - 1, arr2, dp2);
 
        // Return the maximum of ans1 and ans2
        return Math.max(ans1, ans2);
    }
Time Complexity: O(N) + O(N), 
Space Complexity:O(N) + O(N) + O(N) + O(N) + O(N) + O(N)
```

```java
  private int func(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        
        // Base case
        dp[0] = nums[0];
 
        // Iterate through the elements of the array
        for (int i = 1; i < n; i++) {
            
            /* Calculate maximum value by either picking
            the current element or not picking it */
            int pick = nums[i];
            if (i > 1)
                pick += dp[i - 2];
            int nonPick = dp[i - 1];
 
            // Store the maximum value in dp array
            dp[i] = Math.max(pick, nonPick);
        }
 
        /* The last element of the dp array
        will contain the maximum sum */
        return dp[n - 1];
    }
 
    // Function to find the maximum money robber can rob
    public int houseRobber(int[] money) {
        int n = money.length;
        if (n == 0)
            return 0;
        if (n == 1)
            return money[0];
 
        int[] arr1 = new int[n - 1];
        int[] arr2 = new int[n - 1];
 
        // Populate arr1 and arr2
        for (int i = 0; i < n; i++) {
            if (i != n - 1)
                arr1[i] = money[i];
            if (i != 0)
                arr2[i - 1] = money[i];
        }
        int ans1 = func(arr1);
 
        int ans2 = func(arr2);
 
        // Return the maximum of ans1 and ans2
        return Math.max(ans1, ans2);
    }
Time Complexity: O(N)+O(N)
Space Complexity:O(N)+O(N)+O(N)+O(N),
```

```java
 // Function to solve the problem using memoization
    private int func(int[] nums) {
        int n = nums.length;
        int prev = nums[0];
        int prev2 = 0;
 
        for (int i = 1; i < n; i++) {
            // Maximum sum if we pick current element
            int pick = nums[i];
            
            if (i > 1) {
                // Add the maximum sum two elements ago
                pick += prev2;
            }
            // Maximum sum if we don't pick current element
            int nonPick = 0 + prev;
 
            // Maximum at the current element
            int cur_i = Math.max(pick, nonPick);
 
            prev2 = prev;
            prev = cur_i;
        }
        // Return the maximum sum
        return prev;
    }
 
    // Function to find the maximum money robber can rob
    public int houseRobber(int[] money) {
        int n = money.length;
        if (n == 0)
            return 0;
        if (n == 1)
            return money[0];
 
        int[] arr1 = new int[n - 1];
        int[] arr2 = new int[n - 1];
 
        // Populate arr1 and arr2
        for (int i = 0; i < n; i++) {
            if (i != n - 1)
                arr1[i] = money[i];
            if (i != 0)
                arr2[i - 1] = money[i];
        }
        int ans1 = func(arr1);
 
        int ans2 = func(arr2);
 
        // Return the maximum of ans1 and ans2
        return Math.max(ans1, ans2);
    }
Time Complexity: O(N)+O(N)
Space Complexity:O(N)+O(N),
```
