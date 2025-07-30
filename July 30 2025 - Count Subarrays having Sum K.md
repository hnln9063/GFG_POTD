### Count Subarrays having Sum k

Given an unsorted array **arr[]** of integers, find the **number of subarrays** whose **sum** exactly equal to a given number **k**.


**Examples:**
```
Input: arr[] = [10, 2, -2, -20, 10], k = -10
Output: 3
Explaination: Subarrays: arr[0...3], arr[1...4], arr[3...4] have sum exactly equal to -10.
```
```
Input: arr[] = [9, 4, 20, 3, 10, 5], k = 33
Output: 2
Explaination: Subarrays: arr[0...2], arr[2...4] have sum exactly equal to 33.
```
```
Input: arr[] = [1, 3, 5], k = 0
Output: 0
Explaination: No subarray with 0 sum.
```
## Expected Approach
To count subarrays with sum k, we use a hash map to store the frequency of prefix sums. <br>
At each index, we calculate the current prefix sum currSum and check if (currSum - k) exists in the map. <br>
If it does, it means there are subarrays ending at the current index with sum k, and we add their count to the result. <br>
Then we update the frequency of currSum in the map.

## Java Solution
```java
class Solution {
    public int cntSubarrays(int arr[], int k) {
        // code here
        Map<Integer, Integer> prefixSum = new HashMap<>();
        int res = 0;
        int currSum = 0;

        for (int i = 0; i < arr.length; i++) {
            
            // Add current element to sum
            currSum += arr[i];
            
            // Found one subarray which is equal to k
            if (currSum == k)
                res++;
                
            // Check if currenetSum - k exist 
            if (prefixSum.containsKey(currSum - k))
                res += prefixSum.get(currSum - k);
            
            // Add current sum to hashmap
            if(prefixSum.containsKey(currSum)) {
                prefixSum.put(currSum, prefixSum.get(currSum)+1);
            } else {
                prefixSum.put(currSum, 1);
            }
        }

        return res;
    }
}
```
## Problem Link
<a>https://www.geeksforgeeks.org/problems/subarrays-with-sum-k/1</a>
