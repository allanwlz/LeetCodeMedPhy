Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

```
Input: ["flower","flow","flight"]
Output: "fl"
```

**Example 2:**

```
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

# Allan

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        index = 0
        if len(strs) == 0:
            return ""
        if len(strs[0]) == 0:
            return ""
        while True:
            if len(strs[0]) < index + 1:
                break
            character = strs[0][index]
            align_symbol = True 
            for string in strs:
                if len(string) < index + 1 or string[index] != character:
                    align_symbol = False
                    break
            if not align_symbol:
                break
            index = index + 1
        return strs[0][:index]
```

一道非常简单的题。



做这种题，最需要挑战的是能不能一遍过。在第一次提交之前就尽量考虑到所有的可能性。我还不行，需要继续锻炼。