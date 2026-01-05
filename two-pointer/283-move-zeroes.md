# 283. Move Zeroes

## 📘 Problem Statement
Given an integer array `nums`, move all `0`s to the **end of the array** while maintaining the **relative order of the non-zero elements**.

You must do this **in-place** without making a copy of the array.

---

## 🧠 Brute Force Approach

### 🔹 Idea
Create a new array. First copy all non-zero elements, then fill the remaining positions with zeroes, and finally copy the result back to the original array.

### 🔹 Algorithm
1. Create a new array of same length
2. Copy all non-zero elements into it
3. Fill remaining positions with `0`
4. Copy the new array back to `nums`

### ⏱ Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

### 💻 Java Code (Brute Force)
```java
class Solution {
    public void moveZeroes(int[] nums) {
        int[] temp = new int[nums.length];
        int index = 0;

        for (int num : nums) {
            if (num != 0) {
                temp[index++] = num;
            }
        }

        for (int i = 0; i < nums.length; i++) {
            nums[i] = temp[i];
        }
    }
}
````

---

## 🧠 Better Approach (Two Pass – Count Non-Zero)

### 🔹 Idea

Move all non-zero elements to the front in the first pass.
Fill the remaining positions with zeroes in the second pass.

### 🔹 Algorithm

1. Traverse array and place non-zero elements at the front
2. Fill remaining indices with `0`

### ⏱ Complexity

* **Time Complexity:** O(n)
* **Space Complexity:** O(1)

### 💻 Java Code (Better Approach)

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int index = 0;

        // First pass: move non-zero elements forward
        for (int num : nums) {
            if (num != 0) {
                nums[index++] = num;
            }
        }

        // Second pass: fill remaining with zeroes
        while (index < nums.length) {
            nums[index++] = 0;
        }
    }
}
```

---

## 🧠 Optimal Approach ✅ (Two Pointer – Swap)

### 🔹 Idea

Use two pointers:

* `slow` points to position where next non-zero element should go
* `fast` scans the array

Whenever a non-zero is found, swap it with `slow`.

### 🔹 Algorithm

1. Initialize `slow = 0`
2. Traverse array with `fast`
3. If `nums[fast] != 0`, swap with `nums[slow]` and increment `slow`

### ⏱ Complexity

* **Time Complexity:** O(n)
* **Space Complexity:** O(1)

### 💻 Java Code (Optimal Solution)

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int slow = 0;

        for (int fast = 0; fast < nums.length; fast++) {
            if (nums[fast] != 0) {
                int temp = nums[slow];
                nums[slow] = nums[fast];
                nums[fast] = temp;
                slow++;
            }
        }
    }
}
```

