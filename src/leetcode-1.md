# leetcode-algorithms-1 two sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## 解法1

直接对数组进行两个循环匹配,相等返回.

```
class Solution
{
public:
    vector<int> twoSum(vector<int>& nums, int target)
    {
        vector<int> t;
        for (int one = 0; one < nums.size() - 1; ++one)
        {
            for (int two = one + 1; two < nums.size(); ++two)
            {
                if (nums[one] + nums[two] == target)
                {
                    t.push_back(one);
                    t.push_back(two);
                    return t;
                }
            }
        }
        return t;
    }
};
```

时间复杂度: 两个循环都是n个元素遍历,即O($n^2$).

空间复杂度: O(1).

##解法2

```
class Solution
{
public:
    vector<int> twoSum(vector<int>& nums, int target)
    {
        vector<int> t;
        std::unordered_map<int,int> m;
        for (int one = 0; one < nums.size(); ++one)
        {
            int result = target - nums[one];            
            auto fiter = m.find(result);
            if (fiter != m.end())
            {
                t.push_back(fiter->second);
                t.push_back(one);
                return t;
            }
            m[nums[one]] = one;
        }
        return t;
    }
};
```

时间复杂度: 一个循环加上一个查找,由于unordered_map是hash实现,其查找效率O(1),所以最后的复杂度O(n).

空间复杂度: O(n).