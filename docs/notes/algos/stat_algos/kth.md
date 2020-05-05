# k位数与中位数

此处所述k位数，指一个序列中第k小的数。

给定序列 $A[0:n]$，非负整数 $0 \le k \lt n$，若对 $A[0:n]$ 进行升序排序，则k位数等于排完序后的 $A[k-1]$。

此处所述中位数，指统计意义上的中位数，即能将序列分为元素数量相等的前后两部分，使得前一部分的所有数小于等于中位数，后一部分的所有数大于等于中位数的那个数。

给定序列 $A[0:n]$，若对其进行升序排序，则中位数等于：

$$
median=\begin{cases}
A[k-1]&,n=2k-1\\
(A[k-1]+A[k])/2&,n=2k
\end{cases},k=1,2,\dots
$$

现要在不排序的条件下，以比排序更快的速度获取k位数和中位数。

## 序列分区

序列分区是快速排序的基本操作，可用来实现快速地k位数和中位数算法。

**目标：**在序列中选择一个元素作为基准，以该基准值为中心将序列分为前后两部分，前一部分所有元素小于等于基准值，后一部分所有元素大于等于基准值。

序列分区有两种常见方法，一种为基于选择的分区，中文网站和教程较为常用此方法；另一种为基于冒泡的分区，《算法导论》一书使用该方法，国外网站和教程较为常用此方法。二者都完成对子序列 $A[l:r]$ 进行分区的操作，并返回分区后基准值元素所在的位置 $p$。

### 基于选择的序列分区

给定子序列 $A[l:r]$，使用首元素为基准进行分区。分区时，先从右向左扫描寻找第一个小于基准值的元素，并将其交换到序列前部，然后从左到右扫描第一个大于等于基准值的元素并将其交换到序列后部，如此不断循环直到整个序列扫描完毕。

此算法在网上和算法教程中随处可见，此处不再详细描述，下面是算法的伪码。

时间复杂度 $O(n)$，空间复杂度 $O(1)$。

**算法伪码**

!!! abstract "Algorithm: Partition by Selection"
    // $A$：待分区序列；$l, r$：子序列左右端点，左闭右开

    $\text{PartitionBySelection}(A, l, r):$

    $\ \ \ \ \ \ \ \ pivot \leftarrow A[l],i\leftarrow l,j\leftarrow r-1$

    $\ \ \ \ \ \ \ \ \text{WHILE}\ \ i \lt j\ \ \text{DO}:$

    $\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \text{WHILE}\ \ i \lt j\ \ \text{and}\ \ A[j] \ge pivot\ \ \text{DO}\ \ j \leftarrow j-1$ 

    $\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \text{IF}\ \ i \lt j\ \ \text{THEN}\ \ A[i] \leftarrow A[j], i \leftarrow i+1$

    $\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \text{WHILE}\ \ i \lt j\ \ \text{and}\ \ A[i] \lt pivot\ \ \text{DO}\ \ i \leftarrow i+1$ 

    $\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \text{IF}\ \ i \lt j\ \ \text{THEN}\ \ A[j] \leftarrow A[i], j \leftarrow j-1$

    $\ \ \ \ \ \ \ \ A[i]\leftarrow pivot$

    $\ \ \ \ \ \ \ \ \text{RETURN}\ \ i$


### 基于冒泡的序列分区

给定子序列 $A[l:r]$，使用尾元素为基准进行分区。分区时将整个子序列分为三部分，从左到右依次为小于基准值的部分、大于基准值的部分和尚未划分的部分。初始时前两部分长度均为0，随后从左到右扫描第三部分中的每一个元素并根据其值划分到应在的部分中去。

此算法在网上和算法教程中随处可见，此处不再详细描述，下面是算法的伪码。

时间复杂度 $O(n)$，空间复杂度 $O(1)$。

**算法伪码**

!!! abstract "Algorithm: Partition by Bubble"
    // $A$：待分区序列；$l, r$：子序列左右端点，左闭右开

    $\text{PartitionByBubble}(A,l,r):$

    $\ \ \ \ \ \ \ \ i\leftarrow l,last\leftarrow r-1,pivot\leftarrow A[last]$

    $\ \ \ \ \ \ \ \ \text{FOR}\ \ j \leftarrow i\ \ \text{TO}\ \ last-1\ \ \text{DO}:$

    $\ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \ \text{IF}\ \  A[j] \lt pivot\ \ \text{THEN}\ \ \text{Swap}(A[i],A[j]),i\leftarrow i+1$

    $\ \ \ \ \ \ \ \ A[last]\leftarrow A[i]$

    $\ \ \ \ \ \ \ \ A[i]\leftarrow pivot$

    $\ \ \ \ \ \ \ \ \text{RETURN}\ \ i$


## 分区k位数算法

## 分区中位数算法

## 锦标赛算法

## 两个有序序列的中位数

### 模拟归并

### 二分查找
