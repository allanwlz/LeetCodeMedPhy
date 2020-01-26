# 数组种的第K个最大元素

## 题目

在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

**示例 1：**
```
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
```

**示例 2：**
```
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```
**说明：**你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。

## 解法
### 解法一、通过小顶堆解决
**思路：**维护一个大小为*K*的小顶堆，此时堆顶即为堆内第*K*大元素；后续数组后续元素比小顶堆的堆顶要小，则忽略，比堆顶元素大则删除堆顶，添加新的元素。最终当数组内所有元素均通过后，堆顶元素即为第*K*大的元素。
```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var findKthLargest = function(nums, k) {
    // 建立小顶堆
    let priorityQueue = new PriorityQueue((a, b) => {return b < a ? b : a});
    // 先给k个进去
    for (let i = 0; i < k; i++) {
        priorityQueue.insert(nums[i]);
    }
    for (let i = k; i < nums.length; i++) {
        if (nums[i] > priorityQueue.getTop()) {
            priorityQueue.delTop();
            priorityQueue.insert(nums[i]);
        }
    }
    return priorityQueue.getTop();
};

function PriorityQueue(getPrior) {
  this._pq = [];
  this._size = 0;
  // getPrior(pNode, cNode) if cNode has higher priority than pNode then return cNode, else return pNode
  this._getPrior = getPrior;
}

PriorityQueue.prototype.getSize = function () {
  return this._size;
};

PriorityQueue.prototype.insert = function (ele) {
  // 在末尾加入该元素后，上滤
  this._pq[this._size++] = ele;
  this._percolateUp(this._size - 1);
};

PriorityQueue.prototype.getTop = function () {
  if (!this._pq.length) {
    throw new Error('Empty PriorityQueue');
  }
  return this._pq[0];
};

PriorityQueue.prototype.delTop = function () {
  if (this._pq.length === 0) {
    throw new Error('Empty PriorityQueue');
  }
  if (this._size === 1) {
    let maxEle = this._pq[0];
    this._pq = [];
    this._size = 0;
    return maxEle;
  } else {
    let maxEle = this._pq[0];
    this._pq[0] = this._pq.pop();
    this._size --;
    this._percolateDown(this._size, 0);
    return maxEle;
  }
};

PriorityQueue.prototype._percolateUp = function (index) {
  // index 当前父结点的 秩
  let pIndex = Math.floor((index - 1) / 2);
  while (pIndex >= 0) {
    if (this._getPrior(this._pq[pIndex], this._pq[index]) === this._pq[pIndex]) {  // 若当前结点的父结点值大
      break;
    } else {  // 否则交换值
      let tmp = this._pq[pIndex];
      this._pq[pIndex] = this._pq[index];
      this._pq[index] = tmp;
      index = pIndex;
      pIndex = Math.floor((index - 1) / 2);
    }
  }
};

// n 为priorityQueue 的大小，主要用来辅助判断其子是否合法
PriorityQueue.prototype._percolateDown = function (n, index) {
  let properIndex = this._getProperParent(n, index);
  while (index !== properIndex) {
    let tmp = this._pq[properIndex];
    this._pq[properIndex] = this._pq[index];
    this._pq[index] = tmp;
    index = properIndex;
    properIndex = this._getProperParent(n, index);
  }
};

// [0, n) 是合法秩
PriorityQueue.prototype._getProperParent = function (n, index) {
  let lcIndex = index * 2 + 1, rcIndex = index * 2 + 2;
  return this._getValidBiggerIndex(n, this._getValidBiggerIndex(n, index, lcIndex), rcIndex);
};

PriorityQueue.prototype._getValidBiggerIndex = function (size, pIndex, cIndex) {
  // 子结点的index可能非法
  if (cIndex >= size) {
    return pIndex;
  } else {
    // 只有当子结点大于父结点才替换，等于或小于不替换
    return this._getPrior(this._pq[pIndex], this._pq[cIndex]) === this._pq[cIndex] ? cIndex : pIndex;
  }
};
```

### 解法二：

## 思路
在《数据结构（C++ 语言版）》（第3版）中第12章排序中的快速排序一节中有关于*K-选取*问题的描述。

 
