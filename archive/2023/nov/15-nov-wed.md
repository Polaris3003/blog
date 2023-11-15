# 15 Nov - Wed

## Today's stuff

<table data-header-hidden><thead><tr><th width="80" data-type="checkbox"></th><th width="120" data-type="select" data-multiple>Type</th><th>Action</th></tr></thead><tbody><tr><td>false</td><td></td><td>leetcode</td></tr><tr><td>false</td><td></td><td>6.824 zookeeper</td></tr><tr><td>false</td><td></td><td>0x3f tea</td></tr><tr><td>false</td><td></td><td>algorithm</td></tr><tr><td>false</td><td></td><td>日本語のstudy</td></tr><tr><td>false</td><td></td><td>xiaolin coding</td></tr></tbody></table>

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

空间复杂度：O(MN)，其中 M 是矩阵的行数，N 是矩阵的列数。我们需要创建额外的空间对元素进行标记，优先队列中最多存储 O(MN) 个元素，因此空间复杂度为 O(MN)。\
2\. (打卡 2) [882 \[细分图中的可到达节点\]](https://leetcode.cn/problems/reachable-nodes-in-subdivided-graph/description/) 🤩

题目描述：

![](<../../../.gitbook/assets/image (5).png>)

题解：

直接抄灵神的了hhh 一些dij还是不太会 明明都知道原理 但是就是写不出来 可能还是码量少了

![](<../../../.gitbook/assets/image (6).png>)

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

</details>

<details>

<summary>6.824 zookeeper</summary>

1\. (打卡 1) [407 \[接雨水 II\]](https://leetcode.cn/problems/trapping-rain-water-ii/description/) 🤩\
2\. (打卡 2) [882 \[细分图中的可到达节点\]](https://leetcode.cn/problems/reachable-nodes-in-subdivided-graph/description/) 🤩\
3\. (每日)[ 2656 \[K 个元素的最大和\] ](https://leetcode.cn/problems/maximum-sum-with-exactly-k-elements/description/?envType=daily-question\&envId=2023-11-15)

</details>

<details>

<summary>algorithm</summary>

1\. (打卡 1) [407 \[接雨水 II\]](https://leetcode.cn/problems/trapping-rain-water-ii/description/) 🤩\
2\. (打卡 2) [882 \[细分图中的可到达节点\]](https://leetcode.cn/problems/reachable-nodes-in-subdivided-graph/description/) 🤩\
3\. (每日)[ 2656 \[K 个元素的最大和\] ](https://leetcode.cn/problems/maximum-sum-with-exactly-k-elements/description/?envType=daily-question\&envId=2023-11-15)

</details>

<details>

<summary>xiaolin coding</summary>

1\. (打卡 1) [407 \[接雨水 II\]](https://leetcode.cn/problems/trapping-rain-water-ii/description/) 🤩\
2\. (打卡 2) [882 \[细分图中的可到达节点\]](https://leetcode.cn/problems/reachable-nodes-in-subdivided-graph/description/) 🤩\
3\. (每日)[ 2656 \[K 个元素的最大和\] ](https://leetcode.cn/problems/maximum-sum-with-exactly-k-elements/description/?envType=daily-question\&envId=2023-11-15)

</details>

<details>

<summary>日本語のstudy</summary>

1\. (打卡 1) [407 \[接雨水 II\]](https://leetcode.cn/problems/trapping-rain-water-ii/description/) 🤩\
2\. (打卡 2) [882 \[细分图中的可到达节点\]](https://leetcode.cn/problems/reachable-nodes-in-subdivided-graph/description/) 🤩\
3\. (每日)[ 2656 \[K 个元素的最大和\] ](https://leetcode.cn/problems/maximum-sum-with-exactly-k-elements/description/?envType=daily-question\&envId=2023-11-15)

</details>

## How was the day?

<details>

<summary>🧠 Mood tracking</summary>

Start taking notes…

</details>

<details>

<summary>💡 Observations</summary>

Start taking notes…

</details>

{% hint style="info" %}
**GitBook tip:** Use the **rating** column in a table to build a super simple habit-tracking section.
{% endhint %}

<table data-header-hidden><thead><tr><th width="120" data-type="rating" data-max="5"></th><th>Task</th></tr></thead><tbody><tr><td>3</td><td>Sleep</td></tr><tr><td>3</td><td>Work/life balance</td></tr><tr><td>3</td><td>Creativity</td></tr><tr><td>3</td><td>Fitness</td></tr></tbody></table>
