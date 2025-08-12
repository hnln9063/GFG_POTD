### Shop in Candy Store
In a candy store, there are different types of candies available and prices[i] represent the price of  ith types of candies. You are now provided with an attractive offer.
For every candy you buy from the store, you can get up to k other different candies for free. Find the minimum and maximum amount of money needed to buy all the candies.
Note: In both cases, you must take the maximum number of free candies possible during each purchase.

## Examples:
```
Input: prices[] = [3, 2, 1, 4], k = 2
Output: [3, 7]
Explanation: As according to the offer if you buy one candy you can take at most k more for free. So in the first case, you buy the candy worth 1 and takes candies worth 3 and 4 for free, also you need to buy candy worth 2. So min cost: 1+2 = 3. In the second case, you can buy the candy worth 4 and takes candies worth 1 and 2 for free, also you need to buy candy worth 3. So max cost: 3+4 = 7.
```
```
Input: prices[] = [3, 2, 1, 4, 5], k = 4
Output: [1, 5]
Explanation: For minimimum cost buy the candy with the cost 1 and get all the other candies for free. For maximum cost buy the candy with the cost 5 and get all other candies for free.
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
    public ArrayList<Integer> minMaxCandy(int[] prices, int k) {
        ArrayList<Integer> result = new ArrayList<>();
        int n = prices.length;
        
        // Sort the prices array
        Arrays.sort(prices);
        
        // Calculate minimum cost
        // Buy cheapest candies, get expensive ones free
        int minCost = 0;
        int left = 0;
        int right = n - 1;
        
        while (left <= right) {
            minCost += prices[left];
            left++;
            // Skip k candies from the right (expensive ones - get them free)
            right -= k;
        }
        
        // Calculate maximum cost
        // Buy expensive candies, get cheap ones free
        int maxCost = 0;
        left = 0;
        right = n - 1;
        
        while (left <= right) {
            maxCost += prices[right];
            right--;
            // Skip k candies from the left (cheap ones - get them free)
            left += k;
        }
        
        result.add(minCost);
        result.add(maxCost);
        
        return result;
    }
}
```

## Problem Link
<a>https://www.geeksforgeeks.org/problems/shop-in-candy-store1145/1</a>
