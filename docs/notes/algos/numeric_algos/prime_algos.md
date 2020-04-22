# 质数算法

## 质数打表

**目标：**快速列出指定范围内的所有质数。

### 埃氏质数筛

算法标签：``数值`` ``模拟`` ``动态规划`` ``打表``

埃拉托斯特尼质数筛（Seive of Eratosthenes）：从第一个质数2开始在整数区间 $[2, n]$ 内进行筛选，每次筛选从区间中删除当前质数的所有倍数。筛完某个质数 $p_i$ 的倍数后，范围内的下一个未被筛除的数一定是下一个质数 $p_{i+1}$，当筛选进行到某个质数 $p_k$ 满足 $p_k^2\gt n$ 时算法结束。此后区间内所有未被筛除的数即为所有质数。

筛选质数 $p_i$ 的倍数时，可以从 $p_i^2$ 开始，不需要从 $2p_i$ 开始，因为此时从 $2p_i$ 到 $(p_i-1)p_i$ 的所有倍数都已经被小于 $p_i$ 的质数筛除。

![Seive of Eratosthenes](../../img/212_erato.jpg)

时间复杂度 $O(n\log\log{n})$，空间复杂度 $O(n)$。

缺点：当 $n\ge10^6$ 时，初期对2、3、5的倍数筛除过程耗时过长。

**算法伪码**

!!! abstract "Seive of Eratosthenes"
    $\text{EratoSeive}(P, n):$    # $P$：逻辑值序列，即质数表

    $\ \ \ \ \ \ \ \ P\leftarrow true,P[0,1]\leftarrow false$
    
    $\ \ \ \ \ \ \ \ p \leftarrow 2$

    $\ \ \ \ \ \ \ \ \text{WHILE}\ \  p^2 \le n \ \ \text{DO}:$

    $\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ k\leftarrow p^2$

    $\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \text{WHILE}\ \  k \le n \ \ \text{DO}\ \ P[k]\leftarrow false$

    $\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \text{DO}\ \ p \leftarrow p+1\ \ \text{WHILE}\ \ P[p] = false$

    $\ \ \ \ \ \ \ \ \text{RETURN}\ \ P$

优化：若数据规模极大，编程时尚可进行一定的优化以提高运行效率。

!!! tip
    1. C++语言不方便将大数组初始化为全true，可采用以下方法规避：
    ```c++
    std::vector<bool> p(n+1, true);// 方法一：使用 vector<bool> 代替数组，直接初始化为全true

    bool p[MAXN+1] = { 0 }; // 方法二：反用false和true，p[k]==true 表示k为合数，false 为质数
    ```
    2. 表中不放偶数，$P$ 的长度设置为 $n\over2$，$P[k]$ 对应 $2k+1$。

### 欧拉质数筛

