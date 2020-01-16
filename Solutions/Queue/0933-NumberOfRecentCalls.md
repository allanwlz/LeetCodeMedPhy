# 最近的请求次数
By JC
## 题目
写一个 ``RecentCounter`` 类来计算最近的请求。

它只有一个方法：``ping(int t)``，其中 ``t`` 代表以毫秒为单位的某个时间。

返回从 ``3000`` 毫秒前到现在的 ``ping`` 数。

任何处于 ``[t - 3000, t]`` 时间范围之内的 ``ping`` 都将会被计算在内，包括当前（指 ``t`` 时刻）的 ``ping``。

保证每次对 ``ping`` 的调用都使用比之前更大的 ``t`` 值。

示例：
```
输入：inputs = ["RecentCounter","ping","ping","ping","ping"], inputs = [[],[1],[100],[3001],[3002]]
输出：[null,1,2,3,3]
```

提示：

1. 每个测试用例最多调用 10000 次 ``ping``。
2. 每个测试用例会使用严格递增的 ``t`` 值来调用 ``ping``。
3. 每次调用 ``ping`` 都有 ``1 <= t <= 10^9``。
## 解法
```js
let RecentCounter = function() {
    this.pingQueue = [];
};

/** 
 * @param {number} t
 * @return {number}
 */
RecentCounter.prototype.ping = function(t) {
    // push 是在列表后面加入元素，类似于enqueue
    this.pingQueue.push(t);
    while(t - this.pingQueue[0] > 3000) {
        // shift 是从列表前面剔除元素，相当于dequeue
        this.pingQueue.shift()
    }
    return this.pingQueue.length;
};

/**
 * Your RecentCounter object will be instantiated and called as such:
 * var obj = new RecentCounter()
 * var param_1 = obj.ping(t)
 */
```
## 思路
这道题难就难在阅读理解上面。
1. 首先 ``t`` 表示的是时间的毫秒数，然后 ``ping(t)`` 都是在 ``t (ms)`` 时刻发生的；
2. 以例子解释，``1ms`` 时刻 ``ping(1)``，此时在 ``[-2999, 1]`` 只包含 1 一个有效元素，故而返回 1；``100ms`` 发生 ``ping(100)``，在 ``[-2900, 100]`` 范围内有 1 和 100，因此返回结果为2；之后``ping(3001)``，在``[1, 3001]``内，包括1、100和3001，故而返回3；``ping(3002)``时，``[2, 3002]`` 内只包含100、3001和3002，仍然返回3；
3. 读懂了题目后应该就比较好知道，只需要将列表（相当于一个从列表尾部入列、列表头部出列的Queue）首部和当前时间差距大于 ``3000ms``的元素出列，然后计算列表长度即可。
