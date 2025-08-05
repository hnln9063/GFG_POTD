### Palindrome Sentence
Given a single string s, the task is to check if it is a **palindrome sentence** or not.
A palindrome sentence is a sequence of characters, such as word, phrase, or series of symbols that reads the **same** backward as forward after converting all **uppercase** letters to **lowercase** and **removing88 all **non-alphanumeric** characters (including spaces and punctuation).

## Examples:
```
Input: s = "Too hot to hoot"
Output: true
Explanation: If we remove all non-alphanumeric characters and convert all uppercase letters to lowercase, string s will become "toohottohoot" which is a palindrome.
```

```
Input: s = "Abc 012..## 10cbA"
Output: true
Explanation: If we remove all non-alphanumeric characters and convert all uppercase letters to lowercase, string s will become "abc01210cba" which is a palindrome.
```

```
Input: s = "ABC $. def01ASDF"
Output: false
Explanation: The processed string becomes "abcdef01asdf", which is not a palindrome.
```

## Java Solution 1
```java
class Solution {
    public boolean isPalinSent(String s) {
        // code here
        String str = "";
        
        for(int i=0;i<s.length();i++) {
            // Check if a character is alphanumeric
            if(Character.isLetterOrDigit(s.charAt(i))) {
                // Check if it an upper case character.
                //If true, then convert it to lower case. Else append to the result string.
                if(s.charAt(i) >= 'A' && s.charAt(i) <= 'Z') {
                    str += Character.toLowerCase(s.charAt(i));
                } else {
                    str += s.charAt(i);
                }
            }
        }
         // Method to check if a string is palindrome or not
        return checkPalindrome(str);
    }
    
    public static boolean checkPalindrome(String str) {
        int i = 0;
        int j = str.length()-1;
        // Using two pointers, check if first and last characters are equal or not
        while(i <= j) {
            // If first and last characters are not equal then it is not palindrome
            if(str.charAt(i) != str.charAt(j)) {
                return false;
            }
            i++;
            j--;
        }
        return true;
    }
}
```

## Java Solution 2
```java
class Solution {
    // Using two pointers directly 
    public boolean isPalinSent(String s) {
       int i = 0;
       int j = s.length()-1;

        while(i <= j) {
            
            while(i < s.length() && Character.isLetterOrDigit(s.charAt(i)) != true) {
                i++;
            }
            while(j >= 0 && Character.isLetterOrDigit(s.charAt(j)) != true) {
                j--;
            }
            
            if(i <= j) {
                
                char fr = '-';
                char en = '-';
                
                if(Character.isLetter(s.charAt(i))) {
                    fr = Character.toLowerCase(s.charAt(i));
                } else {
                    fr = s.charAt(i);
                }
                
                if(Character.isLetter(s.charAt(j))) {
                    en = Character.toLowerCase(s.charAt(j));
                } else {
                    en = s.charAt(j);
                }
                
                if(fr != en) {
                    return false;
                }
                
            }
            i++;
            j--;
            
        }
        return true;
    }
}
```

**Topic** : Strings, Two Pointers

## Problem Link
<a>https://www.geeksforgeeks.org/problems/string-palindromic-ignoring-spaces4723/1</a>
