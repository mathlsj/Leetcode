# leetcode-algorithms-3 Longest Substring Without Repeating Characters

Given a string, find the length of the longest substring without repeating characters.

Example 1:
```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
```
Example 2:
```
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```
Example 3:
```
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

## 解法1

一步步检查所有字串看是否有重复的字符
```
class Solution
{
public:
    int lengthOfLongestSubstring(string s)
    {       
        string longest;
        for (int i = 0; i < s.size(); ++i)
        {
            for (int j = s.size() - i; j > 0; --j)
            {
                string longesttemp = s.substr(i, j);
                
                bool repect = false;
                int a[256] = {0};
                for (int n = 0; n < longesttemp.size(); ++n)
                {
                    int x = longesttemp[n];
                    ++a[x];
                    if (a[x] > 1)
                    {
                        repect = true;
                        break;   
                    }
                }
                if (!repect && (longesttemp.size() > longest.size())) longest = longesttemp;
            } 
        }
        return longest.size();
    }
};
```
时间复杂度: O(n^3).

空间复杂度: O(min(n,m)).

LeetCode执行时长: 执行太长,时间超时.

## 解法2

解法1的时间复杂度太高了,效率低下.字符串查找要怎么提高效率,首先都应该想到*Sliding Window*算法.设定一个窗口[i, j],将i到j的内容存入map,下面滑动j,如果s[j] (s表示字符串)在map中存在,表示字符串已经重复了,记下最大值,然后将i窗口滑到s[j]
上次的位置.

下面是代码的实现:
```
class Solution
{
public:
    int lengthOfLongestSubstring(string s)
    {       
        int n = s.length();
        std::unordered_map<char, int> m;
        int len = 0;
        
        for (int i = 0, j = 0; j < n; ++j)
        {
            auto fiter = m.find(s[j]);
            if (fiter != m.end())
            {
                i = (fiter->second) > i ? fiter->second : i;
            }
                
            int temp_len = j - i + 1;
            len = (len > temp_len) ? len : temp_len;
            m[s[j]] = j + 1;
        }
        return len;
    }
};
```
时间复杂度: O(n).只有一个j循环.

空间复杂度: O(m).m是最大的不重复子串的长度.

LeetCode执行时长: 24ms.

##解法3

对于解法2有没更快捷的方式.参考KMP算法对字符串的处理,我们可以将字符存入整型数组,值存储字符所在的位置,这样就可以在算法2的基础上少一次查询.
```
class Solution
{
public:
    int lengthOfLongestSubstring(string s)
    {       
        int n = s.length();
        int len = 0;
        int index[128] = {0};
        
        for (int i = 0, j = 0; j < n; ++j)
        {
            i = i > index[s[j]] ? i : index[s[j]];
            int temp_len = j - i + 1;
            len = (len > temp_len) ? len : temp_len; 
            index[s[j]] = j + 1;        
        }
        return len;
    }
};
```
时间复杂度: O(n).

空间复杂度: O(n).

LeetCode执行时长: 12ms.