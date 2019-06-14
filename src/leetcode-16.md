# leetcode-algorithms-16 3Sum Closest

Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

Example:
```
Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

## 解法

解法同[题15](https://www.cnblogs.com/mathli/p/10008490.html)
```
class Solution
{
public:
    int threeSumClosest(vector<int>& nums, int target)
    {
        // If less then 3 elements then return their sum
        while (nums.size() <= 3)
        {
            return std::accumulate(nums.begin(), nums.end(), 0);
        }
        
        std::vector<int> v(nums.begin(), nums.end());           
        std::sort(v.begin(), v.end());
        
        int sum = 0;
        int n = v.size();
        int ans = v[0] + v[1] + v[2];
        for (int i = 0; i < n-2; i++)
        {
            int j = i + 1;
            int k = n - 1;
            while (j < k)
            {
                sum = v[i] + v[j] + v[k];
                if (abs(target - ans) > abs(target - sum))
                {
                    ans = sum;
                    if (ans == target)
                        return ans;
                }
                (sum > target) ? k-- : j++;
            }
        }
        
        return ans;
    }
};
```
空间复杂度: O(n^2).

时间复杂度: O(1)