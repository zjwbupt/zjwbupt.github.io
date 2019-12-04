### Description
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).

Example 1:

Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
Example 2:

Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1

### Idea
1. We need to search in a sorted array, since it is sorted, so we could use binary search
2. the mid can be in two different situations
(1) start -- MID -- Higest or (2) Lowest -- MID -- End
3. for situation (1), the target could be in one of two situations: target in [start, mid] or Other.
if target is in [start, mid], we do binary search in this part, otherwise, transfer it into a sub SEARCH_IN_ROTATED_ARRAY problem. Same idea for situation (2). The target could be in [mid, end], we do binary search in this part. If target is not in [mid, end], we transfer it into another sub-problem.

### Code
```java
public int searchTarget(int[] nums, int target) {
        if (nums == null || nums.length == 0) return -1;

        int start = 0, end = nums.length - 1;

        while (start + 1 < end) {
            int mid = (end - start) / 2 + start;
            if (nums[mid] == target) return mid;

            if (nums[mid] > nums[end]) {
                if (nums[start] <= target && target <= nums[mid]) {
                    end = mid;
                } else
                    start = mid;
            } else {
                if (nums[mid] <= target && target <= nums[end]) {
                    start = mid;
                } else
                    end = mid;
            }
        }

        if (nums[start] == target) return start;
        if (nums[end] == target) return end;
        return -1;
    }
```