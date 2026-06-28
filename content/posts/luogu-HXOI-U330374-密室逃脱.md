---
title: luogu-HXOI U330374-密室逃脱
tags: [OI, HXOI, 搜索, 广搜，BFS]
category: 题解
description: 洛谷-HXOI U330374-密室逃脱 Std | 题解
published: 2023-08-23 08:19:24+08
updated: 2023-09-01 19:52:20+08
---

[原题链接](https://www.luogu.com.cn/problem/U330374)

Algorithms: `搜索` `广搜，BFS`

---

依照题意，不难发现这是一道很普通的广搜题，只不过是三维广搜。对于这种情况我们只需要添加  `dx`、`dy` 数组的值且再添加一个 `dz` 数组，值如下。

```cpp
dz[6] = {-1, 1, 0, 0, 0, 0};
dx[6] = {0, 0, -1, 0, 1, 0};
dy[6] = {0, 0, 0, 1, 0, -1};
```

在此题中，我们发现除了正常广搜之外，还有两个要点：

1. 小H 拥有一些体力值，某些时候会需要消耗体力拆卸陷阱；
2. 小H 手上的钥匙数量会变化，且可能会有需要钥匙开门的时候。

虽然题面看上去很复杂，但我们只需要仔细分析，其实可以发现：

- 当 小H 有足够的体力时，那么必须拆卸陷阱，否则不将当前状态入队。
- 当 小H 受伤有足够的钥匙时，那么必须开门，否则不将当前状态入队。

这样一来，我们广搜中也只是多了两个 ~~分支结构~~。

$Std$

```cpp title="std.cpp"
#include <iostream>
#include <queue>

#define endl '\n'

using namespace std;

struct Node {
	int z, x, y, t, k, v;
};

const int H = 165;
const int N = 405;

int h, n, m, v, w;
int a[H][N][N], sz, sx, sy;
queue<Node> q;
bool inq[H][N][N];
int dz[6]{-1, 1, 0, 0, 0, 0}, dx[6]{0, 0, -1, 0, 1, 0}, dy[6]{0, 0, 0, 1, 0, -1};

int bfs() {
	int k = a[sz][sx][sy] == 5 ? 1 : 0;
	q.push({sz, sx, sy, 0, k, v});
	inq[sz][sx][sy] = true;
	Node p;
	
	while (q.size()) {
		p = q.front();
		q.pop();
		
		for (int i = 0; i < 6; ++i) {
			int nz = p.z + dz[i];
			int nx = p.x + dx[i];
			int ny = p.y + dy[i];
			int nt = p.t + 1;
			int nk = p.k;
			int nv = p.v;
			
			if (nz < 1 || nz > h) continue;
			if (nx < 1 || nx > n || ny < 1 || ny > m) {
				return nt;
			}
			if (inq[nz][nx][ny]) continue;
			if (a[nz][nx][ny] == 2) continue;
			if (a[nz][nx][ny] == 3) {
				if (nv >= w) {
					nv -= w;
				} else {
					continue;
				}
			} else if (a[nz][nx][ny] == 4) {
				if (nk) {
					--nk;
				} else {
					continue;
				}
			} else if (a[nz][nx][ny] == 5) {
				++nk;
			}
			
			q.push({nz, nx, ny, nt, nk, nv});
			inq[nz][nx][ny] = true;
		}
	}
	
	return 0;
}

int main() {
	ios::sync_with_stdio(false);
	cin.tie(nullptr), cout.tie(nullptr);
	
	cin >> h >> n >> m;
	cin >> sz >> sx >> sy;
	cin >> v >> w;
	for (int k = 1; k <= h; ++k) {
		for (int i = 1; i <= n; ++i) {
			for (int j = 1; j <= m; ++j) {
				cin >> a[k][i][j];
			}
		}
	}
	
	int ans = bfs();
	if (!ans) {
		cout << "No";
	} else {
		cout << "Yes" << endl;
		cout << ans;
	}
}
```
