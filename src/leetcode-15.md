# leetcode-algorithms-15 3Sum

Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note:

The solution set must not contain duplicate triplets.

Example:
```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

## 解法

对于a+b+c=0,只要求b+c=-a.定义第一个数为-a.其它两数相加和为a就是要的结果.
```
class Solution
{
public:
    vector<vector<int>> threeSum(vector<int>& nums)
    {
        std::sort(nums.begin(), nums.end());
        std::vector<vector<int> > res;
        
        int len = nums.size();
        for (int i = 0; i < len; ++i)
        {
            int target = -nums[i];
            int front = i + 1;
            int back = len - 1;
            while(front < back)
            {
                int sum = nums[front] + nums[back];
                if (target < sum)
                    --back;
                else if (target > sum)
                    ++front;
                else
                {
                    std::vector<int> v(3);
                    v[0] = nums[i];
                    v[1] = nums[front];
                    v[2] = nums[back];
                    res.push_back(v);
                    
                    //去掉前置重复
                    while (front < back && nums[front] == v[1]) ++front;
                    
                    //去掉后置重复
                    while (front < back && nums[back] == v[2]) --back;                    
                }
            }
            
            //去掉target重复
            while(nums[i + 1] == nums[i]) ++i;
        }
        
        return res;
    }
};
```
时间复杂度: O(n^2).
空间复杂度: O(1).