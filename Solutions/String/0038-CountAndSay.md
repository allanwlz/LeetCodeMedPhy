# 外观数列
## 题目
「外观数列」是一个整数序列，从数字 1 开始，序列中的每一项都是对前一项的描述。前五项如下：
```
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

``1`` 被读作  ``"one 1"``  ("一个一") , 即 ``11``。
``11`` 被读作 ``"two 1s"`` ("两个一"）, 即 ``21``。
``21`` 被读作 ``"one 2"``,  ``"one 1"`` （"一个二" ,  "一个一") , 即 ``1211``。

给定一个正整数 ``n（1 ≤ n ≤ 30）``，输出外观数列的第 ``n`` 项。

注意：整数序列中的每一项将表示为一个字符串。

## 解法
```js
/**
 * @param {number} n
 * @return {string}
 */
var countAndSay = function(n) {
    if (n === 1) {
        return '1';
    }
    let nStr = '1';
    let i = 2;
    while (i <= n) {
        nStr = say(nStr);
        i ++;
    }
    return nStr;
};

function say (str) {
  let count = 0, curStr = '';
  let sayStr = '';
  for (let i = 0; i < str.length; i++) {
    // 初始情况
    if (count === 0) {
        count ++;
        curStr = str[i];
    } else if (curStr === str[i]){
        count ++;
    } else {
        sayStr = sayStr + count + curStr;
        count = 1;
        curStr = str[i];
    }
  }
  if (count) {
    // 清空
    sayStr = sayStr + count + curStr;
  }
  return sayStr;
}
```
## 思路
思路比较简单：
1. 首先构造一个``say()``函数。该函数能按照题目规则将输入字符串读出来；
2. 利用``say()``函数不断迭代读取上一字符串。
