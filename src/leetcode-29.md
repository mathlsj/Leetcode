# leetcode-algorithms-29 Divide Two Integers

Given two integers dividend and divisor, divide two integers without using multiplication, division and mod operator.

Return the quotient after dividing dividend by divisor.

The integer division should truncate toward zero.

Example 1:
```
Input: dividend = 10, divisor = 3
Output: 3
```
Example 2:
```
Input: dividend = 7, divisor = -3
Output: -2
```
Note:

Both dividend and divisor will be 32-bit signed integers.
The divisor will never be 0.
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 231 − 1 when the division result overflows.

## 解法

```
class Solution
{
public:
    int divide(int dividend, int divisor)
    {
        if (divisor == 0 || (dividend == INT_MIN && divisor == -1))
            return INT_MAX;
        
        int sign = ((dividend < 0) ^ (divisor < 0)) ? -1 : 1;
        long long ldvd = labs(dividend);
        long long ldvs = labs(divisor);
        int res = 0;
        while (ldvd >= ldvs)
        { 
            long long temp = ldvs;
            long long multiple = 1;
            while (ldvd >= (temp << 1))
            {
                temp <<= 1;
                multiple <<= 1;
            }
            ldvd -= temp;
            res += multiple;
        }
        return sign == 1 ? res : -res;
    }
};
```