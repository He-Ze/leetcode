# lc5：最长回文子串

## 题目

> 给你一个字符串 s，找到 s 中最长的回文子串。
>
>  
>
> 示例 1：
>
> ```
> 输入：s = "babad"
> 输出："bab"
> 解释："aba" 同样是符合题意的答案。
> ```
>
> 示例 2：
>
> ```
> 输入：s = "cbbd"
> 输出："bb"
> ```
>
> 示例 3：
>
> ```
> 输入：s = "a"
> 输出："a"
> ```
>
> 示例 4：
>
> ```
> 输入：s = "ac"
> 输出："a"
> ```
>
> 
>
>
> 提示：
>
> - 1 <= s.length <= 1000
> - s 仅由数字和英文字母（大写和/或小写）组成
>
> 
>
> 链接：https://leetcode-cn.com/problems/longest-palindromic-substring

## 题解

“中心扩展法”，既然要求回文子串，那么就可以以每个字母作为回文中心，向两侧扩展（两侧相同则继续扩展，否则结束），在扩展时有两种边界情况，即以一个字母为扩展中心和以两个字母为扩展中心，都遍历即可，最后得到以每一个扩展中心为中心的子串，取最长的那一个即可。

```c++
class Solution {
public:
    //扩展函数，输入当前扩展中心的左右序号，返回以这个中心的回文子串的前后序号
    pair<int,int> expand(string& s,int left, int right){
        //左右都不超范围且左右相等（符合回文）则继续扩展
        while(left>=0  && right<s.size() && s[left]==s[right]){
            left--;
            right++;
        }
        return {left+1,right-1};
    }
    //主函数
    string longestPalindrome(string s) {
        int left=0,right=0;    //存储当前最长的回文子串的起点和终点
        for(int i=0;i<s.size();i++){
            auto [l1,r1]=expand(s,i,i);    //以一个字母为扩展中心
            auto [l2,r2]=expand(s,i,i+1);  //以两个字母为扩展中心
            //判断是否比当前更长
            if(r1-l1>right-left){
                left=l1;
                right=r1;
            }
            if(r2-l2>right-left){
                left=l2;
                right=r2;
            }
        }
        //substr有两个参数，起点和长度
        return s.substr(left, right - left + 1);
    }
};
```

