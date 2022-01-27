# lc1：两数之和

## 题目

> 给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出`和`为目标值 target  的那两个整数，并返回它们的数组下标。
>
> 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。
>
> 你可以按任意顺序返回答案。
>
>  
>
> 示例 1：
>
> ```
> 输入：nums = [2,7,11,15], target = 9
> 输出：[0,1]
> 解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
> ```
>
> 示例 2：
>
> ```
> 输入：nums = [3,2,4], target = 6
> 输出：[1,2]
> ```
>
> 示例 3：
>
> ```
> 输入：nums = [3,3], target = 6
> 输出：[0,1]
> ```
>
> 
>
>
> 提示：
>
> - 2 <= nums.length <= 10^4^
> - -10^9^ <= nums[i] <= 10^9^
> - -10^9^ <= target <= 10^9^
> - 只会存在一个有效答案
>
> 进阶：你可以想出一个时间复杂度小于 O(n^2^) 的算法吗？
>
> 
>
> 链接：https://leetcode-cn.com/problems/two-sum

## 题解

暴力法就是两层循环，遍历所有的二元组合，优化方法就是使用哈希表，首先遍历一遍数组，把所有的数字加进map，关键字是数组的值，键值则是该值在数组中的序号，建立完哈希表后只需要再遍历一遍，对于数组中的每个值a，如果`target-a`在哈希表中并且`target-a`并不是自己的话（排除`target=2a`，而数组中只有一个a的这种情况），就返回这个解。

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int,int> a;
        int i;
        //建立哈希表
        for(i=0;i<nums.size();i++){
            a[nums[i]]=i;
        }
        for(i=0;i<nums.size();i++){
            //目标值在哈希表中并且不是自己
            if(a[target-nums[i]]&&a[target-nums[i]]!=i)
                return vector<int>{i,a[target-nums[i]]};
        }
        return vector<int>{i,a[target-nums[i]]};
    }
};
```

