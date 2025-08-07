### Difference Check
Given an array **arr[]** of time strings in 24-hour clock format **"HH:MM:SS"**, return the **minimum difference** in **seconds** between any two time strings in the arr[].
The clock wraps around at midnight, so the time difference between "23:59:59" and "00:00:00" is **1** second.

## Examples:
```
Input: arr[] = ["12:30:15", "12:30:45"]
Output: 30
Explanation: The minimum time difference is 30 seconds.
```
```
Input: arr[] = ["00:00:01", "23:59:59", "00:00:05"]
Output: 2
Explanation: The time difference is minimum between "00:00:01" and "23:59:59".
```

## Approach
- Convert each time string into seconds.
- Sort the list of seconds.
- Calculate the difference between consecutive times.
- For the circular nature check the difference between the last and first time (wraps at midnight).
- Return the minimum difference.

## Java Solution
```java
class Solution {
    public int minDifference(String[] arr) {
        int n = arr.length;
        int[] seconds = new int[n];
        
        // Convert each time to seconds
        for (int i = 0; i < n; i++) {
            String[] parts = arr[i].split(":");
            int h = Integer.parseInt(parts[0]);
            int m = Integer.parseInt(parts[1]);
            int s = Integer.parseInt(parts[2]);
            seconds[i] = h * 3600 + m * 60 + s;
        }
        
        // Sort the array
        Arrays.sort(seconds);
        
        // Compute min difference
        int minDiff = Integer.MAX_VALUE;
        for (int i = 1; i < n; i++) {
            minDiff = Math.min(minDiff, seconds[i] - seconds[i - 1]);
        }
        
        // Check difference across midnight
        int lastDiff = 24*3600 - (seconds[n - 1] - seconds[0]);
        minDiff = Math.min(minDiff, lastDiff);
        
        return minDiff;
    }
}
```

## Problem Link
<a>https://www.geeksforgeeks.org/problems/difference-check/1</a>
