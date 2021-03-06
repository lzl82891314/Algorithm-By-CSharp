# 第六周学习总结

这周开始正式学习动态规划的内容，也是我觉得算法课程里最精妙也是最难得一个部分。

很早以前就接触过01背包问题，当时还有一个专栏叫背包九讲，当时看的真是云里雾里，就感觉DP的内容好高大上，但是自己完全没有掌握过，通过这周的学习，终于发现DP其实也没有那么神秘。

## 基础知识回顾

DP其实应该翻译为`动态递推`，其根本核心也是在`解决重复子问题`，而相较于递归和分治，DP存在`最优子结构`，一般是通过一个状态数组进行存储每一步的最优子结构，并淘汰其余结果。

动态规划相较于递归和分治：

* 共性： 找到重复子问题
* 差异：最优子结构，可以淘汰其余解

在实现上，递归和分治一般的解法都是`自顶向下`进行递归，先计算最顶层，然后逐层递归下层，最终计算结果，比如斐波那契数列问题：

``` C#
private int func(int n) {
    // 自顶向下，如果计算func(5)，转而计算func(3) + func(4)
    return func(n-1) + func(n-2);
}
```

而DP则不同，DP一般是`自底向上`进行递推，同样的斐波那契数列问题，DP就是先进行了初始化计算，然后逐层递推，最终的递推结果就是问题的答案：

``` C#
private int func(int n) {
    var dp = new int[n];
    // 定义初始化状态
    dp[0] = 1; dp[1] = 1;
    for (var i = 2; i < n; i++) {
        // 自底向上逐层递推
        dp[i] = dp[i-1] + dp[i-2];
    }
    return dp[n-1];
}
```

所以DP的难点其实是思维的转换，需要从`要计算f(n)那么我们只需要计算f(n-1)然后递归求解`这种递归的形式转换为`要计算f(n)那么我们只需计算f(1)然后推导f(n)`。

上述提到的`f(1)到f(n)`的推导，在DP中会被称为`状态转移方程`，或者叫`DP方程`。斐波那契数列的问题的DP方程就是最简单的`dp[i] = dp[i-1] + dp[i-2]`。而越复杂的问题其DP的方程越难找到和定义。