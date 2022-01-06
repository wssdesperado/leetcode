### Problem 3 - Longest Substring Without Repeating Characters

## Origininal Version

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if len(s) == 1:
            return 1
        elif len(s) == 0:
            return 0
        else:
            length = 1
            for head in range(0, len(s)):
                for tail in range(1, len(s)):
                    if head == tail:
                        break
                    if not self.hasRepeatingCharacter(head, tail, s):
                        length += 1
                        continue
                    else:
                        head += 1
                break
        return length
    
    def hasRepeatingCharacter(self, head: int, tail: int, s: str):
        for i in range(head, tail + 1):
            for j in range(i + 1, tail + 1):
                if s[i] == s[j]:
                    return True
        return False
'''

Outline: Sliding Window
- 使用两个指针表示字符串中的某个子串（或窗口）的左右边界
- 在每一步的操作中，将左指针向右移动一格，表示 我们开始枚举下一个字符作为起始位置，然后我们可以不断地向右移动右指针，但需要保证这两个指针对应的子串中没有重复的字符。在移动结束后，这个子串就对应着 以左指针开始的，不包含重复字符的最长子串。我们记录下这个子串的长度；
在枚举结束后，我们找到的最长的子串的长度即为答案。

Improve: Use hashmap (dict in python3) to determine the repeating character

## Better Solution
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        dic, res, i = {}, 0, -1   #i是左指针
        for j in range(len(s)):  #j是右指针
            if s[j] in dic:     #若当前元素在之前出现过，更新左指针
                #当之前出现的元素在左右指针中间，左指针更新为之前元素下标，若不在中间，左指针不变 (即此时更新窗口的左边界）
                i = max(i, dic[s[j]]) 
            dic[s[j]] = j    #将当前元素加入哈希表中
            res = max(res, j - i)   
        return res
```
