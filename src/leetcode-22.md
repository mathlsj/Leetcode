# leetcode-algorithms-22 Generate Parentheses

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:
```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

## 解法

```
class Solution {
public:
    vector<string> generateParenthesis(int n)
    {
        std::vector<std::string> result;
        addParenth(result, "", n, 0);
        
        return result;
    }   
        
    void addParenth(std::vector<std::string> &v, std::string str, int n, int m)
    {
        if(n==0 && m==0)
        {
            v.push_back(str);
            return;
        }
         
        if(m > 0)
            addParenth(v, str+")", n, m-1);
        if(n > 0)
            addParenth(v, str+"(", n-1, m+1);
    }
};
```