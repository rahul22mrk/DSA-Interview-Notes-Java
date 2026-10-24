# Priority 2: Arrays + Two Pointers + Sliding Window
Reported array rotation aur sliding-window maximum ko dekhte hue yeh group important hai.

## Questions:
```
1. Rotate Array
2. Sliding Window Maximum
3. Two Sum
4. Maximum Subarray
5. Move Zeroes
6. Best Time to Buy and Sell Stock
```

```   
Resources:
- LeetCode — Array problems
- LeetCode 239 — Sliding Window Maximum
```

1. Rotate Array
```
https://takeuforward.org/practice/dsa/left-rotate-array
```

```java
class Solution {
    public void rotateArray(int[] nums, int k) {
        int n = nums.length;
        k = k % n;
        int temp[] = new int[k];

        for(int i = 0; i<k; i++){
            temp[i] = nums[i];
        }

        for(int i=k; i<nums.length; i++){
            nums[i-k] = nums[i];
        }

        for(int i=0; i<k; i++){
            nums[n-k+i] = temp[i];
        }
    }
}
Time Complexity: O(N)
Space Complexity: O(K)
```

```java
class Solution {
    public void rotateArray(int[] nums, int k) {
        int n = nums.length;
        k = k % n;

        reverse(nums, 0, k-1);
        reverse(nums, k, n-1);
        reverse(nums, 0, n-1);
        
    }

    private void reverse(int[] nums, int start, int end){
        while(start<end){
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
Time Complexity: O(N)
Space Complexity: O(1)
```

1.2. Find out how many times the array is rotated
```
https://takeuforward.org/practice/dsa/find-out-how-many-times-the-array-is-rotated
```

```java
 /* Function to find the number of
       rotations in a rotated sorted array */
    public int findKRotation(ArrayList<Integer> nums) {
        // Get the size of the array
        int n = nums.size();
        
        /* Initialize variables to store
           minimum value and its index */
        int ans = Integer.MAX_VALUE, index = -1;
        
        /* Iterate through the array to
           find the smallest element */
        for (int i = 0; i < n; i++) {
            if (nums.get(i) < ans) {
                ans = nums.get(i);  // Update minimum value
                index = i;          // Update index of minimum value
            }
        }
        // Return the index of smallest element
        return index;
    }
Time Complexity:O(N), where N is size of the array. As the array is being traversed only once using a single loop.

Space Complexity: As no additional space is used, so the Space Complexity is O(1).
```

```java
/* Function to find the number of
       rotations in a rotated sorted array */
    public int findKRotation(ArrayList<Integer> nums) {
        int low = 0, high = nums.size() - 1;
        int ans = Integer.MAX_VALUE;
        int index = -1;
        while (low <= high) {
            int mid = (low + high) / 2;
            
            /* Search space is already sorted
               then nums.get(low) will always be
               the minimum in that search space */
            if (nums.get(low) <= nums.get(high)) {
                if (nums.get(low) < ans) {
                    index = low;
                    ans = nums.get(low);
                }
                break;
            }
            
            // If left part is sorted update the ans
            if (nums.get(low) <= nums.get(mid)) {
                if (nums.get(low) < ans) {
                    index = low;
                    ans = nums.get(low);
                }
                // Eliminate left half
                low = mid + 1;
            } else {
                /* update the ans if it 
                   is less than nums.get(mid) */
                if (nums.get(mid) < ans) {
                    index = mid;
                    ans = nums.get(mid);
                }
                // Eliminate right half
                high = mid - 1;
            }
        }
        // Return the index as answer
        return index;
    }
Time Complexity:O(logN), where N is size of the array. As binary search algorithm is being applied to solve the problem.

Space Complexity: As no additional space is used, so the Space Complexity is O(1).
```



2. Sliding Window Maximum
```

```

```java

```

```java

```

```java

```


3. Two Sum
```
https://takeuforward.org/practice/dsa/two-sum
https://leetcode.com/problems/two-sum/description/
```

```java
//My Solution
```

```java
//Brute Force:
public int[] twoSum(int[] nums, int target) {
        
        int n = nums.length;
        //create ans array to store ans
        int[] ans = new int[2];
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                
                /* if nums[i] + nums[j] is equal to 
                   target put i and j in ans */
                if (nums[i] + nums[j] == target) {
                    ans[0] = i;
                    ans[1] = j;
                    return ans;
                }
                
            }
        }
        
        // Return {-1, -1} if no such pair is found
        return new int[]{-1, -1};
    }
Time Complexity:O(N 2), For using two nested loops to traverse the array, where N is the length of that array.

Space Complexity: O(1), not using extra space.    
```

```java
//Better
public int[] twoSum(int[] nums, int target) {
        
        // Map to store (element, index) pairs
        Map<Integer, Integer> mpp = new HashMap<>();
        
        // Size of the nums array
        int n = nums.length;
        
        for (int i = 0; i < n; i++) {
            // Current number in the array
            int num = nums[i];
            
            // Number needed to reach the target
            int moreNeeded = target - num;
 
            // Check if the complement exists in map
            if (mpp.containsKey(moreNeeded)) {
                /* Return the indices of the two
                numbers that sum up to target*/
                return new int[]{mpp.get(moreNeeded), i};
            }
 
            // Store current number and its index in map
            mpp.put(nums[i], i);
        }
 
        // If no such pair found, return {-1, -1}
        return new int[]{-1, -1};
    }
    Time Complexity:O(N), 
    Space Complexity: O(N)
```

```java
//Optimal
/* Function to find two indices in the array `nums`
       such that their elements sum up to `target`.
    */
    public int[] twoSum(int[] nums, int target) {
        // Size of the nums array
        int n = nums.length;
        
        // Array to store indices of two numbers
        int[] ans = new int[2];
        
        // 2D array to store {element, index} pairs
        int[][] eleIndex = new int[n][2];
        for (int i = 0; i < nums.length; i++) {
            eleIndex[i][0] = nums[i];
            eleIndex[i][1] = i;
        }
        
        /* Sort eleIndex by the first
        element in ascending order*/
        Arrays.sort(eleIndex, (a, b) -> Integer.compare(a[0], b[0]));
 
        /* Two pointers: one starting 
        from left and one from right*/
        int left = 0, right = n - 1;
 
        while (left < right) {
            /* Calculate sum of elements at
            left and right pointers*/
            int sum = eleIndex[left][0] + eleIndex[right][0];
 
            if (sum == target) {
                
                /* If sum equals target, 
                store indices and return*/
                ans[0] = eleIndex[left][1];
                ans[1] = eleIndex[right][1];
                return ans;
                
            } else if (sum < target) {
                
                /* If sum is less than target,
                move left pointer to the right*/
                left++;
                
            } else {
                
                /* If sum is greater than target,
                move right pointer to the left*/
                right--;
                
            }
        }
 
        // If no such pair found, return {-1, -1}
        return new int[]{-1, -1};
    }
}
Time Complexity: O(N) + O(N*logN),
Space Complexity: O(N), 
```

4. Maximum Subarray
```

```

```java

```

```java

```

```java

```


5. Move Zeroes
```
https://leetcode.com/problems/move-zeroes/
https://takeuforward.org/practice/dsa/move-zeros-to-end
```

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int zeroPtr = -1;
        int mvPtr = 0;

        while(mvPtr < nums.length){
            if(nums[mvPtr] == 0){
                if(zeroPtr == -1){
                    zeroPtr = mvPtr;
                }
            }else{
                if(zeroPtr!=-1){
                     swap(nums, zeroPtr++, mvPtr);
                }
            }
            mvPtr++;
        }
    }

    private void swap(int nums[], int i, int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

```java
//Brute:
public void moveZeroes(int[] nums) {
        int n = nums.length;
 
        // Create a temporary array to store non-zero elements
        int[] temp = new int[n];
        int count = 0;
 
        // Copy non-zero elements to temp
        for (int i = 0; i < n; i++) {
            if (nums[i] != 0) {
                temp[count++] = nums[i];
            }
        }
 
        // Copy non-zero elements back to nums
        for (int i = 0; i < count; i++) {
            nums[i] = temp[i];
        }
 
        // Fill the rest with zeroes
        for (int i = count; i < n; i++) {
            nums[i] = 0;
        }
    }
Time Complexity: O(2*N)
Space Complexity: O(N)
```

```java
//Optimal Approach:
public void moveZeroes(int[] nums) {
        // j keeps track of where the next non-zero should be placed
        int j = 0;
 
        // Loop through all elements
        for (int i = 0; i < nums.length; i++) {
            // If current element is non-zero
            if (nums[i] != 0) {
                // Swap current element with the one at index j
                int temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
 
                // Move j forward
                j++;
            }
        }
    }
Time Complexity: O(N), where N is size of the array, as we are traversing the array once.

Space Complexity: O(1) , as no use of any extra space is done to solve this problem.
```


6. Best Time to Buy and Sell Stock
```

```

```java

```

```java

```

```java

```

