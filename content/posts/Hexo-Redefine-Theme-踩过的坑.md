---
title: Hexo - Redefine Theme 踩过的坑
tags: [Hexo, 踩过的坑]
category: 开发
image: https://img.hxrch.top/202507210903988.webp
description: 本文介绍了使用 Hexo 建立个人博客时可能遇到的问题，尤其是针对 Redefine 主题在 Windows 系统中的具体配置步骤。文章详细讲解了 Hexo 的安装、项目初始化、主题安装与启用，以及一些常见的坑和解决方案，包括 Hexo 版本的选择和 LaTeX 渲染的配置。
published: 2023-08-30 11:16:08+08
updated: 2025-07-11 07:07:36+08
---


> 众所周知，在自建博客这一界有个很强的东西：[Hexo](https://hexo.io)
>
> 但这其中的**坑**，可谓是劝退了不少初学者……

所以，今天我就来帮大家避一下**坑**。

这篇文章的所有内容都是建立在 [Hexo](https://hexo.io) 的其中一个主题 [Redefine](https://github.com/EvanNotFound/hexo-theme-redefine) 上的，且仅针对 Windows 系统，原因嘛……就是我现在在用这款主题。

**PS:** 这篇文章的内容对于其他主题和其他操作系统是否有效暂时未知，本文仅供参考。



# 新手教程

## Hexo

### 安装

> 友情链接：[Hexo安装文档](https://hexo.io/zh-cn/docs/)

其实一开始和官网的教程差不多，可以直接 `npm` 全局安装。

如果有不了解 `Node.js` 的同学，我以后会单独出一篇教程来详细解说……

```bash
npm install -g hexo-cli
```

此外，如果你对 `npm` 熟悉一点，那么你可以仅局部安装 `Hexo`。

```bash
npm install hexo
```

### 初始化

`hexo-cli` 中初始化一个博客项目的命令为 `hexo init <folder>`，其中 `<folder>` 为目录名（亦为项目名）。

```bash
hexo init <folder>
cd <folder>
npm install
```

接下来更详细的初始化步骤见 [建站 | Hexo](https://hexo.io/zh-cn/docs/setup)。

### 启动

通过 `hexo s` 命令启动本地博客。

```bash
hexo s
```

## 主题：Redefine

> 友情链接：[Redefine官方文档](https://redefine-docs.ohevan.com/)

### 安装

```bash
npm install hexo-theme-redefine@latest
```

### 启用

在 Hexo 根目录下（也就是刚才所说的`<folder>`）的 `_config.yml`，把 `theme` 值修改为 `redefine`。

```yaml
theme: redefine
```

### 配置

在 Hexo 根目录下创建 `_config.redefine.yml` 文件，并将 [此处](https://github.com/EvanNotFound/hexo-theme-redefine/blob/main/_config.yml) 的所有内容复制进去。

本文件会自动覆盖主题的配置项，创建本文件的目的是为了方便你在升级主题时，不会丢失你的配置。

### 主题初始化完成

接下来你可以[启动](#启动) Hexo 看看效果。

## 踩过的坑

接下来是咱们今天的重点……

### Hexo 版本

Hexo 的版本一定要不能升到最新版（@7.0.0），就目前作者试验，最高可以升到 @6.3.0 版本，否则 tags 可能会报错 `site.tags.date is not iterable`，可以通过 `npm list` 查看当前所有包的版本，如果需要升级的，可以执行以下指令。

```bash
npm install hexo@6.3.0
```

### LaTeX 渲染

如果想要完整显示所有 LaTeX 公式，首先需要安装插件 `hexo-filter-mathjax`。

```bash
npm install hexo-filter-mathjax
```

然后在 Hexo 配置文件 `_config.yml` 最底下增加如下配置。

```yaml
mathjax:
  tags: none               # 或 'ams' 或 'all'
  single_dollars: true     # 启用单个美元符号作为内联（行内）数学公式定界符
  cjk_width: 0.9           # 相对 CJK 字符宽度
  normal_width: 0.6        # 相对正常（等宽）宽度
  append_css: true         # 将 CSS 添加到每个页面
  every_page: true         # 如果为 true，那么无论每篇文章的前题中的 `mathjax` 设置如何，每页都将由 mathjax 呈现
```

接着必须把 Hexo 原先内置的 Markdown 渲染工具 `hexo-renderer-marked` 卸载，其次安装 `hexo-renderer-pandoc` 。

```bash
npm uninstall hexo-renderer-marked
npm install hexo-renderer-pandoc
```

此时你可以尝试启动 Hexo 本地服务器看看效果，如果执行到 `hexo g` 时报错，那么你需要额外安装一个开源项目 `Pandoc`，仓库地址为 [Pandoc](https://github.com/jgm/pandoc/releases)，最后启动 Hexo 服务器，可以看到所有 LaTeX 及 数学公式 都显示出来了。



---

最后祝大家避过所有坑，走向成功！
