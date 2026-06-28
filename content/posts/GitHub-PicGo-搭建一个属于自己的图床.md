---
title: GitHub + PicGo 搭建一个属于自己的图床
tags: [GitHub, PicGo, 图床]
category: 开发
description: 手把手教你如何搭建一个完全属于自己的图床，完全免费，而且空间无限量！
published: 2023-09-01 13:40:21+08
updated: 2024-08-16 16:34:19+08
---


>  想必大家肯定都很想拥有一个完全属于自己的图床吧

那么今天，为了帮助大家实现这个愿望，我花了亿点时间写了一篇博客教程，喜欢的话可以向其他人推荐一下哦。

---

那么，进入正题：

在我们搭建图床之前，我想应该很多同学们都有过这样的经历：

- 花了很长时间在网上找免费图床的网站，但是却发现空间根本不够用。
- 本已经信任了很久的图床网站，却突然有一天崩掉了，一夜之间全部链接都无法显示。

为了解决这些问题，我们自然而然的就想到了自己搭建一个稳定的图床，详细步骤见下。

# 新建 Git 仓库

GitHub 账号应该就不用我多说了吧，如果还没有的请前往 [GitHub 主页](https://github.com) 注册 GitHub 账号。

1. 我们在 GitHub 控制面板找到右上角的 小加号，再点击 `New repository` 新建一个仓库。

![](https://img.hxrch.top/202309011356018.webp)

2. 在新建仓库的页面，我们在 `Repository name` 那里填上 `img-host` （也可以换成其他你喜欢的仓库名称），`Description` 那里填写上你的仓库描述。

{% notel red fa-circle-exclamation 注意 %}
一定要选择 Public 公开仓库，否则可能无法访问你存储的图片。
{% endnotel %}

![](https://img.hxrch.top/202309011356020.webp)

接着点击 `Create Repository` 创建仓库。

最后我们就可以手动把图片推送到仓库里面去啦，到时候访问仓库图片地址就可以了！

# 获取 GitHub Token

在 GitHub 主页，点击右上角你的头像，在出现的菜单里选择 `Settings` 进入设置。

![](https://img.hxrch.top/202309011356022.webp)

再在左侧菜单栏选择 `Developer settings` 进入开发者设置。

![](https://img.hxrch.top/202309011356024.webp)

然后在左侧选择 `Personal access tokens`，再选择 `Tokens (classic)`，进入以后，点击右上角 `Generate new token` 选择 `classic` 版生成新的密钥。

![](https://img.hxrch.top/202309011356025.webp)

接下来 GitHub 可能会让你输入密码以确定是本人操作，这里正常输入密码就行了。

然后 Token 名称自己能知道是什么就行，有效日期作者推荐无期限（No Expiration），不然每次到期还要再新建一个，还要更改配置，然后下面的 Token 权限选择只需要勾选 repo 就可以了，其他权限不需要用到。

![](https://img.hxrch.top/202309011356026.webp)

点击 `Generate token` 生成密钥，然后一定要记得复制生成的密钥，它只会显示一次！

![](https://img.hxrch.top/202309011356027.webp)

最后可以选择把复制的密钥存起来，而且不要被别人看到，以防丢失或泄露。

# 使用 PicGo 上传图片

但是我们直接手动推送图片到仓库的话，可能会有一系列麻烦的过程，所以，有请我们今天的主角：**PicGo**！

PicGo 可以帮助我们更方便地上传图片，[PicGo 下载链接](https://github.com/Molunerfinn/PicGo/releases)。

下载安装好后，我们打开 PicGo，在左侧导航栏选择 `图床设置`，然后选择 GitHub。

接下来是 GitHub 仓库设置的填写：

- `设定仓库名`：`<GitHub 用户名>/<图床仓库名>`。
- `设定分支名`：默认 `main` 就可以了。
- `设定Token`：上文提到的 GitHub Token，复制粘贴进去就行。
- `设定存储路径`：如果没有留空就行。
- `设定自定义域名`：此处我们选择用 `jsdelivr` 来加速访问，填写 `https://cdn.jsdelivr.net/gh/<GitHub 用户名>/<图床仓库名>`。

![](https://img.hxrch.top/202309011356021.webp)

最后选择左侧导航栏 `上传区`，可以把图片拖进去，或者是点击浏览选择文件，皆可上传成功！

上传成功后就可以到你的 GitHub 仓库查看啦，如果你按照上文使用了 `jsdelivr` 加速，那么访问地址为：`https://cdn.jsdelivr.net/gh/<GitHub 用户名>/<图床仓库名>/<存储路径>/<图片文件名>`，或者在左侧导航栏 `相册` 处找到图片复制链接，这样就不用担心你的博客没有一个可以依靠的图床啦！

# 可能会遇到的问题

如果你没有上传成功图片，那么可能是以下原因造成的。

1. `图床设置` > `GitHub` 没有调整好，可以仔细对照着你的 GitHub 仓库信息修改一下。

2. 如果你正在使用 `Watt Toolkit` （原名 `Steam++`） 加速的话，请尝试先暂停加速，再去上传试试，这次应该能够上传成功，如果嫌太麻烦的话，作者可以推荐另一个好用的加速器：[Dev Sidecar](https://github.com/docmirror/dev-sidecar/releases)，用 `Dev Sidecar` 加速时不会导致 PicGo 图片上传失败。

3. 如果你的图片文件名与之前上传的有重复，那么建议更改文件名或找到 PicGo 左侧导航栏 `PicGo设置` 处把 `时间戳重命名` 开关打开，这样就不用担心文件重名了，PicGo 会自动把上传后的文件名更改为当前时间戳。

如果你的问题还没有解决，那么请尝试在网络上查找解决方案。
