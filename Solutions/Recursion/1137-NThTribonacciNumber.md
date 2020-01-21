# 第N个泰波那契数
## 题目
泰波那契序列 Tn 定义如下： 

``T0 = 0, T1 = 1, T2 = 1``, 且在 ``n >= 0`` 的条件下 ``Tn+3 = Tn + Tn+1 + Tn+2``

给你整数 ``n``，请返回第 ``n`` 个泰波那契数 ``Tn`` 的值。

**示例 1：**
```
输入：n = 4
输出：4
解释：
T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4
```

**提示：**

- ``0 <= n <= 37``
- 答案保证是一个32位整数，即 ``answer <= 2^31 - 1``。

## 解法
### 递归解法
```js
/**
 * @param {number} n
 * @return {number}
 */
var tribonacci = function(n) {
    if (n === 0) {
        return 0;
    } else if (n === 1 || n === 2) {
        return 1;
    } else {
        return tribonacci(n - 1) + tribonacci(n - 2) + tribonacci(n - 3);
    }
};
```
运算结果：

超时！

### 迭代算法
```js
/**
 * @param {number} n
 * @return {number}
 */
let tribonacci = function(n) {
    if (n === 0) {
        return 0;
    } else if (n === 1 || n === 2) {
        return 1;
    } else {
        let first = 0, second = 1, third = 1, forth;
        while (n -- > 2) {
            forth = first + second + third;
            first = second;
            second = third;
            third = forth;
        }
        return forth;
    }
};
```
## 思路
整体求解思路和斐波那契数求解一致，将递归修改成从底到顶的迭代形式。
