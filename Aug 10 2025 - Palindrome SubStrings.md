### Palindrome SubStrings
Given a string s, count all palindromic sub-strings present in the string. The length of the palindromic sub-string must be greater than or equal to 2.

Note: A substring is palindromic if it reads the same forwards and backwards.

## Examples:
```
Input: s = "abaab"
Output: 3
Explanation: All palindromic substrings (of length > 1) are: "aba", "aa", "baab".
```
```
Input: s = "aaa"
Output: 3
Explanation: All palindromic substrings (of length > 1) are: "aa", "aa", "aaa".
```
```
Input: s = "abbaeae"
Output: 4
Explanation: All palindromic substrings (of length > 1) are: "bb", "abba", "aea", "eae".
```


## Java Solution
```java
class Solution {
    int countPS(String s) {
        int n = s.length();
        int count = 0;

        // Count odd-length palindromes centered at each index
        for (int i = 0; i < n; i++) {
            int left = i - 1, right = i + 1; // exclude the single-char center (length >= 2)
            while (left >= 0 && right < n && s.charAt(left) == s.charAt(right)) {
                count++;
                left--;
                right++;
            }
        }

        // Count even-length palindromes centered between i and i+1
        for (int i = 0; i + 1 < n; i++) {
            int left = i, right = i + 1;
            while (left >= 0 && right < n && s.charAt(left) == s.charAt(right)) {
                count++;
                left--;
                right++;
            }
        }

        return count;
    }
}
```

## Problem Link
<a>https://www.geeksforgeeks.org/problems/count-palindrome-sub-strings-of-a-string0652/1</a>
