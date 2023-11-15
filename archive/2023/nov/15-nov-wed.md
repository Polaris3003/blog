# 15 Nov - Wed

Today's stuff

<table data-header-hidden><thead><tr><th width="80" data-type="checkbox"></th><th width="120" data-type="select" data-multiple>Type</th><th>Action</th></tr></thead><tbody><tr><td>true</td><td></td><td>leetcode</td></tr><tr><td>false</td><td></td><td>6.824 zookeeper</td></tr><tr><td>false</td><td></td><td>0x3f tea</td></tr><tr><td>false</td><td></td><td>algorithm</td></tr><tr><td>false</td><td></td><td>日本語のstudy</td></tr><tr><td>false</td><td></td><td>xiaolin coding</td></tr></tbody></table>

## Notes & ideas

<details>

<summary>leetcode</summary>

1\. (打卡 1) [407 \[接雨水 II\]](https://leetcode.cn/problems/trapping-rain-water-ii/description/) 🤩

😢希望这次能真的搞懂接雨水

<mark style="color:blue;">**题目描述：**</mark>

<img src="../../../.gitbook/assets/image.png" alt="" data-size="original">

<mark style="color:purple;">题解：</mark>

首先最外围是无法接水的 能接到水的方块是自身的高度比其上下左右四个相邻的方块接水后的高度都要低的

![](<../../../.gitbook/assets/image (3).png>)

根据木桶原理，接到的雨水的高度由这个容器周围最短的木板来确定的。我们可以知道容器内水的高度取决于最外层高度最低的方块

![](<../../../.gitbook/assets/image (2).png>)

我们假设已经知道最外层的方块接水后的高度的最小值，则此时我们根据木桶原理，肯定可以确定最小高度方块的相邻方块的接水高度。我们同时更新最外层的方块标记，我们在新的最外层的方块再次找到接水后的高度的最小值，同时确定与其相邻的方块的接水高度

![](<../../../.gitbook/assets/image (4).png>)

然后再次更新最外层，依次迭代直到求出所有的方块的接水高度，即可知道矩阵中的接水容量。

复杂度分析

时间复杂度：O(MNlog⁡(MN))，其中 M 是矩阵的行数，N 是矩阵的列数。我们需要将矩阵中的每个元素都进行遍历，同时将每个元素都需要插入到优先队列中，总共需要向队列中插入 MN 个元素，因此队列中最多有 MN 个元素，每次堆进行调整的时间复杂度为 O(log⁡(MN))，因此总的时间复杂度为 O(MNlog⁡(MN))。

空间复杂度：O(MN)，其中 M 是矩阵的行数，N 是矩阵的列数。我们需要创建额外的空间对元素进行标记，优先队列中最多存储 O(MN) 个元素，因此空间复杂度为 O(MN)。

代码以后碰到了自己再写一遍补上来（）\
2\. (打卡 2) [882 \[细分图中的可到达节点\]](https://leetcode.cn/problems/reachable-nodes-in-subdivided-graph/description/) 🤩

题目描述：

![](<../../../.gitbook/assets/image (5).png>)

题解：

直接抄灵神的了hhh 一些dij还是不太会 明明都知道原理 但是就是写不出来 可能还是码量少了

![](<../../../.gitbook/assets/image (6).png>)



<mark style="color:blue;">代码：</mark>

{% code overflow="wrap" %}
```
class Solution {
    // Dijkstra 算法模板
    // 返回从 start 到每个点的最短路
    vector<int> dijkstra(vector<vector<pair<int, int>>> &g, int start) {
        vector<int> dist(g.size(), INT_MAX);
        dist[start] = 0;
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> pq;
        pq.emplace(0, start);
        while (!pq.empty()) {
            auto[d, x] = pq.top();
            pq.pop();
            if (d > dist[x]) continue;
            for (auto[y, wt] : g[x]) {
                int new_d = dist[x] + wt;
                if (new_d < dist[y]) {
                    dist[y] = new_d;
                    pq.emplace(new_d, y);
                }
            }
        }
        return dist;
    }

public:
    int reachableNodes(vector<vector<int>> &edges, int maxMoves, int n) {
        vector<vector<pair<int, int>>> g(n);
        for (auto &e: edges) {
            int u = e[0], v = e[1], cnt = e[2];
            g[u].emplace_back(v, cnt + 1);
            g[v].emplace_back(u, cnt + 1); // 建图
        }

        auto dist = dijkstra(g, 0); // 从 0 出发的最短路

        int ans = 0;
        for (int d : dist)
            if (d <= maxMoves) // 这个点可以在 maxMoves 步内到达
                ++ans;
        for (auto &e: edges) {
            int u = e[0], v = e[1], cnt = e[2];
            int a = max(maxMoves - dist[u], 0);
            int b = max(maxMoves - dist[v], 0);
            ans += min(a + b, cnt); // 这条边上可以到达的节点数
        }
        return ans;
    }
};
```
{% endcode %}

\
3\. (每日)[ 2656 \[K 个元素的最大和\] ](https://leetcode.cn/problems/maximum-sum-with-exactly-k-elements/description/?envType=daily-question\&envId=2023-11-15)

这个秒 找到最大值一直用就好了

</details>

<details>

<summary>tea</summary>

[https://codeforces.com/problemset/problem/1861/C](https://codeforces.com/problemset/problem/1861/C)

输入 T(≤1e4) 表示 T 组数据。所有数据的字符串长度之和 ≤2e5。 每组数据长度 ≤2e5 的字符串 s，只包含 + - 1 0 四种字符。

一开始你有一个空栈 t。 从左到右遍历 s： 遇到 +，入栈一个元素，大小未知。 遇到 -，弹出栈顶元素，输入保证此时栈非空。 遇到 1，说明此时从栈底到栈顶，一定是递增的，即一定满足 t\[0] <= t\[1] <= ... 遇到 0，说明此时从栈底到栈顶，一定不是递增的，即一定不满足 t\[0] <= t\[1] <= ... 如果 1 和 0 的描述一定矛盾，输出 NO，否则输出 YES。 注：大小不足 2 的栈是递增的。

input

```
7
++1
+++1--0
+0
0
++0-+1-+0
++0+-1+-0
+1-+0
```

output

<pre><code><strong>YES
</strong>NO
NO
NO
YES
NO
</code></pre>

<mark style="color:red;">**难度：1600**</mark>

提示 1 对于 ...0++0++0，后面两个 0 都是无效信息，因为第一个 0 已经告诉我们栈是无序的了，所以只需要知道【最短】的无序长度，记作 unsortedSize。（初始值为 inf） 特别地，如果当前栈长度缩短至 < unsortedSize，那么 unsortedSize 信息作废，更新为 inf。 遇到 1 时，如果当前栈长度 >= unsortedSize，说明栈包含了一段无序元素，矛盾，直接输出 NO。

提示 2 对于 ...1..1..1，无论中间的 .. 是 + 还是 -，前面两个 1 都是无效信息，我们只需要知道【最新】的有序长度，记作 sortedSize。 特别地，如果当前栈长度缩短至 < sortedSize，那么更新 sortedSize 为当前栈长度。 遇到 0 时，如果当前栈长度 <= sortedSize（或者当前栈长度不足 2），说明整个栈其实是有序的，矛盾，直接输出 NO。

[https://codeforces.com/problemset/submission/1861/231953477](https://codeforces.com/problemset/submission/1861/231953477)

<mark style="color:purple;">解：</mark>

```go
package main

import (
	"bufio"
	. "fmt"
	"io"
	"math"
	"os"
)

func CF1861C(_r io.Reader, _w io.Writer) {
	in := bufio.NewReader(_r)
	out := bufio.NewWriter(_w)
	defer out.Flush()

	T, s := 0, ""
o:
	for Fscan(in, &T); T > 0; T-- {
		Fscan(in, &s)
		curSize := 0
		sortedSize := 1
		unsortedSize := math.MaxInt
		for _, b := range s {
			if b == '+' {
				curSize++
			} else if b == '-' {
				curSize--
				if curSize < unsortedSize {
					unsortedSize = math.MaxInt // 后面 s[i]='1' 是可以的
				}
				if curSize < sortedSize {
					sortedSize = max(curSize, 1)
				}
			} else if b == '0' {
				if curSize <= sortedSize {
					Fprintln(out, "NO")
					continue o
				}
				unsortedSize = min(unsortedSize, curSize)
			} else {
				if curSize >= unsortedSize {
					Fprintln(out, "NO")
					continue o
				}
				sortedSize = max(curSize, 1)
			}
		}
		Fprintln(out, "YES")
	}
}
func main() { CF1861C(os.Stdin, os.Stdout) }
func min(a, b int) int {
	if b < a {
		return b
	}
	return a
}
func max(a, b int) int {
	if b > a {
		return b
	}
	return a
}
```

</details>

<details>

<summary><a href="https://pdos.csail.mit.edu/6.824/papers/zookeeper.pdf">6.824 zookeeper</a></summary>

今天看了点线性一致方面的东西 然后重要的就是zookeeper是将所有的写请求通过leader下发，将读请求发送给某一个副本 因为现实世界中 大量的负载是读请求 增加了zookeeper现实的可用性

\
**question:**

如果我们直接将客户端的请求发送给副本，我们能得到预期的结果吗？因为可能有很多原因会导致副本的数据不是up to date的 所以可能会读到一个旧的数据

**answer:**

实际上，Zookeeper并不要求返回最新的写入数据。Zookeeper的方式是，放弃线性一致性。它对于这里问题的解决方法是，不提供线性一致的读。所以，因此，Zookeeper也不用为读请求提供最新的数据。它有自己有关一致性的定义，而这个定义不是线性一致的，因此允许为读请求返回旧的数据。所以，Zookeeper这里声明，自己最开始就不支持线性一致性，来解决这里的技术问题。如果不提供这个能力，那么（为读请求返回旧数据）就不是一个bug。这实际上是一种经典的解决性能和强一致之间矛盾的方法，也就是不提供强一致。

然而，我们必须考虑这个问题，如果系统不提供线性一致性，那么系统是否还可用？客户端发送了一个读请求，但是并没有得到当前的正确数据，也就是最新的数据，那我们为什么要相信这个系统是可用的？我们接下来看一下这个问题。

在这之前，还有问题吗？Zookeeper的确允许客户端将读请求发送给任意副本，并由副本根据自己的状态来响应读请求。副本的Log可能并没有拥有最新的条目，所以尽管系统中可能有一些更新的数据，这个副本可能还是会返回旧的数据。这就来到了一致性保证的问题

</details>

<details>

<summary>algorithm</summary>



今日dij模板

<pre class="language-cpp"><code class="lang-cpp">返回从 start 到每个点的最短路
<strong>vector&#x3C;int> dijkstra(vector&#x3C;vector&#x3C;pair&#x3C;int, int>>> &#x26;g, int start) {
</strong>        vector&#x3C;int> dist(g.size(), INT_MAX);
        dist[start] = 0;
        priority_queue&#x3C;pair&#x3C;int, int>, vector&#x3C;pair&#x3C;int, int>>, greater&#x3C;>> pq; 
        pq.emplace(0, start);
        while (!pq.empty()) {
            auto[d, x] = pq.top(); //从0开始
            pq.pop();
            if (d > dist[x]) continue;
            for (auto[y, wt] : g[x]) {
                int new_d = dist[x] + wt;
                if (new_d &#x3C; dist[y]) {
                    dist[y] = new_d;
                    pq.emplace(new_d, y);
                }
            }
        }
        return dist;
    }
</code></pre>

思想:

将节点分成两个集合：已确定最短路长度的点集S和为确定最短路长度的点集T，一开始全部节点都属于T集合

初始化dis(s)=0，其他点的dis均为max

然后重复这些操作：

1.从T集合中，选取一个最短路长度最小的节点，移到S集合中。

2.对哪些刚刚被加入S集合的节点的所有出边执行松弛操作

直到T集合为空，算法结束

#### 时间复杂度

有多种方法来维护 1 操作中最短路长度最小的结点，不同的实现导致了 Dijkstra 算法时间复杂度上的差异。

1. 暴力：不用任何数据结构维护 直接遍历找最短路长度最小的节点。<mark style="color:red;">O(n^2)</mark>
2. 二叉堆：直接取堆顶节点即可，m次插入操作，n次删除堆顶操作，删除和插入时间复杂度都为logn，<mark style="color:red;">O(mlogn)</mark>
3. 优先队列：和二叉堆是差不多的，但使用优先队列时，如果同一个点的最短路被更新多次，因为先前更新时插入的元素不能被删除，也不能被修改，只能留在优先队列中，故优先队列内的元素个数是O(m)的<mark style="color:red;">,O(mlogn)</mark>
4. Fibonacci堆：没了解过 可能不太用得上
5. 线段树：和二叉堆类似，<mark style="color:red;">O(mlogn)</mark>

在稀疏图中，![](data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)m=O(n)，使用二叉堆实现的 Dijkstra 算法较 Bellman–Ford 算法具有较大的效率优势；而在稠密图中，m=O(n^2)，这时候使用暴力做法较二叉堆实现更优。

</details>

<details>

<summary>xiaolin coding</summary>

呃 其实看过一遍了 但是忘得有点快 就从新开始再过一遍

</details>

<details>

<summary>日本語のstudy</summary>

希望有时间能学。。每天抽出个十几二十分钟试试

</details>

## How was the day?

<details>

<summary>🧠 Mood tracking</summary>

Not so bad?😢Trying to find some new songs for relax

</details>

<details>

<summary>💡 Observations</summary>

Brain is a little rusty.... and too lazy

</details>

{% hint style="info" %}
**GitBook tip:** Use the **rating** column in a table to build a super simple habit-tracking section.
{% endhint %}

<table data-header-hidden><thead><tr><th width="120" data-type="rating" data-max="5"></th><th>Task</th></tr></thead><tbody><tr><td>3</td><td>Sleep</td></tr><tr><td>3</td><td>Work/life balance</td></tr><tr><td>3</td><td>Creativity</td></tr><tr><td>3</td><td>Fitness</td></tr></tbody></table>
