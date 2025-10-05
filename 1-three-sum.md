---
difficulty: Medium
tags: [Array, Hash Table, Two Pointers]
category: Arrays
leetcode: 15
companies: [Google, Amazon, Facebook]
---

# 3Sum

## Problem Statement
Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

**Example:**Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]

## Initial Thoughts
- Brute force: O(n³) - try all combinations
- Better: Sort + two pointers = O(n²)
- Edge cases: duplicates, empty array

## Solution Approach

### Strategy
1. Sort the array
2. Fix first element, use two pointers for remaining
3. Skip duplicates to avoid repeated triplets

### Step-by-Step
1. Sort array: `[-4, -1, -1, 0, 1, 2]`
2. For each element `i`:
   - Set `left = i+1`, `right = len-1`
   - Find pairs that sum to `-nums[i]`
3. Move pointers based on sum

## Code

### Python Solution
```pythondef threeSum(nums):
nums.sort()
result = []for i in range(len(nums) - 2):
    # Skip duplicates for first element
    if i > 0 and nums[i] == nums[i-1]:
        continue    left, right = i + 1, len(nums) - 1    while left < right:
        total = nums[i] + nums[left] + nums[right]        if total < 0:
            left += 1
        elif total > 0:
            right -= 1
        else:
            result.append([nums[i], nums[left], nums[right]])            # Skip duplicates for second element
            while left < right and nums[left] == nums[left+1]:
                left += 1
            # Skip duplicates for third element
            while left < right and nums[right] == nums[right-1]:
                right -= 1            left += 1
            right -= 1return result

### JavaScript Solution
```javascriptfunction threeSum(nums) {
nums.sort((a, b) => a - b);
const result = [];for (let i = 0; i < nums.length - 2; i++) {
    if (i > 0 && nums[i] === nums[i-1]) continue;    let left = i + 1, right = nums.length - 1;    while (left < right) {
        const sum = nums[i] + nums[left] + nums[right];        if (sum < 0) left++;
        else if (sum > 0) right--;
        else {
            result.push([nums[i], nums[left], nums[right]]);
            while (left < right && nums[left] === nums[left+1]) left++;
            while (left < right && nums[right] === nums[right-1]) right--;
            left++;
            right--;
        }
    }
}return result;
}

## Complexity Analysis
- **Time Complexity:** O(n²)
  - Sorting: O(n log n)
  - Nested loops: O(n²)
  - Overall: O(n²)
  
- **Space Complexity:** O(1)
  - Not counting output array
  - Only using pointers

## Edge Cases
- Empty array → `[]`
- All positive/negative → `[]`
- Duplicates → Handle with skip logic
- Array length < 3 → `[]`

## Key Insights & Patterns
- ⭐ **Two pointers** after fixing one element
- ⭐ **Skip duplicates** to avoid repeated results
- ⭐ **Sort first** to enable two-pointer approach
- Pattern: "Find triplets/quadruplets" → Fix + two pointers

## Common Mistakes
- ❌ Forgetting to skip duplicates
- ❌ Not sorting the array first
- ❌ Off-by-one errors with pointers
- ❌ Modifying while iterating without careful indexing

## Follow-up Questions
- What if we need 4Sum? → Same pattern, add one more loop
- What if no sorting allowed? → Use hash map (more complex)
- What if numbers are very large? → Consider overflow

## Related Problems
- [1. Two Sum](1-two-sum.md)
- [18. 4Sum](18-4sum.md)
- [16. 3Sum Closest](16-3sum-closest.md)

## Practice Notes
**First Attempt:** 2024-10-05
- Took 25 minutes
- Forgot to skip duplicates initially
- Remember: ALWAYS skip duplicates after sorting!

**Review 1:** 2024-10-12
- Solved in 15 minutes
- Much smoother, pattern clicked