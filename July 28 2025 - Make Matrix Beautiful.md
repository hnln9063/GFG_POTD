### Make Matrix Beautiful 

A **beautiful matrix** is defined as a square matrix in which the **sum** of elements in every row and every column is equal. Given a square matrix **mat[][]**, your task is to determine the **minimum number of operations** required to make the matrix beautiful.
In one operation, you are allowed to increment the value of any single cell by 1.

**Examples:**
```
Input: mat[][] = [[1, 2], 
                [3, 4]]
Output: 4
Explanation:
Increment value of cell(0, 0) by 3, 
Increment value of cell(0, 1) by 1. 
Matrix after the operations: [[4, 3], 
                            [3, 4]]
Here, sum of each row and column is 7.
Hence total 4 operation are required.
```
```
Input: mat[][] = [[1, 2, 3],
                [4, 2, 3],
                [3, 2, 1]]
Output: 6
Explanation: 
Increment value of cell(0, 0) by 1, 
Increment value of cell(0, 1) by 2, 
Increment value of cell(2, 1) by 1, 
Increment value of cell(2, 2) by 2. 
Matrix after the operations: [[2, 4, 3], 
                            [4, 2, 3],
                            [3, 3, 3]] 
Here, sum of each row and column is 9.
Hence total 6 operation are required.
```
## Expected Approach
The idea is to equalize all row and column sums, <br>
so for that we will first compute: **maxSum = max(maxRowSum, maxColSum)**. <br>
We aim to make every row and column sum equal to maxSum. To do this, we increment elements only in rows and columns that fall short of maxSum, ensuring we never exceed maxSum for any row or column. Each increment at a cell (i, j) contributes to both the row and column sums.

- minOperations = n × s – totalSum

## Java Solution
```java
class Solution {
    public static int balanceSums(int[][] mat) {
        // code here
        
        /*
        The idea is to equalize all row and column sums, 
        so for that we will first compute: maxSum = max(maxRowSum, maxColSum).
        
        We aim to make every row and column sum equal to maxSum. To do this, 
        we increment elements only in rows and columns that fall short of maxSum, 
        ensuring we never exceed maxSum for any row or column. 
        Each increment at a cell (i, j) contributes to both the row and column sums.
        */
        int n = mat.length;
        int colSum[] = new int[n];
        int rowSum[] = new int[n];
        int maxRow = 0;
        int maxCol = 0;
        int curSum = 0;
        
        for(int i=0;i<n;i++) {
            for(int j=0;j<mat[i].length;j++) {
                colSum[j] = colSum[j] + mat[i][j];
                rowSum[i] = rowSum[i] + mat[i][j];
                curSum = curSum + mat[i][j];
            }
        }
        
        for(int i=0;i<mat.length;i++) {
            maxRow = Math.max(maxRow, rowSum[i]);
            maxCol = Math.max(maxCol, colSum[i]);
        }
        
        int maxSum = Math.max(maxCol, maxRow);
        
        return (maxSum*mat.length) - curSum;
    }
}
```



