### Roman Number to Integer
Given a string s in Roman number format, your task is to convert it to an integer. Various symbols and their values are given below.
Note: I = 1, V = 5, X = 10, L = 50, C = 100, D = 500, M = 1000

## Examples:
```
Input: s = "IX"
Output: 9
Explanation: IX is a Roman symbol which represents 10 – 1 = 9.
```

```
Input: s = "XL"
Output: 40
Explanation: XL is a Roman symbol which represents 50 – 10 = 40.
```

```
Input: s = "MCMIV"
Output: 1904
Explanation: M is 1000, CM is 1000 – 100 = 900, and IV is 4. So we have total as 1000 + 900 + 4 = 1904.
```

## Java Solution
```java
class Solution {
    // Finds decimal value of a given roman numeral
    public int romanToDecimal(String str) {
        // code here
        HashMap<Character,Integer> hm = new HashMap<Character,Integer>();
        hm.put('I',1);
        hm.put('V',5);
        hm.put('X',10);
        hm.put('L',50);
        hm.put('C',100);
        hm.put('D',500);
        hm.put('M',1000);
        
        int sum = 0;
        for(int i=0;i<str.length()-1;i++) {
            int curr = hm.get(str.charAt(i));
            int next = hm.get(str.charAt(i+1));
            if(curr < next) {
                sum -= curr;
            } else {
                sum += curr;
            }
        }
        return sum+hm.get(str.charAt(str.length()-1));
    }
}
```
**Topic** : Strings, HashMaps

## Problem Link
<a>https://www.geeksforgeeks.org/problems/roman-number-to-integer3201/1</a>
