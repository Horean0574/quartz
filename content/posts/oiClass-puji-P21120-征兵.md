---
title: oiClass-puji P2112-征兵
tags: [OI, 最小生成树]
category: 题解
description: oiClass-puji P2112-征兵 题解
published: 2023-08-24 12:08:30+08
updated: 2023-08-30 22:45:26+08
---

[原题链接](http://oiclass.com/d/puji/p/P2112/)

Algorithms: `最小生成树`

---

## 一眼看出最小生成树

> 赛时不小心把存边数组开大了，结果 MLE……

依照题意，我们可以把总点数看作是 $N+M$，边数最多有 $R$ 条，边权为 $10000 - V_i$，为了给每个点一个编号，我们把女生编为 $X_i + 1$，男生编为 $Y_i + N + 1$。

因为可能不止一个需要单独征集的士兵，所以我们需要建立一个 0号 **虚拟点**，与全部其他节点相连，权值为 $10000$ ，但这个时候边数最多就有 $R + N + M$ 条了（注意数组大小）。

接下来跑一遍 $Kruskal$ 就可以了。

**PS:** 变量解释：

```cpp
// t: T, x: N, y: M, r: R

// n: 总点数, m: 总边数

// cnt: 统计剩余点数目
```

$Ac Code$

```cpp title="AcCode.cpp"
#include <iostream>
#include <algorithm>

#define endl '\n'

using namespace std;

struct Edge {  // 存边结构体
	int u, v, w;
	
	bool operator < (const Edge &A) const {  // 重载排序运算符
		return w < A.w;
	}
};

const int N = 2e4 + 5;
const int M = 9e4 + 5;
const int ORGL = 1e4;  // 征集士兵原价 10000

int t, x, y, r;
int n, m, cnt, ans;
int fa[N];  // 并查集 fa 数组
struct Edge e[M];  // 存边数组

inline void init() {  // 多组数据，记得重置
	ans = cnt = m = 0;
	
	for (int i = 1; i <= n; ++i) {  // 并查集初始化
		fa[i] = i;
	}
}

inline int find(const int &l) {  // 并查集 find
	return fa[l] == l ? l : fa[l] = find(fa[l]);
}

inline int gid(const int &l, const bool &girl) {  // 获取节点编号
	if (girl) {
		return l + 1;
	} else {
		return l + x + 1;
	}
}

int main() {
	ios::sync_with_stdio(false);
	cin.tie(nullptr), cout.tie(nullptr);
	
	cin >> t;
	while (t--) {
		cin >> x >> y >> r;
		n = x + y;
		init();
		for (int i = 1; i <= r; ++i) {
			int xi, yi, vi;
			cin >> xi >> yi >> vi;
			int xid = gid(xi, true);
			int yid = gid(yi, false);
			e[++m].u = xid;
			e[m].v = yid;
			e[m].w = ORGL - vi; // 边权为 10000 - Vi
		}
		
		// 虚拟 0 号节点
		for (int i = 1; i <= n; ++i) {
			e[++m].u = 0;
			e[m].v = i;
			e[m].w = ORGL;
		}
		
		// Kruskal 最小生成树
		sort(e + 1, e + m + 1);
		for (int i = 1; i <= m; ++i) {
			int fu = find(e[i].u);
			int fv = find(e[i].v);
			if (fu != fv) {
				fa[fu] = fv;
				ans += e[i].w;
				if (++cnt == n - 1) break;
			}
		}
		
		// 最终答案加上 剩余的一个点原价
		cout << ans + ORGL << endl;
	}
}
```