### Maximum Sum Rectangle
Given a 2D matrix mat[][] with dimensions n×m. Find the maximum possible sum of any submatrix within the given matrix.

## Examples:
```
Input: mat[][] = [[1, 2, -1, -4, -20], [-8, -3, 4, 2, 1], [3, 8, 10, 1, 3], [-4, -1, 1, 7, -6]]
Output: 29
Explanation: The matrix is as follows and the green rectangle denotes the maximum sum rectangle which is equal to 29.
```

## Approach
- **Reduce the problem to 1D:** For every pair of columns left and right, sum elements between these columns for each row to form a 1D temporary array.
- **Kadane’s Algorithm:** Apply Kadane’s algorithm to this 1D array to find the maximum subarray sum, representing the maximal rectangle for the selected column boundaries.
- **Track the maximum:** Keep updating the global maximum among all such rectangles.

## Java Solution
```java
class Solution {
    int maxRectSum(int[][] mat) {
        int n = mat.length, m = mat[0].length;
        int maxSum = Integer.MIN_VALUE;

        for (int left = 0; left < m; left++) {
            int[] temp = new int[n];
            for (int right = left; right < m; right++) {
                // Add the current column to the row sums
                for (int i = 0; i < n; i++) {
                    temp[i] += mat[i][right];
                }
                // Apply Kadane's algorithm on temp[]
                int sum = 0, localMax = Integer.MIN_VALUE;
                for (int val : temp) {
                    sum = Math.max(val, sum + val);
                    localMax = Math.max(localMax, sum);
                }
                maxSum = Math.max(maxSum, localMax);
            }
        }
        return maxSum;
    }
}

```

## Problem Link
<a>https://www.geeksforgeeks.org/problems/maximum-sum-rectangle2948/1</a>
