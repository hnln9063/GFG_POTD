### Longest Prefix Suffix
Given a string s, of lowercase english alphabets, find the length of the longest proper prefix which is also a suffix.
Note: Prefix and suffix can be overlapping but they should not be equal to the entire string.

## Examples:
```
Input: s = "abab"
Output: 2
Explanation: The string "ab" is the longest prefix and suffix. 
```
```
Input: s = "aabcdaabc"
Output: 4
Explanation: The string "aabc" is the longest prefix and suffix.
```
```
Input: s = "aaaa"
Output: 3
Explanation: "aaa" is the longest prefix and suffix. 
```

## Approach

- Create an LPS Array:
  For a string of length n, an array lps[] is created, where lps[i] stores the length of the longest prefix which is also a suffix for the substring s[0...i].

- Iterate Over the String:
  You start checking characters from the second character (i=1) because a single character cannot have a proper prefix/suffix.

- Matching Logic:

  - If s[i] == s[len], it means you can extend the current prefix-suffix, so you increase len and set lps[i] = len.
  - If they do not match and len is not zero, you update len to lps[len-1] to try the next best match, without moving i.
  - If len is zero and there is no match, set lps[i]=0 and move to the next character.

- Return the Result:

  - Once this process is complete, lps[n-1] (last element) gives the length of the longest prefix which is also a suffix for the string.
  - We use this value as the answer because a proper prefix-suffix cannot be the whole string itself.

## Java Solution
```java
class Solution {
    int getLPSLength(String s) {
        int n = s.length();
        int[] lps = new int[n];
        int len = 0; // length of the previous longest prefix suffix
    
        int i = 1;
        while (i < n) {
            if (s.charAt(i) == s.charAt(len)) {
                len++;
                lps[i] = len;
                i++;
            } else {
                if (len != 0) {
                    len = lps[len - 1];
                } else {
                    lps[i] = 0;
                    i++;
                }
            }
        }
        // The value at the last index of lps array gives longest prefix-suffix length
        return lps[n - 1];
    }

}
```

## Problem Link
<a>https://www.geeksforgeeks.org/problems/longest-prefix-suffix2527/1</a>
