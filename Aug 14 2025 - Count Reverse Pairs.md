### Count Reverse Pairs
You are given an array arr[] of positive integers, find the count of reverse pairs. A pair of indices (i, j) is said to be a reverse pair if both the following conditions are met:

- 0 ≤ i < j < arr.size()
- arr[i] > 2 * arr[j]

## Examples:
```
Input: arr[] = [3, 2, 4, 5, 1, 20]
Output: 3
Explanation:
The Reverse pairs are 
(0, 4), arr[0] = 3, arr[4] = 1, 3 > 2*1 
(2, 4), arr[2] = 4, arr[4] = 1, 4 > 2*1 
(3, 4), arr[3] = 5, arr[4] = 1, 5 > 2*1 
```
```
Input: arr[] = [5, 4, 3, 2, 2]
Output: 2
Explanation:
The Reverse pairs are
(0, 3), arr[0] = 5, arr[3] = 2, 5 > 2*2
(0, 4), arr[0] = 5, arr[4] = 2, 5 > 2*2
```

## Approach

- Sort the prices array in non-decreasing order.
- Minimum Cost:
  - Use two pointers: left at the start (cheapest), right at the end (costliest).
  - While left ≤ right:
    - Pay prices[left] (buy the cheapest available).
    - Increment left by 1.
    - Decrement right by k (take up to k most expensive remaining for free).
- Maximum Cost:
  - Reset pointers: left at start, right at end.
  - While left ≤ right:
    - Pay prices[right] (buy the most expensive available).
    - Decrement right by 1.
    - Increment left by k (take up to k cheapest remaining for free).
- Return [minCost, maxCost].

## Java Solution
```java

class Solution {
    public int countRevPairs(int[] arr) {
        return mergeSort(arr, 0, arr.length - 1);
    }
    
    private int mergeSort(int[] arr, int left, int right) {
        int count = 0;
        if (left < right) {
            int mid = left + (right - left) / 2;
            count += mergeSort(arr, left, mid);
            count += mergeSort(arr, mid + 1, right);
            count += mergeAndCount(arr, left, mid, right);
        }
        return count;
    }
    
    private int mergeAndCount(int[] arr, int left, int mid, int right) {
        // Create temp arrays for left and right subarrays
        int[] leftArr = new int[mid - left + 1];
        int[] rightArr = new int[right - mid];
        
        // Copy data to temp arrays
        for (int i = 0; i < leftArr.length; i++) {
            leftArr[i] = arr[left + i];
        }
        for (int j = 0; j < rightArr.length; j++) {
            rightArr[j] = arr[mid + 1 + j];
        }
        
        int count = 0;
        int i = 0, j = 0;
        
        // Count reverse pairs where arr[i] > 2 * arr[j]
        for (i = 0; i < leftArr.length; i++) {
            while (j < rightArr.length && leftArr[i] > 2L * rightArr[j]) {
                j++;
            }
            count += j;
        }
        
        // Reset pointers for merging
        i = 0;
        j = 0;
        int k = left;
        
        // Merge the temp arrays back into arr[left..right]
        while (i < leftArr.length && j < rightArr.length) {
            if (leftArr[i] <= rightArr[j]) {
                arr[k++] = leftArr[i++];
            } else {
                arr[k++] = rightArr[j++];
            }
        }
        
        // Copy remaining elements
        while (i < leftArr.length) {
            arr[k++] = leftArr[i++];
        }
        while (j < rightArr.length) {
            arr[k++] = rightArr[j++];
        }
        
        return count;
    }
}
```

## Problem Link
<a>https://www.geeksforgeeks.org/problems/count-reverse-pairs/1</a>
