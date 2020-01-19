# 
## 题目
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
