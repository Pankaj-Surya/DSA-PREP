# 16. 3Sum Closest

## 📘 Problem Statement
Given an integer array `nums` of length `n` and an integer `target`,
find **three integers** in `nums` such that the sum is **closest** to `target`.

Return the **sum** of the three integers.

You may assume that each input would have **exactly one solution**.

---

## 🧠 Brute Force Approach

### 🔹 Idea
Try **all possible triplets** using three nested loops and track the sum
with the minimum absolute difference from the target.

### 🔹 Algorithm
1. Initialize `closestSum` with a very large value
2. Iterate over all triplets `(i, j, k)`
3. Calculate current sum
4. Update `closestSum` if current sum is closer to target

### ⏱ Complexity
- **Time Complexity:** O(n³)
- **Space Complexity:** O(1)

### 💻 Java Code (Brute Force)
```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        int n = nums.length;
        int closestSum = nums[0] + nums[1] + nums[2];

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                for (int k = j + 1; k < n; k++) {
                    int sum = nums[i] + nums[j] + nums[k];

                    if (Math.abs(sum - target) < Math.abs(closestSum - target)) {
                        closestSum = sum;
                    }
                }
            }
        }
        return closestSum;
    }
}
````

---

## 🧠 Better Approach (HashSet Based)

### 🔹 Idea

Fix one element and try to find the closest two-sum using a HashSet.
This is **better conceptually**, but still less efficient than two pointers.

### 🔹 Algorithm

1. Fix index `i`
2. Use HashSet to track visited elements
3. For each `j`, calculate required complement
4. Update closest sum if found value is closer

### ⏱ Complexity

* **Time Complexity:** O(n²)
* **Space Complexity:** O(n)

### 💻 Java Code (Better Approach)

```java
import java.util.*;

class Solution {
    public int threeSumClosest(int[] nums, int target) {
        int closestSum = nums[0] + nums[1] + nums[2];

        for (int i = 0; i < nums.length; i++) {
            Set<Integer> set = new HashSet<>();

            for (int j = i + 1; j < nums.length; j++) {
                int required = target - nums[i] - nums[j];

                if (set.contains(required)) {
                    int sum = nums[i] + nums[j] + required;
                    if (Math.abs(sum - target) < Math.abs(closestSum - target)) {
                        closestSum = sum;
                    }
                }
                set.add(nums[j]);

                int currentSum = nums[i] + nums[j] + required;
                if (Math.abs(currentSum - target) < Math.abs(closestSum - target)) {
                    closestSum = currentSum;
                }
            }
        }
        return closestSum;
    }
}
```

---

## 🧠 Optimal Approach ✅ (Sort + Two Pointer)

### 🔹 Idea

Sort the array.
Fix one element and use **two pointers** to adjust the sum closer to the target.

### 🔹 Algorithm

1. Sort the array
2. Fix index `i`
3. Use `left = i + 1`, `right = n - 1`
4. Update closest sum while adjusting pointers
5. Return closest sum

### ⏱ Complexity

* **Time Complexity:** O(n²)
* **Space Complexity:** O(1)

### 💻 Java Code (Optimal Solution)

```java
import java.util.*;

class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int closestSum = nums[0] + nums[1] + nums[2];

        for (int i = 0; i < nums.length - 2; i++) {
            int left = i + 1;
            int right = nums.length - 1;

            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];

                if (Math.abs(sum - target) < Math.abs(closestSum - target)) {
                    closestSum = sum;
                }

                if (sum < target) {
                    left++;
                } else if (sum > target) {
                    right--;
                } else {
                    return sum; // Exact match
                }
            }
        }
        return closestSum;
    }
}
```
