# 167. Two Sum II – Input Array Is Sorted

## 📘 Problem Statement
You are given a **1-indexed** array of integers `numbers` that is already sorted in non-decreasing order.
Find two numbers such that they add up to a specific `target`.

Return the indices of the two numbers (1-based indexing) such that:
- `numbers[i] + numbers[j] == target`
- `i < j`

Exactly one solution exists.

---

## 🧠 Brute Force Approach

### 🔹 Idea
Check every possible pair of elements using two nested loops and return the pair whose sum equals the target.

### 🔹 Algorithm
1. Loop through the array using index `i`
2. For each `i`, loop through remaining elements using index `j`
3. If `numbers[i] + numbers[j] == target`, return indices

### ⏱ Complexity
- **Time Complexity:** O(n²)
- **Space Complexity:** O(1)

---

## 🧠 Better Approach (HashMap)

### 🔹 Idea
Use a HashMap to store previously visited elements and check if the complement
`(target - current element)` already exists.

> Note: This approach does **not use the sorted property**, but improves time complexity.

### 🔹 Algorithm
1. Create a HashMap to store number → index
2. Iterate through the array
3. For each element:
   - Calculate `complement = target - current element`
   - If complement exists in map, return indices
   - Otherwise, store current element in map

### ⏱ Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

---

## 🧠 Optimal Approach ✅ (Two Pointer)

### 🔹 Idea
Since the array is sorted, use two pointers:
- One starting from the beginning
- One starting from the end

Move pointers based on comparison of current sum with target.

### 🔹 Algorithm
1. Initialize `left = 0` and `right = n - 1`
2. While `left < right`:
   - Calculate sum of `numbers[left] + numbers[right]`
   - If sum equals target, return indices
   - If sum is less than target, increment `left`
   - If sum is greater than target, decrement `right`

### ⏱ Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(1)

---

## 💻 Java Code (Optimal Solution)

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length - 1;

        while (left < right) {
            int sum = numbers[left] + numbers[right];

            if (sum == target) {
                return new int[]{left + 1, right + 1};
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
        return new int[]{};
    }
}
