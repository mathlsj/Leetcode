# leetcode-algorithms-9 Palindrome Number

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.
Example 1:
```
Input: 121
Output: true
```
Example 2:
```
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```
Example 3:
```
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```
Follow up:

Coud you solve it without converting the integer to a string?

## 解法 

将数反转,反转后的数与原来的数相等.
```
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0) return false;
        
        long long rx = 0;
        int last = x;
        while(last != 0)
        {
            rx = rx * 10 + last % 10;
            last /= 10;
        }
        
        retrun rx == x;
    }
};
```
时间复杂度: O(lg(x)).
空间复杂度: O(1).