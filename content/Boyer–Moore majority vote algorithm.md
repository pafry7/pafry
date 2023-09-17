---
title: Boyer-Moore majority vote alghorithm
---

Published in 1981 by Robert S. Boyer and J Strother Moore is used for finding the majority element in a sequence.

```
var majorityElement = function(nums) {
   let counter = 0;
   let candidate;
   for(let i = 0; i < nums.length; i++){
       if(counter === 0){
           candidate = nums[i]
           counter = 1;
       }else if(nums[i] === candidate){
           counter++
       }else{
           counter--
       }
   }
   return candidate;
};
```

If there may be no majority element in the sequence, a second pass is required to verify that the element found in the first pass occurs more than n/2 times, where n is the size of the sequence.

Time complexity: O(n)
Space complexity: O(1)
