---
title: Kadane's alghoritm
date: 2023-09-18
---

Alghoritm is used for finding a contiguous subarray with the largest sum in one-dimensional array.

```
function maxSubarraySum(nums) {
  let sum = 0;
  let max = -Infinity;
  for(let i = 0; i < nums.length; i++){
      sum = Math.max(sum + nums[i], nums[i]);
      max = Math.max(sum, max);
  }
  return max;
};
```

Time complexity: O(n)
Space complexity: O(1)
