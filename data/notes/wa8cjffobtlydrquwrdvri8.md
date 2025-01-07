
### Leetcode solutions + explanation


### 53.Maximum Subarray 

https://leetcode.com/problems/maximum-subarray/

#### Approach
In order to get the maximum sub array, we keep track of the maximum sum so far and a running sum of the current subarray.

We iterate over the array from the 2nd index, with both current and max sum set to the first value in the array. We need to determine whether we consider the current number as part of this sub array or if we should start a new window. How do we know if continuing this subarray or not is the right choice? We check whether the sum so far PLUS the current number is better than just taking the number itself. This is to cater for the scenario where you have negative numbers in a subarray. Consider the scenario where subarray is either good to continue vs starting new:

a) [4, -1, 8] 

vs

b) [4, -6, 8]

In a) when we get to the number 8, currentSum will equal 3 (4+(-1)). We then check whether currentSum + 8 is better than 8 itself. In this scenario, the sum is better (3+8 > 8) therefore we take the whole array and max sum becomes 11

if we take b), when we get to 8, the current sum is -2 (4+(-6)). If we compare the currentsum + 8 to just 8, it's more beneficial to start a new window (at 8) since (-2 + 8 < 8). Therefore max sum in the second scenario becomes 8.

#### Solution

**Time**: `O(n)`

**Space**: `O(n)`

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function(nums) {
    let maxSum = nums[0];
    let currentSum = nums[0];

    for(let i = 1 ; i < nums.length; i++) {
        currentSum = Math.max(currentSum + nums[i], nums[i]);
        maxSum = Math.max(currentSum, maxSum)
    }

    return maxSum;
};

```