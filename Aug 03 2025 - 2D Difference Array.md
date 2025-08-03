### 2D Difference Array
You are given a 2D integer matrix mat[][] of size n × m and a list of q operations opr[][]. Each operation is represented as an array [v, r1, c1, r2, c2], where:

- v is the value to be added
- (r1, c1) is the top-left cell of a submatrix
- (r2, c2) is the bottom-right cell of the submatrix (inclusive)
For each of the q operations, add v to every element in the submatrix from (r1, c1) to (r2, c2). Return the final matrix after applying all operations.

## Examples:
```
Input: mat[][] = [[1, 2, 3],  opr[][] = [[2, 0, 0, 1, 1], [-1, 1, 0, 2, 2]]
                [1, 1, 0],
                [4,-2, 2]]
Output: [[3, 4, 3],
        [2, 2, -1],
        [3, -3, 1]] 
```

## Java Solution
```java
class Solution {
    public ArrayList<ArrayList<Integer>> applyDiff2D(int[][] mat, int[][] opr) {
        int n = mat.length;
        int m = mat[0].length;
        int[][] diff = new int[n + 2][m + 2]; // extend size to avoid bounds issues
        
        // Step 1: Apply each operation to diff
        for (int[] op : opr) {
            int v = op[0], r1 = op[1], c1 = op[2], r2 = op[3], c2 = op[4];
            diff[r1][c1] += v;
            if (c2 + 1 < m)
                diff[r1][c2 + 1] -= v;
            if (r2 + 1 < n)
                diff[r2 + 1][c1] -= v;
            if (r2 + 1 < n && c2 + 1 < m)
                diff[r2 + 1][c2 + 1] += v;
        }
        
        // Step 2: Row-wise prefix sum
        for (int i = 0; i < n; i++)
            for (int j = 1; j < m; j++)
                diff[i][j] += diff[i][j - 1];
        
        // Step 3: Column-wise prefix sum
        for (int j = 0; j < m; j++)
            for (int i = 1; i < n; i++)
                diff[i][j] += diff[i - 1][j];
        
        // Step 4: Add diff to mat and build result
        ArrayList<ArrayList<Integer>> result = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            ArrayList<Integer> row = new ArrayList<>();
            for (int j = 0; j < m; j++) {
                row.add(mat[i][j] + diff[i][j]);
            }
            result.add(row);
        }
        return result;
    }
}
```

## Problem Link
<a>https://www.geeksforgeeks.org/problems/2-d-difference-array/1</a>
