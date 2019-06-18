# leetcode-algorithms-36 Valid Sudoku

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

1. Each row must contain the digits 1-9 without repetition.
2. Each column must contain the digits 1-9 without repetition.
3. Each of the 9 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.

![](../image/250px-Sudoku-by-L2G-20050714.svg.png)

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

Example 1:
```
Input:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: true
```
Example 2:
```
Input:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being 
    modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.
```
Note:

+ A Sudoku board (partially filled) could be valid but is not necessarily solvable.
+ Only the filled cells need to be validated according to the mentioned rules.
+ The given board contain only digits 1-9 and the character '.'.
+ The given board size is always 9x9.

## 解法

将行,列和小方框三个全都各自存到一个二维数组中,第一维存位置,第二维数值,并将结果置1.如果已在当前数组中有重复的数值,其值会是1.如例子2: board[0][0]位置有数值8,则column[0][7]=1,在board[3][0]位置还有个数值8同,则重复了column[0][7],验证失败.
```
class Solution
{
public:
    bool isValidSudoku(vector<vector<char>>& board)
    {
        int row[9][9] = {0};
        int column[9][9] = {0};
        int sub_box[9][9] = {0};
        
        for (int i = 0; i < board.size(); ++i)
        {
            for (int j = 0; j < board[i].size(); ++j)
            {
                if (board[i][j] != '.')
                {
                    int num = board[i][j] - '0' - 1;
                    int sub_index = i / 3 * 3 + j / 3;
                    if (column[i][num] > 0 || row[j][num] > 0 || sub_box[sub_index][num] > 0)
                        return false;
                    column[i][num] = row[j][num] = sub_box[sub_index][num] = 1; 
                }                               
            }
        }
        return true;
    }
};
```
时间复杂度: O(n^2).

空间复杂度: O(3*n^2).
