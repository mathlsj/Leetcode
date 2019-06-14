# leetcode-algorithms-20 Valid Parentheses

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.

Example 1:
```
Input: "()"
Output: true
```
Example 2:
```
Input: "()[]{}"
Output: true
```
Example 3:
```
Input: "(]"
Output: false
```
Example 4:
```
Input: "([)]"
Output: false
```
Example 5:
```
Input: "{[]}"
Output: true
```

## 解法

通过栈实现匹配.
```
class Solution
{
public:
    bool isValid(string s)
    {
        std::stack<char> matchs;
        for (int i = 0; i < s.size(); ++i)
        {
            switch(s[i])
            {
                case '(':
                case '{':
                case '[':
                    matchs.push(s[i]);
                    break;
                case ')':
                    if (matchs.size() <= 0 || matchs.top() != '(') return false;
                    matchs.pop();
                    break;
                case '}':
                    if (matchs.size() <= 0 || matchs.top() != '{') return false;
                    matchs.pop();
                    break;
                case ']':
                    if (matchs.size() <= 0 || matchs.top() != '[') return false;
                    matchs.pop();
                    break;
            }
        }
        return matchs.empty();
    }
};
```