# leetcode-algorithms-34  Find First and Last Position of Element in Sorted Array

Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

Example 1:
```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```
Example 2:
```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

## 解法

二分法查找
```
class Solution
{
public:
    vector<int> searchRange(vector<int>& nums, int target)
    {
        vector<int> target_pos(2, -1);
        int min = 0;
        int max = nums.size() - 1;
        int mid = 0;
        int t = 0;
        while(min <= max)
        {
            mid = (min + max) / 2;
            t = nums[mid];
            if (t == target)
            {
                target_pos.clear();                
                int pre = mid - 1;
                bool have = false;
                while(pre >= min && nums[pre] == target)
                {
                    have = true;
                    --pre;
                }
                if (have) target_pos.push_back(++pre);
                else target_pos.push_back(mid);
                have = false;
                pre = mid + 1;
                while (pre <= max && nums[pre] == target)
                {
                    have = true;
                    ++pre;
                }
                if (have) target_pos.push_back(--pre);
                else target_pos.push_back(mid);
                break;
            }
            else if (t > target)
            {
                max = mid - 1;
            }
            else
            {
                min = mid + 1;
            }
        }
        return target_pos;
    }
};
```
时间复杂度: O(logn).

空间复杂度: O(1).
