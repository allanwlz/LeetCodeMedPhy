# 两个数组的交集
By JC

## 题目
给定两个数组，编写一个函数来计算它们的交集。

示例一：
```
输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2]
```

示例二：
```
输入: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出: [9,4]
```

说明：
- 输出结果中的每个元素一定是唯一的；
- 我们可以不考虑输出结果的顺序。
## 解法
```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersection = function(nums1, nums2) {
    let set1 = new Set(nums1);
    let set2 = new Set(nums2);
    let outArr = [];
    for (let s of set1) {
        if (set2.has(s)) {
            outArr.push(s);
        }
    }
    return outArr;
};
```
## 思路
目前是先将数组转换成``Set``，然后用暴力方法求解。
