# leetcode-algorithms-5 Longest Palindromic Substring

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example 1:
```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```
Example 2:
```
Input: "cbbd"
Output: "bb"
```

## 解法1

暴力破解,从最长的长度开始查找所有的子串,检查子串是否为回文串.
```
class Solution
{
public:
    bool checkPalindrome(const std::string &s)
    {
        int len = s.size();
        for (int i = 0; i < len/2; ++i)
        {
            if (s[i] != s[len -i - 1])
                return false;
        }
        return true;
    }
    
    string longestPalindrome(string s)
    {
        std::string pal;
        int len = s.size();
        for (int i = len; i > 0; --i)
        {
            for (int start = 0; start + i <= len; ++start)
            {
                pal = s.substr(start, i);
                if (checkPalindrome(pal))
                    return pal;
            }
        }
        
        return pal;
    }
};
```
时间复杂度: O(n^3).三个嵌套循环,O(n) * O(n) * O(n/2) = O(n^3).
空间复杂度: O(1)

##解法2
观察回文串的规律.如:aba,先找到一个字母,然后两边都增加相同字母也是回文串,以此类推,就可以找到最大回文串.还有另种情况是:abba,则要先找到两个相邻是相同的字母.因此关键就是找到这个回文串的中心.
```
class Solution
{
public:
    int palindromeCenter(const std::string &s, int left, int right)
    {
        while(left >= 0 && right < s.size() && s[left] == s[right])
        {
            --left;
            ++right;
        }
        
        return right - left - 1;
    }
    
    string longestPalindrome(string s) {
        int len = s.size();
        if (len <= 0) return "";
        
        int start = 0;
        int palindromeLen = 0;
        for (int i = 0; i < len; ++i)
        {
            int len1 = palindromeCenter(s, i, i);
            int len2 = palindromeCenter(s, i, i + 1);
            int maxLen = len1 > len2 ? len1 : len2;
            if (maxLen > palindromeLen)
            {
                start = i - (maxLen - 1) / 2;
                palindromeLen = maxLen;
            }
        }
        return s.substr(start,palindromeLen);
    }
};
```
时间复杂度: O(n^2).
空间复杂度: O(1).
