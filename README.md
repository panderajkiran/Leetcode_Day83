# Leetcode_Day83
# Day 83: Minimum Removals to Balance Array

**LeetCode Problem:** 3634. Minimum Removals to Balance Array  
**Difficulty:** Medium  
**Language:** Java  
**Topics:** Sorting, Binary Search, Two Pointers, Arrays

## Problem Description

You are given an integer array `nums` and an integer `k`.

An array is considered balanced if its maximum element is at most `k` times its minimum element.

You can remove any number of elements without making the array empty.

Return the minimum number of elements to remove so that the remaining array is balanced.

## Approach

### 1. Sort the Array

Sort `nums` in ascending order.

After sorting, the smallest element in a selected range is at the left pointer, and the largest element is at the right pointer.

### 2. Use Binary Search

For every index `i`, consider `nums[i]` as the minimum element of a balanced group.

Calculate the maximum allowed value:

`limit = (long) nums[i] * k`

Use binary search to find the largest index whose value is less than or equal to this limit.

### 3. Find the Largest Balanced Group

Calculate the number of elements in the valid range:

`count = rightmostIndex - i + 1`

Keep track of the maximum number of elements that can remain in the array.

### 4. Calculate Minimum Removals

Subtract the maximum balanced group size from the original array length:

`minimumRemovals = n - maxSum`

This gives the minimum number of elements that must be removed.

## Java Solution

```java
import java.util.Arrays;

class Solution {
    public int minRemoval(int[] nums, int k) {
        Arrays.sort(nums);

        int n = nums.length;
        int maxSum = 1;

        for (int i = 0; i < n; i++) {
            int left = i;
            int right = n - 1;
            int ans = i;

            long limit = (long) nums[i] * k;

            while (left <= right) {
                int mid = left + (right - left) / 2;

                if (nums[mid] <= limit) {
                    ans = mid;
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }

            int count = ans - i + 1;
            maxSum = Math.max(maxSum, count);
        }

        return n - maxSum;
    }
}
```

## Example

**Input:**
```text
nums = [2, 1, 5]
k = 2
```

**Output:**
```text
1
```

**Explanation:**

After sorting, the array becomes `[1, 2, 5]`.

The elements `[1, 2]` form a balanced array because:

`2 <= 1 * 2`

The element `5` cannot be included with `1` or `2` in this group while maintaining the balance condition.

Removing `5` leaves `[1, 2]`, so the minimum number of removals is `1`.

## Complexity Analysis

Let `n` be the length of the array.

**Time Complexity:** `O(n log n)`

- Sorting takes `O(n log n)`.
- Binary search is performed for every element, taking `O(n log n)` overall.

**Space Complexity:** `O(1)` auxiliary space, excluding the space used internally by Java's sorting implementation.

## What I Learned

- Sorting can simplify problems involving minimum and maximum values.
- Binary search helps find the largest valid index efficiently.
- Choosing the largest valid group is the key to minimizing removals.
- Using `long` for multiplication helps prevent integer overflow.

## Takeaway

**Sometimes, the best way to minimize what we lose is to first identify what is worth keeping.**

Day 83 complete! Another Medium problem solved, another step forward in my DSA journey.
