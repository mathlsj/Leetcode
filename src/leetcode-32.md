# leetcode-algorithms-32 Longest Valid Parentheses

Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

Example 1:
```
Input: "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()"
```
Example 2:
```
Input: ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()"
```

## 解法

使用栈来解决,碰到"("入栈,")"出栈,用字符串的位置减去出栈位置就可获得长度,找出最大值就是需要求的长度.
```
class Solution {
public:
    int longestValidParentheses(string s) {
        if (s.size() == 0)
            return 0;
        
        int max = 0;
        std::stack<int> st;        
        st.push(-1);
        for (int i = 0; i < s.length(); ++i)
        {
            if (s[i] == '(')
                st.push(i);
            else
            {
                st.pop();
                if (st.empty())
                    st.push(i);
                else
                {
                    int t = i - st.top();
                    max = max > t ? max : t;
                }
            }
        }
        
        return max;
    }
};
```
时间复杂度: O(n).n是字符串长度.

空间复杂度: O(n).n是字符串长度.