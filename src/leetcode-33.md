# leetcode-algorithms-33  Search in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).

Example 1:
```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```
Example 2:
```
Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

##解法

要找到一个值,其效率为O(logn),就需要使用二分查找,二分查找是要求要有序的.现在先来看nums=[4,5,6,7,0,1,2],target=5这组数字,我们可看成是[4,5,6,7,inf,inf,inf]于是就变成了有序,同时对于nums=[4,5,6,7,0,1,2],target=1,可看成是[-inf,-inf,-inf,-inf,0,1,2]同样变成有序.接下来只要二分查找即可.
```
class Solution
{
public:
    int search(vector<int>& nums, int target)
    {
        int low = 0;
        int high = nums.size();
        while (low < high)
        {
            int mid = (low + high) / 2;

            double num = (nums[mid] < nums[0]) == (target < nums[0])
                       ? nums[mid]
                       : (target < nums[0] ? -INFINITY : INFINITY);

            if (num < target)
                low = mid + 1;
            else if (num > target)
                high = mid;
            else
                return mid;
        }
        return -1;        
    }
};
```