Given an array `nums` of *n* integers and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. Return the sum of the three integers. You may assume that each input would have exactly one solution.

**Example:**

```
Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

# Allan

```c++
#define INT_MAX 2147483645
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        int length = nums.size();
        std::sort(nums.begin(), nums.end());
        vector<int> sum_table(length*length, INT_MAX);
        for(int i=0;i<length;i++)
        {
            for(int j=0;j<length;j++)
            {
                if(i >= j) continue;
                int res = target - nums[i] - nums[j];
                int sum_pos = i * length + j;
                auto t = std::lower_bound(nums.begin(), nums.end(), res);
                int upper = t - nums.begin();
                int lower = upper - 1;
                while(upper==i || upper == j) upper++;
                while(lower==i || lower == j) lower--;
                if(lower<0 && upper < length) 
                {
                    sum_table[sum_pos] = nums[i] + nums[j] + nums[upper];
                    continue;
                }
                else if(upper >= length && lower>=0)
                {
                    sum_table[sum_pos] = nums[i] + nums[j] + nums[lower];
                    continue;
                }
                else
                {
                    if(nums[i] + nums[j] + nums[upper] - target > target - (nums[i] + nums[j] + nums[lower]))
                    {
                        sum_table[sum_pos] = nums[i] + nums[j] + nums[lower];
                        continue;
                    }
                    else
                    {
                        sum_table[sum_pos] = nums[i] + nums[j] + nums[upper];
                        continue;
                    }
                }
            }
        }
        std::sort(sum_table.begin(), sum_table.end());
        auto t = std::lower_bound(sum_table.begin(), sum_table.end(), target);
        if(t > sum_table.begin()) return *t - target < target - *(t - 1) ? *t:*(t - 1);
        else  return *t;
    }
};
```

**125 / 125** test cases passed.

Status: 

#### Accepted

Runtime: **304 ms**

Memory Usage: **20.6 MB**

Submitted: **2 minutes ago**

$O(n^2\log(n))$ 复杂度。两次遍历，再加上在内循环中一个binaray_search。



```c++
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        std::sort(nums.begin(), nums.end());
        int res = nums[0] + nums[1] + nums[2];
        for(int i = 0;i<nums.size()-2;i++)
        {
            int left = i + 1;
            int right = nums.size() - 1;
            while(left < right)
            {
                int t = nums[i] + nums[left] + nums[right];
                res = abs(res - target) < abs(t - target)?res:t;
                if(t < target) left++;
                else right--;
            }
        }
        return res;
    }
};
```

| **125 / 125** test cases passed.           | Status: Accepted             |
| ------------------------------------------ | ---------------------------- |
| Runtime: **16 ms**Memory Usage: **8.6 MB** | Submitted: **3 minutes ago** |

$O(n^2)$ 复杂度。标准的3指针解法。一开始没有想到这个方法的原因是对两指针解最近距离的方法理解不到位。