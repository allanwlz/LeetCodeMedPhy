# 最后一块石头的重量
## 题目
有一堆石头，每块石头的重量都是正整数。

每一回合，从中选出两块**最重的**石头，然后将它们一起粉碎。假设石头的重量分别为 ``x`` 和 ``y``，且 ``x <= y``。那么粉碎的可能结果如下：

- 如果 ``x == y``，那么两块石头都会被完全粉碎；
- 如果 ``x != y``，那么重量为 ``x`` 的石头将会完全粉碎，而重量为 ``y`` 的石头新重量为 ``y-x``。

最后，最多只会剩下一块石头。返回此石头的重量。如果没有石头剩下，就返回 0。

**提示：**

1. ``1 <= stones.length <= 30``
2. ``1 <= stones[i] <= 1000``

## 解答
```js
/**
 * @param {number[]} stones
 * @return {number}
 */
var lastStoneWeight = function(stones) {
    let priorityQueue = new PriorityQueue();
    // 先将所有石头置入堆内
    for (let stone of stones) {
        priorityQueue.insert(stone);
    }
    // 当堆非空时
    let no1Stone, no2Stone, diff;
    while (priorityQueue.getSize()) {
        no1Stone = priorityQueue.delMax();
        // 如果出来第一个石头，堆就空了
        if (priorityQueue.getSize() === 0) {
            return no1Stone;
        }
        no2Stone = priorityQueue.delMax();
        diff = no1Stone - no2Stone;
        if (diff > 0) {
            priorityQueue.insert(diff);
        }
    }
    return 0;
};

// 注意，PriorityQueue的实现在`Summary/Heap/Heap.md`中
```

- 执行用时在所有的JavaScript提交中击败了``96.32%``的用户；
- 内存消耗击败了``84.15%``的用户。

## 思路
由于本题目需要频繁使用到最大值的操作，同时又可能要插入新的值，非常符合堆的特性。
