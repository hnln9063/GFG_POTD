### Powerful Integer

You are given a 2D integer array intervals[][] of length n, where each intervals[i] = [start, end] represents a closed interval (i.e., all integers from start to end, inclusive). You are also given an integer k. An integer is called Powerful if it appears in at least k intervals. Find the maximum Powerful Integer.

Note: If no integer occurs at least k times return -1.

**Examples:**
```
Input : n = 3, intervals[][] = [[1, 3], [4, 6], [3, 4]], k = 2
Output: 4
Explanation: Integers 3 and 4 appear in 2 intervals. The maximum is 4.
```
```
Input : n = 4, intervals[][] = [[1, 4], [12, 45], [3, 8], [10, 12]], k = 3
Output: -1
Explanation: No integer appears in at least 3 intervals.
```
```
Input : n = 5, intervals[][] = [[16, 21], [5, 8], [12, 17], [17, 29], [9, 24]], k = 3
Output: 21
Explanation: Integers 16, 17, 18, 19, 20 and 21 appear in at least 3 intervals. The maximum is 21.
```
## Expected Approach
The idea is to use the sweep line or difference array technique to efficiently count how many intervals cover each integer, without iterating through every number in every interval.<br>
For each interval, we increment the count at the start point and decrement the count just after the end point. <br>
Then, we traverse the sorted map keys while maintaining a running sum (prefix sum) of the interval overlaps. <br>
If this running count is at least k, we update the answer to the current integer (or one less if the count drops below k). <br>
This allows us to find the maximum powerful integer in an optimized way.<br>

## Java Solution
```java
class Solution {
    /*public int powerfulInteger(int[][] intervals, int k) {
        // code here
        
        // Approach One
        int max = -1;
        HashMap<Integer, Integer> hm = new HashMap<Integer,Integer>();
        for(int i=0;i<intervals.length;i++) {
            int start = intervals[i][0];
            int end = intervals[i][1];
            for(int j=start;j<=end;j++) {
                if(hm.containsKey(j)) {
                    hm.put(j, hm.get(j)+1);
                } else {
                    hm.put(j, 1);
                }
            }
        }
        
        for(Map.Entry<Integer, Integer> e : hm.entrySet()) {
            if(e.getValue() >= k) {
                max = Math.max(e.getKey(), max);
            }
        }
        return max;
        
        // 
    } */
    public int powerfulInteger(int[][] intervals, int k) {
        // code here
        // Using Sweep Line
        TreeMap<Integer, Integer> tm = new TreeMap<Integer, Integer>();
        
        for(int i=0;i<intervals.length;i++) {
            int start = intervals[i][0];
            int end = intervals[i][1];
            
            if(tm.containsKey(start))
                tm.put(start, tm.get(start)+1);
            else 
                tm.put(start, 1);
                
            if(tm.containsKey(end+1))
                tm.put(end+1, tm.get(end+1)-1) ;
            else 
                tm.put(end+1, -1); 
        }
        
        int max = -1;
        int temp = 0;
        
        for(Map.Entry<Integer, Integer> e : tm.entrySet()) {
            if(e.getValue() >= 0) {
                temp = temp + e.getValue();
                if(temp >= k) {
                    max = e.getKey();
                }
            } else {
                if(temp >= k) {
                    max = e.getKey()-1;
                }
                temp = temp + e.getValue();
            }
        }
        
        return max;
        
        
    }
}
```
## Problem Link
<a>https://www.geeksforgeeks.org/problems/powerfull-integer--170647/1</a>
