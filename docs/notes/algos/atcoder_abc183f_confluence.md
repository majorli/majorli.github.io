# AtCoder Beginner Contest 183F

## Confluence

---

Time Limit: 3 sec / Memory Limit: 1024 MB

### Problem Statement

$N$ students are about to go to school. Student $i$ belongs to Class $C_i$.

After leaving home, each student will head to school while repeatedly joining up with a group of other students. Once students join up with each other, they will not separate.

You will be given $Q$ queries that should be processed in order. There are two kinds of queries, in the following formats, that mean the following:

- <font color='red'>1 a b</font>: The group containing Student $a$ and the group containing Student $b$ merges. (If they are already in the same group, nothing happens.)
- <font color='red'>2 x y</font>: You are asked to find the number of students belonging to Class $y$ who are already in the same group as Student $x$ (including Student $x$) at the time of this query.

### Constraints

- $1 \le N \le 2\times10^5$
- $1 \le Q \le 2\times10^5$
- $1 \le C_i,a,b,x,y\le N$
- In a query in the format <font color='red'>1 a b</font>, $a \neq b$.
- All values in input are integers.

---

### Input

Input is given from Standard Input in the following format:

!!! info "Input"
    $N,Q$

    $C_1,\dots,C_N$

    $Query_1$

    $\vdots$

    $Query_Q$

### Output

Print the answers to the queries in the format <font color='red'>2 x y</font>, each in its own line, in order.

---

## Solution

关键在于如何快速进行队伍合并和队伍中指定班级学生人数两种查询，尽量实现 $O(1)$ 的查询，至多达到 $O(\log N)$。如果某种查询的时间复杂度达到 $O(N)$ 那么在大数据量大查询量的情况下一定会TLE。

如果要实现 $O(1)$ 级别的人数查询（2型查询），最简单的方法是为每一个队伍维护一张队伍中每个班级学生数的表，$n$ 个队伍 $m$ 个班级的话，用二维数组来维护这些数据需要 $nm$ 的数据量，极限状态下为 $4\times10^{10}$，一定会导致MLE。但是实际上由于学生人数最多为 $2\times10^5$，所以最坏情况总共的数据量也不会超过这个数字。因此可以考虑采用 ``map<int, int>`` 结构来存放这一批数据，每一个队伍一个 ``map``，key是班级号，value是这个队伍中这个班级的学生人数，不存无人的情况。这样最坏情况一次2型查询的时间复杂度为 $O(\log N)$。

然后考虑1型查询，即队伍合并的情况。如果使用线性表，例如队列、数组、链表、顺序表等数据结构来表示学生的队伍，那么队伍合并的工作量至少为 $O(N)$，显然不能满足要求。此处应该使用森林结构来表示队伍，队伍合并就是森林中树的合并，只需要以 $O(\log N)$ 效率找到两棵树的根节点，然后以 $O(1)$ 时间合并两个树根即可。这其实是一个堆归并。

接下来还要合并两个原树根的 ``map``，可以总是把较小的树向较大的树归并，假设较小的树上有 $n_1$ 个学生，较大的树有 $n_2$ 个学生，那么归并效率为 $O(n_1\log n_2)$。考虑到森林堆的特性，树的最大高度为 $\log N$，所以综合效率是很高的。

## AC Code in C++

```c++
#include <cstdio>
#include <map>
#include <vector>

using namespace std;

vector<int> cnt;	// cnt[i]: number of students in group i
vector<int> root;	// root[i]: parent node of student i
vector<map<int, int> > cls_cnt;

inline int leader(int s)
{
	while (root[s] != s) s = root[s];
	return s;
}

inline void swap(int &a, int &b)
{
	int t = a;
	a = b;
	b = t;
}

int main()
{
	int n, q;
	scanf("%d %d", &n, &q);
	cnt.resize(n+1, 1);
	root.resize(n+1);
	cls_cnt.resize(n+1);
	int t;
	for (int i = 1; i <= n; ++i) {
		root[i] = i;		// root of student i is i
		scanf("%d", &t);	// input the class of student i
		cls_cnt[i][t] = 1;	// in the group leading by student i there is 1 student of class t
	}
	int cmd, a, b;
	for (int i = 1; i <= q; ++i) {
		scanf("%d %d %d", &cmd, &a, &b);
		if (cmd == 1) {
			// find leader of groups that a and b belong to respectively
			a = leader(a);
			b = leader(b);
			if (a == b) continue;
			// before merge group (a) into group (b), make group a smaller
			// than group b so that we can always merge smaller groups into
			// larger groups
			if (cnt[a] > cnt[b]) swap(a, b);
			// link group a to group b
			cnt[b] += cnt[a];
			root[a] = b;
			// merge number of students of classes
			map<int, int>::iterator it = cls_cnt[a].begin();
			while (it != cls_cnt[a].end()) {
				cls_cnt[b][it->first] += it->second;
				++it;
			}
		} else {
			printf("%d\n", cls_cnt[leader(a)][b]);
		}
	}

	return 0;
}
```
