# 快乐数

## 题目
编写一个算法来判断一个数 n 是不是快乐数。

「快乐数」定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，然后重复这个过程直到这个数变为 1，也可能是 **无限循环** 但始终变不到 1。如果 可以变为  1，那么这个数就是快乐数。

如果 n 是快乐数就返回 True ；不是，则返回 False 。

**示例**：
```
输入：19
输出：true
解释：
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```
## 解法
```js
/**
 * @param {number} n
 * @return {boolean}
 */
var isHappy = function(n) {
    const resultSet = new Set();
    let result = happyOnce(n);
    resultSet.add(result);
    while (result !== 1) {
        result = happyOnce(result);
        if (resultSet.has(result)) {
            return false;
        } else {
            resultSet.add(result);
        }
    }
    return true;
};

/**
 * happy 一下
 * @param num{number}
 * @returns {number}
 */
function happyOnce(num) {
    const numArr = String(num).split('');
    let sum = 0;
    for (let i = 0, len = numArr.length; i < len; i++) {
        sum += parseInt(numArr[i]) ** 2;
    }
    return sum;
}
```
## 思路

题干有提示，如果非快乐数会陷入无限循环，因此只要在“快乐一下”的过程中，出现了之前出现过的数字，那么表明必然会陷入循环，这个数字就不是快乐数，而 Set 数据结构正好对此十分在行！
