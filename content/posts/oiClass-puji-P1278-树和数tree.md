---
title: oiClass-puji P1278-树和数tree
tags: [OI, 树结构]
category: 题解
description: oiClass-puji P1278-树和数tree 题解
published: 2023-08-25 11:48:42+08
updated: 2023-08-30 21:24:25+08
---

[原题链接](http://oiclass.com/d/puji/p/1278)

Algorithms: `树结构`

---

## 很水的一道题

只需要判断如果 _**父节点的优先级**_  $\geq$ _**子节点的优先级**_ 就需要加括号。

但是当给左节点加括号时，且父节点与左节点的优先级相同时，括号可以省略。

$Ac Code$

```cpp title="AcCode.cpp"
#include <iostream>

using namespace std;

const int N = 1e5 + 5;

int n, m, a[N], ans;
int g[N][2];

void dfs(const int &u) {
    for (int i = 0; i < 2; ++i) {
        int v = g[u][i];
        if (!g[u][i]) continue;
        if (a[v] <= a[u]) {  // 需要括号
            ++ans;
        }
        if (a[v] == a[u] && !i) {  // 可以省略
            --ans;
        }
        dfs(v);
    }
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr), cout.tie(nullptr);

    cin >> n >> m;
    for (int i = 1; i <= n; ++i) {
        int l, r, x;
        cin >> l >> r >> x;
        g[i][0] = l;
        g[i][1] = r;
        a[i] = x;
    }

    dfs(1);

    cout << ans;
}
```