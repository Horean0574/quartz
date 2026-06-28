---
title: luogu-HXOI U332989-身高
tags: [OI, HXOI, 倍增算法]
category: 题解
description: 洛谷-HXOI U332989-身高 Std | 题解
published: 2023-08-27 22:12:54+08
updated: 2023-08-30 22:31:14+08
---

[原题链接](https://www.luogu.com.cn/problem/U332989)

Algorithms: `倍增算法`

---

依照题意，我们需要每次求出区间 $[l, r]$ 中的最小值，再把他与 小H 的身高 $k$ 作比较。

但是看到数据范围，我们可以发现普通暴力的做法是绝对会超时的，所以考虑**倍增算法**，先用 $O(n \log n)$ 的时间复杂度初始化，以后每次查询都只需要 $O(1)$ 的时间复杂度。

$Std$

```cpp title="std.cpp"
#include <iostream>
#include <cmath>

#define endl '\n'

using namespace std;

const int N = 1e6 + 5;
const int LN = log2(N) + 5;

int k, n, t;
int logx[N], f[N][LN];

inline void init() {
	logx[0] = -1;
	for (int i = 1; i <= n; ++i) {
		logx[i] = logx[i / 2] + 1;
	}
	
	for (int j = 1; j <= logx[n]; ++j) {
		for (int i = 1; i + (1 << j) - 1 <= n; ++i) {
			f[i][j] = min(f[i][j - 1], f[i + (1 << (j - 1))][j - 1]);
		}
	}
}

inline int query(const int &x, const int &y) {
	int j = logx[y - x + 1];
	return min(f[x][j], f[y - (1 << j) + 1][j]);
}

int main() {
	ios::sync_with_stdio(false);
	cin.tie(nullptr), cout.tie(nullptr);
	
	cin >> k >> n;
	for (int i = 1; i <= n; ++i) {
		cin >> f[i][0];
	}
	init();
	cin >> t;
	while (t--) {
		int l, r;
		cin >> l >> r;
		if (k >= query(l, r)) {
			cout << "Yes" << endl;
		} else {
			cout << "No" << endl;
		}
	}
}
```
