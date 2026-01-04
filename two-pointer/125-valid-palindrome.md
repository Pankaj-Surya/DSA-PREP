# 125. Valid Palindrome

## 📘 Problem Statement
Given a string `s`, determine if it is a palindrome, considering **only alphanumeric characters** and ignoring **case sensitivity**.

Return `true` if it is a palindrome, otherwise return `false`.

---

## 🧠 Brute Force Approach

### 🔹 Idea
Filter the string to keep only lowercase alphanumeric characters.
Reverse the filtered string and compare it with the original filtered string.

### 🔹 Algorithm
1. Create a new string with only lowercase alphanumeric characters
2. Reverse the string
3. Compare both strings

### ⏱ Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

### 💻 Java Code (Brute Force)
```java
class Solution {
    public boolean isPalindrome(String s) {
        StringBuilder filtered = new StringBuilder();

        for (char c : s.toCharArray()) {
            if (Character.isLetterOrDigit(c)) {
                filtered.append(Character.toLowerCase(c));
            }
        }

        String original = filtered.toString();
        String reversed = filtered.reverse().toString();

        return original.equals(reversed);
    }
}
````

---

## 🧠 Better Approach (Two Strings)

### 🔹 Idea

Instead of reversing one string, build:

* One string from left to right
* One string from right to left
  Compare both strings.

### 🔹 Algorithm

1. Traverse from start and append valid characters to `forward`
2. Traverse from end and append valid characters to `backward`
3. Compare both strings

### ⏱ Complexity

* **Time Complexity:** O(n)
* **Space Complexity:** O(n)

### 💻 Java Code (Better Approach)

```java
class Solution {
    public boolean isPalindrome(String s) {
        StringBuilder forward = new StringBuilder();
        StringBuilder backward = new StringBuilder();

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (Character.isLetterOrDigit(c)) {
                forward.append(Character.toLowerCase(c));
            }
        }

        for (int i = s.length() - 1; i >= 0; i--) {
            char c = s.charAt(i);
            if (Character.isLetterOrDigit(c)) {
                backward.append(Character.toLowerCase(c));
            }
        }

        return forward.toString().equals(backward.toString());
    }
}
```

---

## 🧠 Optimal Approach ✅ (Two Pointer)

### 🔹 Idea

Use two pointers starting from both ends.
Skip non-alphanumeric characters and compare characters ignoring case.

### 🔹 Algorithm

1. Initialize `left = 0`, `right = s.length() - 1`
2. Skip non-alphanumeric characters
3. Compare lowercase characters
4. If mismatch found, return `false`

### ⏱ Complexity

* **Time Complexity:** O(n)
* **Space Complexity:** O(1)

### 💻 Java Code (Optimal Solution)

```java
class Solution {
    public boolean isPalindrome(String s) {
        int left = 0;
        int right = s.length() - 1;

        while (left < right) {

            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }

            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }

            if (Character.toLowerCase(s.charAt(left)) 
                != Character.toLowerCase(s.charAt(right))) {
                return false;
            }

            left++;
            right--;
        }
        return true;
    }
}
```