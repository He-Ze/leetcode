# lc50[lc16]：快速幂

## 题目

> 实现 pow(x, n) ，即计算 x 的 n 次幂函数（即，xn）。不得使用库函数，同时不需要考虑大数问题。
>
>  
>
> 示例 1：
>
> ```
> 输入：x = 2.00000, n = 10
> 输出：1024.00000
> ```
>
> 示例 2：
>
> ```
> 输入：x = 2.10000, n = 3
> 输出：9.26100
> ```
>
> 示例 3：
>
> ```
> 输入：x = 2.00000, n = -2
> 输出：0.25000
> 解释：2-2 = 1/22 = 1/4 = 0.25
> ```
>
> 
>
>
> 提示：
>
> - -100.0 < x < 100.0
> - -231 <= n <= 231-1
> - -104 <= xn <= 104
>
> 
>
> 链接：https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof

 ## 题解

### 递归

分治，二分

- 递归计算$y=x^{_[n/2_]} $向下取整
- 若n为偶数，则x^n^=y^2^ 否则x^n^=y^2^*x

```c++
class Solution {
public:
    //x为底数，n为指数
    double myPow(double x, int n) {
        long res = n;
        return n >= 0 ? quickMul(x, res) : quickMul(1.0 / x, -res);
    }
    //快速幂
    double quickMul(double x, long res) {
        if(res == 0) return 1.0;
        double y = quickMul(x, res / 2);
        return res % 2 == 0 ? y * y : y * y * x;
    }
};
```

## 迭代

将指数用二进制表示，若第i位为1，则结果*=2^i^ 

```c++
class Solution {
public:
    //x为底数，n为指数
    double myPow(double x, int n) {
        //特例判断
        if(n == 0) return 1.0;
        if(x == 0 || x == 1) return x;
        long N = n;
        //指数为负
        if(N < 0) {
            x = 1.0 / x;
            N = -N;
        }
        double res = 1.0;
        while(N > 0) {
            //这一位为1
            if(N % 2 == 1) res *= x;
            x *= x;
            N /= 2;
        }
        return res;
    }
};
```

