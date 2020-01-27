# 最长连续序列
## 题目
给定一个未排序的整数数组，找出最长连续序列的长度。

要求算法的时间复杂度为 *O(n)*。

**示例：**
```
输入: [100, 4, 200, 1, 3, 2]
输出: 4
解释: 最长连续序列是 [1, 2, 3, 4]。它的长度为 4。
```

## 解法
```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var longestConsecutive = function(nums) {
    let hashSet = new Set(nums);
    let maxLength = 0, currLength = 0;
    for (let ele of hashSet) {
        // 这里是抄的思路，为了避免多次重复计数，只对子序列首元素的进行计算
        if (!hashSet.has(ele - 1)) {
            // 记录当前元素
            currLength ++;
            while(hashSet.has(ele + 1)) {
                ele = ele + 1;
                currLength ++;
            }
            maxLength = Math.max(maxLength, currLength);
            // 需要初始化当前长度为 0
            currLength = 0;
        }
    }
    return maxLength;
};
```
## 思路
题目的关键思路有两部分：
1. 能够快速查询当前元素的下一个元素：自然而然会让人想到HashSet；
2. 避免对某个子序列中的元素进行重复计数，因为这可能会使最差的时间复杂度退化到*O(n^2)*。
