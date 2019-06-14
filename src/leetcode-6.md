# leetcode-algorithms-6 ZigZag Conversion

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
```
P   A   H   N
A P L S I I G
Y   I   R
```
And then read line by line: "PAHNAPLSIIGYIR"

Write the code that will take a string and make this conversion given a number of rows:
```
string convert(string s, int numRows);
```
Example 1:
```
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```
Example 2:
```
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:

P     I    N
A   L S  I G
Y A   H R
P     I
```

## 解法

观察输出后的字符串,可得出规律:

+ row = 0(第一行)时,对于index k = k * (2 * numRows - 2);
+ row = numRows - 1(最后一行),对于index k = k * (2 * numRows - 2) + numRows - 1;
+ row = i(第i行),有两种情况,k * (2 * numRows - 2) + i和 (k + 1) * (2 * numRows - 2) - i;

```
class Solution
{
public:
    string convert(string s, int numRows)
    {
        if (numRows == 1) return s;
        
        std::string convertString;
        int n = s.size();
        int loopLen = 2 * numRows - 2;
        for (int i = 0; i < numRows; i++)
        {
            for (int j = 0; j + i < n; j += loopLen)
            {
                convertString += s[j + i];
                if (i != 0 && i != numRows - 1 && j + loopLen - i < n)
                    convertString += s[j + loopLen - i];
            }
        }
        return convertString;
    }
};
```
时间复杂度: O(n).
空间复杂度: O(1).