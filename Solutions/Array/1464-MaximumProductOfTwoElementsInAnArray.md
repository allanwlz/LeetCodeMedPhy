# 数组中两元素的最大乘积

## 题目
给你一个整数数组 ``nums``，请你选择数组的两个不同下标 ``i`` 和 ``j``，使 ``(nums[i]-1)*(nums[j]-1)`` 取得最大值。

请你计算并返回该式的最大值。

**示例 1**：
```
输入：nums = [3,4,5,2]
输出：12 
解释：如果选择下标 i=1 和 j=2（下标从 0 开始），则可以获得最大值，(nums[1]-1)*(nums[2]-1) = (4-1)*(5-1) = 3*4 = 12 。 
```

**示例 2**：
```
输入：nums = [1,5,4,5]
输出：16
解释：选择下标 i=1 和 j=3（下标从 0 开始），则可以获得最大值 (5-1)*(5-1) = 16 。
```

**示例 3**：
```
输入：nums = [3,7]
输出：12
```

**提示**：
```
2 <= nums.length <= 500
1 <= nums[i] <= 10^3
```

## 解答

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxProduct = function(nums) {
    let maxNum = 0;
    let maxIdx;
    for (let i = 0, len = nums.length; i < len; i++) {
        if (maxNum < nums[i]) {
            maxNum = nums[i];
            maxIdx = i;
        }
    }
    let secondMax = 0;
    for (let i = 0, len = nums.length; i < len; i++) {
        if (i === maxIdx) {
            continue;
        }
        if (secondMax < nums[i]) {
            secondMax = nums[i];
        }
    }
    return (maxNum - 1) * (secondMax - 1);
};
```
## 思路

由于数组内的元素都是正整数，所以一开始想先对数组进行排序，但这样的话其实时间复杂度应该会要 ``O(nlog(n))``，后来想到只是要找到最大的两个元素，所以想一下感觉两次遍历，分别取前两个数字，时间复杂度只有 ``O(n)``。