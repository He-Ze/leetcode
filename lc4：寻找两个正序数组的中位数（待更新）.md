# lc4：寻找两个正序数组的中位数（待更新）

## 题目

> 给定两个大小分别为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。请你找出并返回这两个正序数组的 中位数 。
>
> 算法的时间复杂度应该为 O(log (m+n)) 。
>
>  
>
> 示例 1：
>
> ```
> 输入：nums1 = [1,3], nums2 = [2]
> 输出：2.00000
> 解释：合并数组 = [1,2,3] ，中位数 2
> ```
>
> 示例 2：
>
> ```
> 输入：nums1 = [1,2], nums2 = [3,4]
> 输出：2.50000
> 解释：合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
> ```
>
> 示例 3：
>
> ```
> 输入：nums1 = [0,0], nums2 = [0,0]
> 输出：0.00000
> ```
>
> 示例 4：
>
> ```
> 输入：nums1 = [], nums2 = [1]
> 输出：1.00000
> ```
>
> 示例 5：
>
> ```
> 输入：nums1 = [2], nums2 = []
> 输出：2.00000
> ```
>
> 
>
>
> 提示：
>
> - nums1.length == m
> - nums2.length == n
> - 0 <= m <= 1000
> - 0 <= n <= 1000
> - 1 <= m + n <= 2000
> - -106 <= nums1[i], nums2[i] <= 106
>
> 
>
> 链接：https://leetcode-cn.com/problems/median-of-two-sorted-arrays

## 题解

第一个想法就是暴力，把两个数组合并后排序，然后直接取中位数

```c++
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int l1=nums1.size();
        int l2=nums2.size();
        int l=l1+l2;
        vector<int> nums;
        //合并
        for(int i=0;i<l1;i++){
            nums.push_back(nums1[i]);
        }
        for(int i=0;i<l2;i++){
            nums.push_back(nums2[i]);
        }
        //排序
        sort(nums.begin(),nums.end());
        //取中位数
        if(l%2==0) return (nums[l/2-1]+nums[l/2])/2.0;//注意此处要除2.0而不是2，否则返回结果为int不是float
        else return nums[(l+1)/2-1];
    }
};
```

接下来可以优化，但这是个困难题，等以后再更（不知道何年何月，咕咕