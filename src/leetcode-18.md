# leetcode-algorithms-18 4Sum

Given an array nums of n integers and an integer target, are there elements a, b, c, and d in nums such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.

Note:

The solution set must not contain duplicate quadruplets.

Example:
```
Given array nums = [1, 0, -1, 0, -2, 2], and target = 0.

A solution set is:
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

## 解法

解法同[题15](https://www.cnblogs.com/mathli/p/10008490.html)
```
class Solution
{
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target)
    {
        vector<vector<int>> r;

        sort(nums.begin(), nums.end());
        int n = nums.size();
        if (n < 4) return r;
        for (int i = 0; i < n; ++i)
        {
            int target3 = target - nums[i];
            if (target3 < 0 && nums[i] >= 0) break;
            for (int j = i + 1; j < n; ++j)
            {
                int target2 = target3 - nums[j];
                if (target2 < 0 && nums[j] >= 0) break;
                
                int front = j + 1;
                int back = n - 1;
                while(front < back)
                {
                    int two = nums[front] + nums[back];
                    
                    if (two > target2)
                        --back;
                    else if (two < target2)
                        ++front;
                    else
                    {
                        vector<int> t(4,0);
                        t[0] = nums[i];
                        t[1] = nums[j];
                        t[2] = nums[front];
                        t[3] = nums[back];
                        r.push_back(t);
                        
                        ++front; --back;                        
                        while((front < back) && nums[front] ==t[2]) ++front;
                        while((front < back) && nums[back] == t[3]) --back;
                    }
                }
                
                while (j < n  && nums[j + 1] == nums[j]) ++j;
            }
            
            while (i < n  && nums[i + 1] == nums[i]) ++i;
        }
        return r;        
    }
};
```