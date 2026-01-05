# Merge Two Sorted Arrays In-Place 
## Problem Statement

You are given two sorted integer arrays:

- `nums1` of length `m + n`, with the first `m` elements being valid numbers and the last `n` elements as extra space (zeros)

- `nums2` of length `n`, containing `n` numbers

Goal: Merge `nums2` into `nums1` so that `nums1` is fully sorted.

##### Example:
```
Example 1:
nums1 = [1, 3, 5, 0, 0, 0], m = 3
nums2 = [2, 4, 6], n = 3
Output: [1, 2, 3, 4, 5, 6]

Example 2:
nums1 = [0], m = 0
nums2 = [1], n = 1
Output: [1]
  
-> Explanation: The arrays we are merging are [] and [1].
The result of the merge is [1].
Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.

```

## Key Idea

- Start merging **from the end** of nums1 to avoid overwriting numbers.

- Use three pointers:

| Pointer    | Meaning |
| -------- | ------- |
| i | Last valid number in nums1 (index m-1)  |
| j |Last number in nums2 (index n-1)    |
| k   | Last position in nums1 (index m+n-1)   |



- Compare nums1[i] and nums2[j]:

- Place the larger at nums1[k]

- Move the corresponding pointer (i or j) backward

- Move k backward

- After this loop, if any numbers remain in nums2, copy them into the remaining empty slots at the front of nums1.

-> Any remaining numbers in nums1 are already in place.



## Java Solution


```
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {

        int i = m - 1;
        int j = n - 1;
        int k = m + n - 1;

        // Merge from the end
        while (i >= 0 && j >= 0) {
            if (nums1[i] < nums2[j]) {
                nums1[k] = nums2[j];
                j--;
            } else {
                nums1[k] = nums1[i];
                i--;
            }
            k--;
        }

        // Copy any remaining numbers from nums2
        while (j >= 0) {
            nums1[k] = nums2[j];
            j--;
            k--;
        }
    }
}

```

## Complexity


| Type   | Complexity |
| -------- | ------- |
| Time | O(m + n) because Each element in nums1 and nums2 is processed exactly once|
| Space |O(1)	because only 3 integer pointers used (in-place merge)    |



