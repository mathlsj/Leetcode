# leetcode-algorithms-11 Container With Most Water 

Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2.

![](../image/question_11.jpg)

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

Example:
```
Input: [1,8,6,2,5,4,8,3,7]
Output: 49
```

##解法1

列出所有情况,找到最大值.
```
class Solution
{
public:
    int maxArea(vector<int>& height)
    {
        int area = 0;
        for (int i = 0; i < height.size(); ++i)
        {
            for (int j = i + 1; j < height.size(); ++j)
            {
                int low = height[i] > height[j] ? height[j] : height[i];
                int temp_area = low * (j - i);
                if (temp_area > area)
                    area = temp_area;
            }
        }
        
        return area;        
    }
};
```
时间复杂度: O(n^2).

空间复杂度: O(1).

## 解法2

要算出最大的面积,不考虑高度的情况下,肯定是长度越长,面积越大.接着,长度减小,面积是由短的那个决定的,因此,要使得到面积更大,就只需要移动短的那个高度.所以可得到下面的算法.
```
class Solution {
public:
    int maxArea(vector<int>& height) {
        int area = 0;
        int left = 0;
        int right = height.size() - 1;
        
        while(left < right)
        {
            int low = height[left] < height[right] ? height[left] : height[right];
            int temp_area = low * (right - left);
            if (temp_area > area)
                area = temp_area;
            
            if (height[left] < height[right])
                ++left;
            else
                --right;
        }
        
        return area;        
    }
};
```
时间复杂度: O(n).

空间复杂度: O(1).