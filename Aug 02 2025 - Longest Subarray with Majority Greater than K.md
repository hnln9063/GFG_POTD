### Longest Subarray with Majority Greater than K

Given an array **arr[]** and an integer **k**, the task is to find the length of the **longest subarray** in which the **count** of elements **greater than k** is **more** than the count of elements **less than or equal to k**.

## Examples:
```
Input: arr[] = [1, 2, 3, 4, 1], k = 2
Output: 3
Explanation: The subarray [2, 3, 4] or [3, 4, 1] satisfy the given condition, and there is no subarray of length 4 or 5 which will hold the given condition, so the answer is 3.
```
```
Input: arr[] = [6, 5, 3, 4], k = 2
Output: 4
Explanation: In the subarray [6, 5, 3, 4], there are 4 elements > 2 and 0 elements <= 2, so it is the longest subarray.
```

## Approach

To solve this problem efficiently, we utilize prefix sums and a hashmap to store the first occurrence of specific prefix sums. Here’s the step-by-step explanation:

1. **Transform the Array:**  
   Convert each element of the array to:
   - `1` if the element is **greater than k**,
   - `-1` otherwise (i.e., element is **less than or equal to k**).

   This transformation allows us to reduce the problem to finding the longest subarray whose sum is **greater than zero**.

2. **Prefix Sum Concept:**  
   Calculate the running sum (prefix sum) as we iterate over the array.  
   - If the prefix sum is **greater than 0** at any index `i`, it means from the start to `i` there are more elements greater than `k` than less than or equal to `k`.  
   - The length of such subarray is `i + 1`.

3. **Hashmap for Prefix Indices:**  
   Use a hashmap to store the **first occurrence** of every unique prefix sum.  
   - If we encounter a prefix sum of `currentSum - 1` before, it means there's a subarray between those indices with sum greater than zero.
   - The length of such subarray is `i - previousIndex`.

4. **Iterative Computation:**  
   - At each step, update the prefix sum and check if the new prefix sum or its required value for a longer subarray already exists in the hashmap.

5. **Answer Construction:**  
   - The answer is the maximum length found following these rules.

**Example:**

Let’s consider  
**Input:** `arr[] = [1, 2, 3, 4, 1], k = 2`

- After transformation:  
  `[ -1, -1, 1, 1, -1 ]`  (since only 3 and 4 are > 2)
- Calculate prefix sums:  
  `-1, -2, -1, 0, -1`
- Store first occurrence of each prefix sum in hashmap:
  - `0` at index `-1` (initialize for subarrays starting from index 0)
- Iterate and keep updating/checking as per the outlined logic.

The solution finds subarrays like `[2, 3, 4]` and `[3, 4, 1]` both of length `3`, which is the answer.

## Java Solution
```java
class Solution {
    public int longestSubarray(int[] arr, int k) {
        int n = arr.length;
        // Convert the array into +1 for >k and -1 for <=k
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = arr[i] > k ? 1 : -1;
        }

        // Use a map to store the first occurrence of a prefix sum
        HashMap<Integer, Integer> prefixMap = new HashMap<>();
        int maxLen = 0, prefixSum = 0;
        
        prefixMap.put(0, -1); // Initial prefix sum of 0 at index -1

        for (int i = 0; i < n; i++) {
            prefixSum += nums[i];
            // If prefixSum > 0, from 0 to i has majority >k
            if (prefixSum > 0) {
                maxLen = i + 1;
            } else {
                // Try to find if (prefixSum - 1) occurred before
                if (prefixMap.containsKey(prefixSum - 1)) {
                    int prevIdx = prefixMap.get(prefixSum - 1);
                    maxLen = Math.max(maxLen, i - prevIdx);
                }
            }
            // Record the first occurrence of each prefixSum
            prefixMap.putIfAbsent(prefixSum, i);
        }
        return maxLen;
    }
}
```

## Problem Link
<a>https://www.geeksforgeeks.org/problems/longest-subarray-with-majority-greater-than-k/1</a>
