---
title: luogu-HXOI-U331150-密室逃脱2
tags: [OI, HXOI, 图论, 最小生成树]
category: 题解
description: 洛谷-HXOI U331150-密室逃脱2 Std | 题解
published: 2023-08-25 16:45:27+08
updated: 2023-09-01 19:51:10+08
---


[原题链接](https://www.luogu.com.cn/problem/U331150)

Algorithms: `图论` `最小生成树`

---

不要看题面花里胡哨的，实际上它意思已经很明确了，就是让你在若干个站点存放 **能量补给用具**，使得能量能够扩散到图内每个站点。说到这里应该有些同学觉得，那我存放一个 **能量补给用具** 不就行了吗，这应该都能联通到每个站点啊。

:::danger[警告]

那其实你就大错特错了！

:::

因为它还是要考虑消耗的体力最小啊，那这怎么办……

这时候就需要用上我们的最小生成树了！其实这道题只需要多建一个 **0号虚拟节点**，与其他各个节点相连，就不用考虑每个站点的消耗了，然后再跑一遍 $Kruskal$ 模板，就可以了。

$Std$

```cpp title="std.cpp"
#include <iostream>
#include <algorithm>

using namespace std;

typedef long long ll;

struct Edge {
	int u, v, w;
	
	bool operator < (const Edge &A) const {
		return w < A.w;
	}
};

const int N = 2e3 + 5;
const int M = N * (N - 1);

int n, m, fa[N];
ll ans;
struct Edge e[M];

inline void init() {
	for (int i = 1; i <= n; ++i) {
		fa[i] = i;
	}
}

inline int find(const int &x) {
	return fa[x] == x ? x : fa[x] = find(fa[x]);
}

int main() {
	ios::sync_with_stdio(false);
	cin.tie(nullptr), cout.tie(nullptr);
	
	cin >> n;
	init();
	for (int i = 1; i <= n; ++i) {
		int v;
		cin >> v;
		e[++m].u = 0;
		e[m].v = i;
		e[m].w = v;
	}
	for (int i = 1; i <= n; ++i) {
		for (int j = 1; j <= n; ++j) {
			int w;
			cin >> w;
			if (i != j) {
				e[++m].u = i;
				e[m].v = j;
				e[m].w = w;
			}
		}
	}
	
	sort(e + 1, e + m + 1);
	for (int i = 1; i <= m; ++i) {
		int fu = find(e[i].u);
		int fv = find(e[i].v);
		if (fu != fv) {
			fa[fu] = fv;
			ans += e[i].w;
		}
	}
	
	cout << ans;
}
```
