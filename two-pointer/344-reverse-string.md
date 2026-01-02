# 344. Reverse String

## 📘 Problem Statement
Write a function that reverses a string.  
The input string is given as an array of characters `s`.

You must do this by modifying the input array **in-place** with **O(1) extra memory**.

---

## 🧠 Brute Force Approach

### 🔹 Idea
Create a new array and copy characters from the end of the original array to the beginning of the new array.

### 🔹 Algorithm
1. Create a new character array of same length
2. Traverse the original array from end to start
3. Copy characters into the new array
4. Copy the new array back to the original array

### ⏱ Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 🧠 Better Approach (Stack)

### 🔹 Idea
Use a stack to reverse the characters by pushing all characters and popping them back.

> Note: This approach also uses extra space.

### 🔹 Algorithm
1. Push all characters into a stack
2. Pop characters one by one and put them back into the array

### ⏱ Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 🧠 Optimal Approach ✅ (Two Pointer)

### 🔹 Idea
Use two pointers:
- One pointer at the beginning
- One pointer at the end

Swap characters while moving pointers toward each other.

### 🔹 Algorithm
1. Initialize `left = 0`, `right = s.length - 1`
2. While `left < right`:
   - Swap `s[left]` and `s[right]`
   - Increment `left`
   - Decrement `right`

### ⏱ Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 💻 Java Code (Optimal Solution)

```java
class Solution {
    public void reverseString(char[] s) {
        int left = 0;
        int right = s.length - 1;

        while (left < right) {
            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;

            left++;
            right--;
        }
    }
}
