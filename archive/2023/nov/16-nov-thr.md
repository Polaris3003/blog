# 16 Nov - Thr

Today's stuff

<table data-header-hidden><thead><tr><th width="80" data-type="checkbox"></th><th width="120" data-type="select" data-multiple>Type</th><th>Action</th></tr></thead><tbody><tr><td>false</td><td></td><td>leetcode</td></tr><tr><td>false</td><td></td><td>6.824 zookeeper</td></tr><tr><td>false</td><td></td><td>0x3f tea</td></tr><tr><td>false</td><td></td><td>algorithm</td></tr><tr><td>false</td><td></td><td>日本語のstudy</td></tr><tr><td>false</td><td></td><td>xiaolin coding</td></tr></tbody></table>

## Notes & ideas

{% embed url="https://www.youtube.com/watch?t=946s&v=HYTDDLo2vSE" %}
zookeeper
{% endembed %}

<details>

<summary>leetcode</summary>

1\. (打卡 1) [37 \[解数独\]](https://leetcode.cn/problems/sudoku-solver/description/) 🤩

![](<../../../.gitbook/assets/image (7).png>)\
2\. (打卡 2) [745 \[前缀和后缀搜索\] ](https://leetcode.cn/problems/prefix-and-suffix-search/description/)🤩

![](<../../../.gitbook/assets/image (9).png>)\
3\. (每日) [2760 \[最长奇偶子数组\]](https://leetcode.cn/problems/longest-even-odd-subarray-with-threshold/description/?envType=daily-question\&envId=2023-11-16) ![](../../../.gitbook/assets/FK0\(U]GU\[5%XVGX3MX$@7BR.png)

![](<../../../.gitbook/assets/image (8).png>)

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



</details>

<details>

<summary>algorithm</summary>



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
