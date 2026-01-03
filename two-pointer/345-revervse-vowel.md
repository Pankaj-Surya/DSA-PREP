# 345. Reverse Vowels of a String

## 📘 Problem Statement
Given a string `s`, reverse only the vowels of the string and return the resulting string.

Vowels include: **a, e, i, o, u** (both lowercase and uppercase).

---

## 🧠 Brute Force Approach

### 🔹 Idea
Extract all vowels from the string, reverse them, and then place them back into their original vowel positions.

### 🔹 Algorithm
1. Traverse the string and store all vowels in a list
2. Reverse the list of vowels
3. Traverse the string again and replace vowels with reversed ones

### ⏱ Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 🧠 Better Approach (Stack)

### 🔹 Idea
Use a stack to store vowels. While traversing the string again, pop vowels from the stack and replace them.

### 🔹 Algorithm
1. Traverse the string and push all vowels into a stack
2. Traverse the string again
3. If a vowel is found, replace it with the top of the stack

### ⏱ Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 🧠 Optimal Approach ✅ (Two Pointer)

### 🔹 Idea
Use two pointers:
- One pointer starting from the beginning
- One pointer starting from the end

Move pointers until vowels are found and swap them.

### 🔹 Algorithm
1. Initialize `left = 0`, `right = s.length() - 1`
2. While `left < right`:
   - Move `left` forward until a vowel is found
   - Move `right` backward until a vowel is found
   - Swap characters at `left` and `right`
3. Continue until pointers cross

### ⏱ Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 💻 Java Code (Optimal Solution)

```java
class Solution {
    public String reverseVowels(String s) {
        char[] chars = s.toCharArray();
        int left = 0;
        int right = chars.length - 1;

        while (left < right) {

            while (left < right && !isVowel(chars[left])) {
                left++;
            }

            while (left < right && !isVowel(chars[right])) {
                right--;
            }

            char temp = chars[left];
            chars[left] = chars[right];
            chars[right] = temp;

            left++;
            right--;
        }

        return new String(chars);
    }

    private boolean isVowel(char c) {
        return c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u'
            || c == 'A' || c == 'E' || c == 'I' || c == 'O' || c == 'U';
    }
}
