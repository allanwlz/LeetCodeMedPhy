Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![img](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

**Example:**

```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

# Allan

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        d = {2:"abc",3:"def",4:"ghi",5:"jkl",6:"mno",7:"pqrs",8:"tuv",9:"wxyz"}
        ar = []
        if '1' in digits or '0' in digits or len(digits)<=0:
            return []
        for i in (digits):
            if int(i) in d:
                ar.append(list(d[int(i)]))
    
        for i in range(len(ar)-1,0,-1):
            ans = []
            for char in ar[i-1]:
                for char2 in ar[i]:
                    ans.append(char+char2)
            ar[i-1] = ans

        return ar[0] 
```

一道非常简单的题。


