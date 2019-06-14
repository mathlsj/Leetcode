# leetcode-algorithms-14 Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

Example 1:
```
Input: ["flower","flow","flight"]
Output: "fl"
```
Example 2:
```
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```
Note:

All given inputs are in lowercase letters a-z.

## 解法

从第一个字符串开始分别对其它字符串从头到尾匹配,只要碰到一个不相同的或已到其中一个字符串的末尾就说明其公共的字符串就是前面的i个字符.
```
class Solution
{
public:
    string longestCommonPrefix(vector<string>& strs)
    {
        if (strs.size() <= 0) return "";
               
        for (int i = 0; i < strs[0].length(); ++i)
        {
            for (int j = 1; j < strs.size(); ++j)
            {
                if (strs[j].length() == i || strs[0][i] != strs[j][i])
                    return strs[0].substr(0, i);
            }
        }
        
        return strs[0];
    }
};
```
时间复杂度: O(n).

空间复杂度: O(1).