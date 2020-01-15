# 下一个更大元素 I
## 题目
给定两个**没有重复元素**的数组 ``nums1`` 和 ``nums2`` ，其中 ``nums1`` 是 ``nums2`` 的子集。找到 ``nums1`` 中每个元素在 ``nums2`` 中的下一个比其大的值。

``nums1`` 中数字 ``x`` 的下一个更大元素是指 ``x`` 在 ``nums2`` 中对应位置的右边的第一个比 ``x`` 大的元素。如果不存在，对应位置输出-1。

示例一：
```
输入: nums1 = [4,1,2], nums2 = [1,3,4,2].
输出: [-1,3,-1]
解释:
    对于num1中的数字4，你无法在第二个数组中找到下一个更大的数字，因此输出 -1。
    对于num1中的数字1，第二个数组中数字1右边的下一个较大数字是 3。
    对于num1中的数字2，第二个数组中没有下一个更大的数字，因此输出 -1。
```

示例二：
```
输入: nums1 = [2,4], nums2 = [1,2,3,4].
输出: [3,-1]
解释:
    对于num1中的数字2，第二个数组中的下一个较大数字是3。
    对于num1中的数字4，第二个数组中没有下一个更大的数字，因此输出 -1。
```

注意：
1. ``nums1`` 和 ``nums2`` 中所有元素是唯一的。
2. ``nums1`` 和 ``nums2`` 的数组大小都不超过1000。

## 解法
```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
let nextGreaterElement = function(nums1, nums2) {
    let resultMap = new Map();
    let monotonicStack = [];
    for (let val of nums2) {
        if (!monotonicStack.length) {
            // 当栈内为空的时候，push
            monotonicStack.push(val);
        } else if (val > monotonicStack[monotonicStack.length - 1]) {
            // 当下一个元素比栈顶元素更大，不断推出栈顶元素加入到哈希表，直至栈清空或栈顶元素不小于val
            while (monotonicStack.length && monotonicStack[monotonicStack.length - 1] < val) {
                resultMap.set(monotonicStack.pop(), val);
            }
            monotonicStack.push(val);
        } else {
            // 当下一个元素比
            monotonicStack.push(val);
        }
    }
    let result = [];
    for (let i = 0; i < nums1.length; i++) {
        let nextVal = resultMap.get(nums1[i]);
        if (nextVal) {
            result.push(nextVal);
        } else {
            result.push(-1);
        }
    }
    return result;
};
```
## 思路
这道题目比较重要的思路主要分为两点：
1. 运用**单调栈**，获得 ``nums2`` 中的每个元素的下一个最大元素（Next Greater Element, NGE）；
2. 将 ``nums2`` 中每一个元素的下一个最大元素以哈希表保存，方便查找其子集 ``nums1`` 中各个元素的 NGE。 
