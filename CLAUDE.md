# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

个人网站，基于 Hugo v0.153.2（extended）+ PaperMod 主题，部署在 GitHub Pages（`dlabde.github.io`）。所有内容使用 Markdown 编写，`git push` 到 main 分支后由 GitHub Actions 自动构建部署。

## 常用命令

```bash
hugo server -D          # 本地开发服务器（含草稿），http://localhost:1313
hugo new content posts/my-post.md  # 新建文章
hugo --minify            # 构建生产版本到 public/
```

## 架构

### 内容板块

六类内容对应 `content/` 下的 section 目录，首页仅展示 `posts`：

| Section | 用途 |
|---|---|
| `posts/` | 技术文章、教程、文学感想 |
| `projects/` | 项目图文展示 |
| `about/` | 个人简历介绍 |
| `reading/` | 在读的书、读书笔记 |
| `life/` | 个人生活记录 |
| `search.md` | 搜索页面 |

### 主题定制

PaperMod 作为 git submodule 引入，**不要直接修改 `themes/PaperMod/` 内的文件**。通过 Hugo 模板覆盖机制在以下目录定制：

- `layouts/` — 覆盖主题的 HTML 模板（同名文件优先于主题）
- `assets/css/extended/custom.css` — 追加自定义 CSS
- `static/` — 静态资源（图片、字体等），发布时直接拷贝到站点根目录

### 文章 frontmatter

```yaml
---
title: "标题"
date: "2026-05-26"
description: "摘要"
tags: ["标签1", "标签2"]
categories: ["分类"]
draft: true       # true=草稿，发布时改为 false 或删掉这行
ShowToc: true     # 显示目录
---
```

### 部署流程

`.github/workflows/deploy.yml` — push 到 main 触发，执行 `hugo --minify` 后部署到 GitHub Pages。要求 Hugo 版本与 workflow 中声明的 `0.153.2` 一致。

### Giscus 评论

`hugo.toml` 末尾已预留 Giscus 配置（注释状态）。启用步骤：
1. 仓库 Settings → 开启 Discussions
2. 访问 giscus.app 生成配置
3. 填入 repoId/categoryId 并取消注释
