Given *n* non-negative integers *a1*, *a2*, ..., *an* , where each represents a point at coordinate (*i*, *ai*). *n* vertical lines are drawn such that the two endpoints of line *i* is at (*i*, *ai*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note:** You may not slant the container and *n* is at least 2.

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

**Example:**

```
Input: [1,8,6,2,5,4,8,3,7]
Output: 49
```



# Allan

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        length = len(height)
        left = 0
        right = length - 1
        maxArea = 0
        while(left < right):
            height_left = height[left]
            height_right = height[right]
            area = min(height_right, height_left) * (right - left)
            if area > maxArea:
                maxArea = area
            if height_left > height_right:
                right = right - 1
            else:
                left = left + 1
        return maxArea
```

一道略微脑筋急转弯的题目

问题的难点在于怎样确定指针移动的关系。左右指针每次计算完面积之后，移动高度较矮的指针至下一个位置。这是因为高度较矮的指针，不可能成为下一个更大面积区域的左指针，因为面积由其自身高度和其与另一个指针的距离确定。如果移动较高的指针，所得面积必然更小。