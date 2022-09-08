# 剑指offer 14-1 剪绳子

问题：给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

## 思路

动态规划。通过判断 n = i 的时候，它的选取中间部分来获取最大值

```c++
class Solution {
public:
// 动态规划，空间换时间
    int cuttingRope(int n) {
        if(n == 2)
            return 1;
        if(n == 3)
            return 2;
        vector<int> dp(n+1);
        // 这里的都是不分为最大的
        dp[1] = 1;
        dp[2] = 2;
        dp[3] = 3;
        // 开始遍历
        for(int i = 4; i <= n; i++) {
            int maxValue = 0;
            for(int j = 1; j <= i/2; j++) {
                // 状态转移方程
                maxValue = max(maxValue,dp[j] * dp[i-j]);
            }
            dp[i] = maxValue;
        }
        return dp[n];
    }
};
```

