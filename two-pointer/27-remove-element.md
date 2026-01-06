# 27. Remove Element

## 📘 Problem Statement
Given an integer array `nums` and an integer `val`, remove all occurrences of `val` **in-place**.
Return the number of elements in `nums` which are not equal to `val`.

The order of elements **may be changed**.  
Elements beyond the returned length do not matter.

---

## 🧠 Brute Force Approach

### 🔹 Idea
Create a new array, copy all elements that are not equal to `val`, and then copy them back to the original array.

### 🔹 Algorithm
1. Create a new array of same length
2. Copy all elements not equal to `val`
3. Copy them back to `nums`
4. Return count of valid elements

### ⏱ Complexity
- **Time Complexity:** O(n)
- **Space Complexity:** O(n)

### 💻 Java Code (Brute Force)
```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int[] temp = new int[nums.length];
        int index = 0;

        for (int num : nums) {
            if (num != val) {
                temp[index++] = num;
            }
        }

        for (int i = 0; i < index; i++) {
            nums[i] = temp[i];
        }

        return index;
    }
}
````

---

## 🧠 Better Approach (Two Pass)

### 🔹 Idea

Move all elements not equal to `val` to the front in one pass.
No need for swapping.

### 🔹 Algorithm

1. Initialize `index = 0`
2. Traverse the array
3. If element is not equal to `val`, copy it to `nums[index]` and increment `index`
4. Return `index`

### ⏱ Complexity

* **Time Complexity:** O(n)
* **Space Complexity:** O(1)

### 💻 Java Code (Better Approach)

```java
class Solution {
public int removeElement(int[] nums, int val) {
       int j=0;
       for(int i=0; i<nums.length; i++){
        if(nums[i]!=val){
            nums[j++]=nums[i];
         }
       }

       return j;
    }
}
```

---

## 🧠 Optimal Approach ✅ (Two Pointer – Swap with End)

### 🔹 Idea

Use two pointers:

* One pointer iterates through the array
* Another pointer tracks the last valid element

When `val` is found, swap it with the last element.

> Order does not matter, which allows this optimization.

### 🔹 Algorithm

1. Initialize `i = 0`, `n = nums.length`
2. While `i < n`:

   * If `nums[i] == val`, replace it with `nums[n-1]` and decrement `n`
   * Else, increment `i`
3. Return `n`

### ⏱ Complexity

* **Time Complexity:** O(n)
* **Space Complexity:** O(1)

### 💻 Java Code (Optimal Solution)

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int i = 0;
        int n = nums.length;

        while (i < n) {
            if (nums[i] == val) {
                nums[i] = nums[n - 1];
                n--;
            } else {
                i++;
            }
        }
        return n;
    }
}
```
