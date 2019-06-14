# leetcode-algorithms-4 Median of Two Sorted Arrays

There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume nums1 and nums2 cannot be both empty.

Example 1:
```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```
Example 2:
```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

## 解法

```
    left        |     right
a[0] ... a[i-1] | a[i] ... a[m]
b[0] ... b[j-1] | b[j] ... b[n]
```
对于两个数组,如上所示,保证max(left) <= min(right)同时左边数的个数为中位数个数即(m+n+1)/2.就可以找到中位数的值.

可先取a数组i = m/2,那j = mid(中位数) - i;如果a[i - 1]大于b[j]不能保证max(left) <= min(right)就需要把a的扣掉一个,b[j - 1]和a[i]也是一样的情况.当上面两种都不符合时,就说明已经找到中位数的位置.
```
class Solution
{
public:
     double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2)
     {
        int l1 = nums1.size();
        int l2 = nums2.size();
        int l = l1 + l2;
        if (l1 > l2)
        {
            nums1.swap(nums2);
            l1 = l - l1;
            l2 = l - l1;            
        }  
  
        int mid = (l + 1) / 2;
        int min = 0;
        int max = l1;
        while(min <= max)
        {
            int i = (min + max) / 2;
            int j = mid - i;
            if (i < max && nums2[j - 1] > nums1[i])
                min = i + 1;
            else if (i > min && nums1[i - 1] > nums2[j])
                max = i - 1;
            else
            {
                int left = 0;
                if (i == 0)
                    left = nums2[j - 1];
                else if (j == 0)
                    left = nums1[i - 1];
                else
                    left = nums2[j - 1] > nums1[i - 1] ? nums2[j - 1] : nums1[i - 1];
                if (l % 2 != 0)
                    return left;
                
                int right = 0;
                if (i == l1)
                    right = nums2[j];
                else if (j == l2)
                    right = nums1[i];
                else
                    right = nums2[j] > nums1[i] ? nums1[i] : nums2[j];
                
                return double(left + right) / 2.0;                   
            }            
        }
        return 0.0;
    }
};
```
时间复杂度: O(log(m+n)).
空间复杂度: O(1).