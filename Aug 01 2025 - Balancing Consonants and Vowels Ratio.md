### Balancing Consonants and Vowels Ratio

You are given an array of strings arr[], where each arr[i] consists of lowercase english alphabets. You need to find the number of balanced strings in arr[] which can be formed by concatinating one or more contiguous strings of arr[].
A balanced string contains the equal number of vowels and consonants. 

**Examples:**
```
Input: arr[] = ["aeio", "aa", "bc", "ot", "cdbd"]
Output: 4
Explanation: arr[0..4], arr[1..2], arr[1..3], arr[3..3] are the balanced substrings with equal consonants and vowels.
```
```
Input: arr[] = ["ab", "be"]
Output: 3
Explanation: arr[0..0], arr[0..1], arr[1..1] are the balanced substrings with equal consonants and vowels.
```
```
Input: arr[] = ["tz", "gfg", "ae"]
Output: 0
Explanation: There is no such balanced substring present in arr[] with equal consonants and vowels.
```
## Expected Approach
Assign each string a net score: +1 for every vowel and -1 for every consonant. <br>
Compute the prefix sum of these scores across the array. If the same prefix sum appears more than once, the subarray between those indices has equal vowels and consonants. <br>
Use a hash map to count the frequency of each prefix sum during traversal. Add the frequency of the current prefix sum to the result before updating it.

## Java Solution
```java
class Solution {
    
    public static boolean isVowel(char ch) {
        if(ch =='a' || ch =='e' || ch == 'i' || ch == 'o' || ch == 'u') {
            return true;
        }
        return false;
    }
    
    public int countBalanced(String[] arr) {
        // code here
        int prefix = 0;
        int res = 0;
        
        HashMap<Integer, Integer> hm = new HashMap<Integer, Integer>();
        hm.put(0, 1);
        
        for(int i=0;i<arr.length;i++) {
            int val = 0;
            for (int j=0;j<arr[i].length();j++) {
                if (isVowel(arr[i].charAt(j))) 
                    val++;
                else 
                    val--;
            }
            prefix = prefix + val;
            
            res += hm.getOrDefault(prefix, 0);
            hm.put(prefix, hm.getOrDefault(prefix, 0) + 1);
        }
        return res;
    }
}
```
## Problem Link
<a>https://www.geeksforgeeks.org/problems/balancing-consonants-and-vowels-ratio/1</a>
