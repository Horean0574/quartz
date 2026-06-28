---
title: 数据迁移之「从 Waline 到 Twikoo」
published: 2026-02-20 21:26:27+08
description: '本文介绍了如何将博客的评论系统从 Waline 迁移到 Twikoo，重点在于分析两者的数据结构差异并自行编写迁移程序。文中首先回顾了前一篇文章中的相关背景，然后详细比较了 Waline 和 Twikoo 的数据格式，接着阐述了程序的构思、数据迁移的流程和实现，并提供了完整的迁移代码。'
tags: [技术, 博客, 迁移, 教程, 评论系统, Waline, Twikoo]
category: '开发'
draft: false
---

> 本文是对上一篇中提到的待解决问题给出的应对方案，可以点此阅读 [LeanCloud停止对外服务&第一次博客迁移](/posts/leancloud停止对外服务第一次博客迁移/)。

距离上一次发文已经有足足十二天了！这篇文章也大概拖了有一个多星期了，不过还是先不讲这么多废话了吧。

# 前言

上一篇文章其实是有提到我将博客评论系统从 [Waline](https://waline.js.org/) 迁移到 [Twikoo](https://twikoo.js.org/) 的，但是当时并没有迁移原来的评论数据，因为 [Twikoo](https://twikoo.js.org/) 的管理面板中并不支持直接从 [Waline](https://waline.js.org/) 导入，目前好像只支持从 [Valine](https://valine.js.org/)、[Disqus](https://disqus.com/)、[Artalk](https://artalk.js.org/) 和 [Twikoo](https://twikoo.js.org/) 本身导入；本来我还想着因为 [Waline](https://waline.js.org/) 是 [Valine](https://valine.js.org/) 的进化版，可不可以把 [Waline](https://waline.js.org/) 的评论数据通过 [Valine](https://valine.js.org/) 选项导入……但是非常不幸的是，**失败了**！看来这两者之间的数据格式还是与些许不兼容的。

——那么，正所谓“自己动手，丰衣足食”，既然前面的选项都无法直接导入，那就干脆自己从零开始制作一个程序把 [Waline](https://waline.js.org/) 格式的评论数据转换为 [Twikoo](https://twikoo.js.org/) 格式的评论数据然后通过 [Twikoo](https://twikoo.js.org/) 选项导入啦~（谁会想着自己一个一个手动迁移呢）

# 自己动手，丰衣足食

## 对比数据结构

迁移之前，当然要先充分了解 [Waline](https://waline.js.org/) 和 [Twikoo](https://twikoo.js.org/) 各自的数据结构特点，找出其中的相同和不同之处，才能更加系统地制作迁移程序。

### 总览全局

首先，放长眼光，总览全局，两者导出的数据都是 `JSON` 格式的文件：

不难发现 [Waline](https://waline.js.org/) 的数据结构大致是：

```json title="waline.json"
{
  "data": {
    "Comment": [
      {/*...*/},
      {/*...*/},
      {/*...*/},
    ],
    /*...*/
  },
}
```

而 [Twikoo](https://twikoo.js.org/) 的数据结构大致是：

```json title="twikoo.json"
[
  {/*...*/},
  {/*...*/},
  {/*...*/},
]
```

对比非常明显，[Twikoo](https://twikoo.js.org/) 的数据文件应该是要比 [Waline](https://waline.js.org/) 小很多的，而且结构也更加清晰。在仔细观察后，就会发现 [Twikoo](https://twikoo.js.org/) 的数据结构整体的这个数组就对应了 [Waline](https://waline.js.org/) 数据结构中的 `Comment` 字段的数组，而且这个数组中的每一个值都是一个对象，代表着每一条评论数据。

### 深入探究

其次，分析两者评论数据数组中的具体内容，请看下面两组例子（这里就拿我的博客的一些评论数据举例）：

1. 第一组（非回复评论）：

   ```json title="waline.json"
   {
     "nick": "静凇",
     "ip": "12.345.678.90",
     "like": 1,
     "mail": "abcdefg@example.com",
     "ua": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
     "insertedAt": "2023-12-27T13:29:58.613Z",
     "status": "approved",
     "link": "",
     "comment": "谢谢，帮了大忙了",
     "url": "/posts/hexo-redefine-theme-踩过的坑/",
     "objectId": "68799fea6e25c660f962a2c7",
     "createdAt": "2025-07-18T01:14:18.723Z",
     "updatedAt": "2025-07-18T01:14:18.723Z"
   },
   ```

   ```json title="twikoo.json"
   {
     "_id": "f34674e295fa49539b8984cb99a59f94",
     "nick": "静凇",
     "mail": "abcdefg@example.com",
     "link": "",
     "ua": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36",
     "ip": "12.345.678.90",
     "url": "/posts/hexo-redefine-theme-%E8%B8%A9%E8%BF%87%E7%9A%84%E5%9D%91/",
     "comment": "<p>谢谢，帮了大忙了</p>",
     "uid": "8bc585221ed5410c8d73b2d629bd24a7",
     "mailMd5": "1a7ca9215b81484630893cb8d5f73e0f",
     "master": false,
     "href": "https://blog.hxrch.top/posts/hexo-redefine-theme-%E8%B8%A9%E8%BF%87%E7%9A%84%E5%9D%91/",
     "isSpam": false,
     "created": 1703683798613,
     "updated": 1752801258723,
     "top": false
   },
   ```

 2. 第二组（回复评论）：

    ```json title="waline.json"
    {
      "nick": "Horean0574",
      "ip": "98.765.432.10",
      "mail": "uvwxyz@example.com",
      "ua": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/140.0.0.0 Safari/537.36",
      "insertedAt": "2025-07-18T01:28:52.287Z",
      "pid": "68799fea6e25c660f962a2c7",
      "status": "approved",
      "link": "https://www.hxrch.top",
      "comment": "感谢您的认可<img class=\"wl-emoji\" src=\"//unpkg.com/@waline/emojis@1.2.0/bmoji/bmoji_unavailble_doge.png\" alt=\"bmoji_unavailble_doge\">",
      "url": "/posts/hexo-redefine-theme-踩过的坑/",
      "user_id": "64eabd5c7eac3a7867657e83",
      "rid": "68799fea6e25c660f962a2c7",
      "objectId": "6879a35413c0fe150872ea9e",
      "createdAt": "2025-07-18T01:28:52.561Z",
      "updatedAt": "2025-07-18T01:28:52.561Z"
    },
    ```

    ```json title="twikoo.json"
    {
      "_id": "6d26831b6dcf40f082d2f66d1c7e5c51",
      "nick": "Horean",
      "mail": "uvwxyz@example.com",
      "link": "https://www.hxrch.top",
      "ua": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/140.0.0.0 Safari/537.36",
      "ip": "98.765.432.10",
      "url": "/posts/hexo-redefine-theme-%E8%B8%A9%E8%BF%87%E7%9A%84%E5%9D%91/",
      "comment": "<p>感谢您的认可<img class=\"wl-emoji\" src=\"//unpkg.com/@waline/emojis@1.2.0/bmoji/bmoji_unavailble_doge.png\" alt=\"bmoji_unavailble_doge\"></p>",
      "pid": "f34674e295fa49539b8984cb99a59f94",
      "rid": "f34674e295fa49539b8984cb99a59f94",
      "uid": "51fa62a9deed478544da9e60663434d8",
      "mailMd5": "65b03c3c3cdd117c392cf74f5e588083",
      "master": true,
      "href": "https://blog.hxrch.top/posts/hexo-redefine-theme-%E8%B8%A9%E8%BF%87%E7%9A%84%E5%9D%91/",
      "isSpam": false,
      "created": 1752802132287,
      "updated": 1752802132561,
      "top": false
    },
    ```

不知道大家有没有发现些什么，[Waline](https://waline.js.org/) 与 [Twikoo](https://twikoo.js.org/) 这两种评论系统的数据结构非常相似呢，例如 `nick`, `mail`, `comment` 等等；当然也有一些不一样的地方，比如 [Waline](https://waline.js.org/) 的 `objectId` 和 [Twikoo](https://twikoo.js.org/) 的 `_id`、 [Waline](https://waline.js.org/) 的 `status` 和 [Twikoo](https://twikoo.js.org/) 的 `isSpam`。

所以这里就需要我们逐个分析，一一对比，便可得到如下表格数据对应表格：

<style>
    #table-1 th, #table-1 td {
        text-align: center;
    }

    #table-1 tr td:first-child {
        font-weight: 600;
    }
    .tb1-hint {
    	color: gray;
    	margin-left: 4px;
    }
</style>

<table id="table-1" border="1">
<thead>
<tr><th>字段含义</th><th>Waline 字段名称</th><th>Twikoo 字段名称</th></tr>
</thead>
<tbody>
<tr><td>评论者昵称</td><td colspan="2">nick</td></tr>
<tr><td>评论者邮箱</td><td colspan="2">mail</td></tr>
<tr><td>评论者用户代理</td><td colspan="2">ua</td></tr>
<tr><td>评论者IP地址</td><td colspan="2">ip</td></tr>
<tr><td>评论内容</td><td colspan="2">comment</td></tr>
<tr><td>评论者网站</td><td colspan="2">link</td></tr>
<tr><td>评论地址资源路径</td><td colspan="2">url</td></tr>
<tr><td>回复的父评论ID</td><td colspan="2">pid<span class="tb1-hint">(null | 24位MongoDB ObjectId / UUID4)</span></td></tr>
<tr><td>回复的根评论ID</td><td colspan="2">rid<span class="tb1-hint">(null | 24位MongoDB ObjectId / UUID4)</span></td></tr>
<tr><td>点赞人数/列表</td><td colspan="2">like<span class="tb1-hint">(number / string[])</span></td></tr>
<tr><td>评论ID</td><td>objectId<span class="tb1-hint">(24位MongoDB ObjectId)</span></td><td>_id<span class="tb1-hint">(UUID4)</span></td></tr>
<tr><td>Twikoo中的用户ID</td><td>-</td><td>uid<span class="tb1-hint">(UUID4)</span></td></tr>
<tr><td>Waline中的用户ID</td><td>user_id<span class="tb1-hint">(24位MongoDB ObjectId)</span></td><td>-</td></tr>
<tr><td>评论者邮箱的MD5密文</td><td>-</td><td>mailMd5</td></tr>
<tr><td>是否博主评论</td><td>-</td><td>master<span class="tb1-hint">(boolean)</span></td></tr>
<tr><td>评论完整地址</td><td>-</td><td>href</td></tr>
<tr><td>评论状态</td><td>status<span class="tb1-hint">("approved" | "waiting" | "spam")</span></td><td>isSpam<span class="tb1-hint">(boolean)</span></td></tr>
<tr><td>评论插入/创建时间</td><td>insertedAt<span class="tb1-hint">(ISO 8601)</span></td><td>created<span class="tb1-hint">(UNIX 时间戳)</span></td></tr>
<tr><td>Waline中评论创建时间</td><td>createdAt<span class="tb1-hint">(ISO 8601)</span></td><td>-</td></tr>
<tr><td>评论更新时间</td><td>updatedAt<span class="tb1-hint">(ISO 8601)</span></td><td>updated<span class="tb1-hint">(UNIX 时间戳)</span></td></tr>
<tr><td>是否置顶</td><td>sticky<span class="tb1-hint">(number)</span></td><td>top<span class="tb1-hint">(boolean)</span></td></tr>
</tbody>
</table>

> [!warning] 注意
> 非常重要的一点，这里需要注意相同字段在两种不同的评论系统下**数据类型可能不同**。

## 程序构思

为了更好地编写迁移程序，我们需要在这之前梳理程序思路，思考这些数据的具体处理方式。

### 数据处理

> 以下条例中将用 **中括号[]** 代指 [Twikoo](https://twikoo.js.org/) 字段，用 **尖括号<>** 代指 [Waline](https://waline.js.org/) 字段。

- 完全照搬：`nick`, `mail`, `ua`, `ip`, `comment`, `link`, `url`.

- `[_id]` 与 `<objectId>`一一对应，直接生成新的 UUID4 作为`[_id]`.

- 当 `<status>` 为 **"waiting"** 或 **"spam"** 时，`[isSpam]` 为 true.

- 当 `<status>` 为 **"approved"** 时，`[isSpam]` 为 false.

- `[created]` 与 `<insertedAt>` 一一对应（需将 **ISO 8601** 时间转换为 **UNIX 时间戳**）.

  > 为什么不是与 `<createdAt>` 对应呢？因为 `<createdAt>` 可能会随 [Waline](https://waline.js.org/) 系统的更新而改变[我的推测]，而 `<insertedAt>` 代指这条评论插入数据库的时间，就不会受到影响。

- `[updated]` 与 `<updatedAt>` 一一对应（需将 **ISO 8601** 时间转换为 **UNIX 时间戳**）.

- `<url>` 中的非 ASCII 字符（如中文字符）需要进行**URL编码**后才可以存为 `[url]`，否则无效.

- `[href]` 由**博客域名**与 `[url]` 拼接而得.

- `[master]` 取决于评论者邮箱是否为博主邮箱.

- `[pid]`, `[rid]` 格式与 `[_id]` 相同，均为 UUID4 **或者当其为 *非回复评论* 时，其值为 null**.

- `<pid>`, `<rid>` 格式与 `<objectId>` 相同，均为 MongoDB ObjectId **或者当其为 *非回复评论* 时，则不存在**.

- `[mailMd5]` 由 `[mail]` 字段进行 MD5 加密而得，32位或64位皆可，这里取32位.

- `[top]` 与 `<sticky>` 一一对应，当 `<sticky>` 的值大于零时，`[top]` 的值为真.

- `[comment]` 应为 HTML 格式，而 `<comment>` 可以选择是否保留 HTML 标签，所以转换时需要把 `<comment>` 从 Markdown 进一步转换为 HTML.

> [!note] 提醒
> 1. `<user_id>` 字段可以<u>完全不用理会</u>，因为未注册的用户没有这一属性，所以这里以 `<mail>` 作为判断是否为同一用户的依据。
> 2. `<like>` 字段也可以<u>不用理会</u>，因为 [Waline](https://waline.js.org/) 中的 `<like>` 字段存储数据为点赞总量，而 [Twikoo](https://twikoo.js.org/) 中的 `[like]` 字段则是一个包含点赞用户ID的数组，所以不兼容，只可从 [Twikoo](https://twikoo.js.org/) 到 [Waline](https://waline.js.org/) 单向转换。

### 流程&算法

1. 最开始当然是先读取原来 [Waline](https://waline.js.org/) 的评论数据啦。
2. 第一次循环，遍历原评论数据。因为 `[_id]` 与 `<objectId>` 一一对应，而且需要根据 `<mail>` 确定 `[uid]`，又考虑到后面转换数据时可能有多层嵌套关系，所以第一次遍历原评论数据应该先**建立**以上字段的**映射**，以便后来使用。
3. 第二次遍历原评论数据。这一次则需要根据上文提到的表格进行数据转换，这里需要充分利用好刚才的映射。
4. 然后就可以将转换结果写入文件啦~

这样一来，我们就可以大致画出整个程序的流程图了：

<img src="https://img.hxrch.top/20260220171113316.svg" alt="程序流程图" style="width: 30%; min-width: 250px; margin: 0 auto;" />

## Coding!

数据和算法逻辑都有了，接下来就是纯手工活了——这里使用 [Python](https://www.python.org/) 为编程语言编写了这个迁移程序，依照上面的思路，我设计了一款交互式输入的迁移程序并部署至 [GitHub 仓库](https://github.com/Horean0574/waline2twikoo/)：

::github{repo="Horean0574/waline2twikoo"}

也可以直接在这里下载运行主要代码文件（更多详细说明还请参考 [GitHub 仓库](https://github.com/Horean0574/waline2twikoo/)）：

> [!tip] 注意
> 根据以上流程，本程序需提前安装的第三方库：`click`, `Markdown`:
> ```bash
> pip install click markdown
> ```

```python title="main.py"
import json
import uuid
import hashlib
import click
from pathlib import Path
from datetime import datetime
from urllib.parse import quote
from markdown import markdown

cidMap = { }
uidMap = { }
res = []


def step_start(prompt):
    click.echo(prompt, nl=False)


def step_complete(another_newline=False):
    if another_newline:
        click.echo("  完成✅\n")
    else:
        click.echo("  完成✅")


def new_uuid():
    return str(uuid.uuid4()).replace("-", "")


def md5_encrypt(data):
    md5 = hashlib.md5()
    md5.update(data.encode("UTF-8"))
    return md5.hexdigest()


def iso2unix(iso):
    dt = datetime.fromisoformat(iso)
    return int(dt.timestamp() * 1000)


def get_converted(item, site_domain, master_mail):
    url = quote(item["url"])
    return {
        "nick": item["nick"],
        "mail": item["mail"],
        "link": item["link"],
        "ua": item["ua"],
        "ip": item["ip"],
        "url": url,
        "comment": markdown(item["comment"].replace("\n", "\n\n")),
        "pid": cidMap[item["pid"]] if "pid" in item else None,
        "rid": cidMap[item["rid"]] if "rid" in item else None,
        "_id": cidMap[item["objectId"]],
        "uid": uidMap[item["mail"]],
        "mailMd5": md5_encrypt(item["mail"]),
        "master": bool(item["mail"] == master_mail),
        "href": "https://" + site_domain + url,
        "isSpam": bool(item["status"] != "approved"),
        "created": iso2unix(item["insertedAt"]),
        "updated": iso2unix(item["updatedAt"]),
        "top": bool(item["sticky"] > 0) if "sticky" in item else False,
    }


def read_waline(read_file):
    step_start("读取 Waline 评论数据中……")
    with open(read_file, "r", encoding="UTF-8") as f:
        waline = json.load(f)["data"]["Comment"]
    total = len(waline)
    cnt = 0
    step_complete()
    return waline, total, cnt


def establish_map(waline):
    step_start("映射建立中……")
    for item in waline:
        cidMap[item["objectId"]] = new_uuid()
        if item["mail"] not in uidMap:
            uidMap[item["mail"]] = new_uuid()
    step_complete(True)


def convert_all(site_domain, master_mail, waline, total, cnt):
    for item in waline:
        cnt += 1
        step_start(f"{cnt}/{total}: 正在转换来自 [{item["nick"]}] 的评论……")
        res.append(get_converted(item, site_domain, master_mail))
        step_complete()


def write_twikoo(write_file):
    step_start("\n写入文件中……")
    output_path = Path(write_file)
    output_path.parent.mkdir(parents=True, exist_ok=True)
    with open(write_file, "w", encoding="UTF-8") as f:
        json.dump(res, f, ensure_ascii=False, indent=2)
    step_complete()


def main(site_domain, master_mail, master_uid, read_file, write_file):
    global uidMap
    if master_uid != "":
        uidMap = { master_mail: master_uid }
    waline, total, cnt = read_waline(read_file)
    establish_map(waline)
    convert_all(site_domain, master_mail, waline, total, cnt)
    write_twikoo(write_file)


def interactive_input():
    site_domain = click.prompt("你的站点域名")
    bcf = click.prompt("你（博主）有在新的Twikoo评论系统上评论过吗？(y/N)", type=bool, default=False, show_default=False)
    if bcf:
        master_mail = click.prompt("你的电子邮件")
        master_uid = click.prompt("你的 Twikoo UID（可在导出 Twikoo 评论数据后看到）")
    else:
        master_mail = master_uid = ""
    read_file = click.prompt("原 Waline 评论数据文件路径（相对路径，JSON文件）")
    write_file = click.prompt("新的 Twikoo 评论数据文件存储路径（相对路径，JSON文件）")
    click.echo()
    main(site_domain, master_mail, master_uid, read_file, write_file)


if __name__ == '__main__':
    click.echo("Program started.\n")
    interactive_input()
    click.echo("\nProgram ended.")
```

# 后记

总结一下要点：自己制作一个评论数据迁移程序，大概就是 `分析数据结构`、`程序构思` 再到 `编码` 这三个过程，整体上来看难度不大，但是有点费时，不过写完并正确运行之后真的非常有成就感，就会觉得这段时间的功夫没有白费，想想就觉得舒服~ 同时也推荐大家自己去尝试编写这样一个程序。

如果觉得本项目不错的，欢迎在 [GitHub 仓库](https://github.com/Horean0574/waline2twikoo/) 上给个 **Star** 哦~ 感谢大家对本项目的支持！如有任何疑问或想法也欢迎在[仓库](https://github.com/Horean0574/waline2twikoo/)上提交 [Issue](https://github.com/Horean0574/waline2twikoo/issues/new) 或 [Pull request](https://github.com/Horean0574/waline2twikoo/compare)。
