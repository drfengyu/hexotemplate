---
title: C#项目Git忽略项
categories:
  - git
tags:
  - git
comments: true
toc: true
donate: true
share: true
date: 2024-10-15 16:01:08

---
在 C# 项目上传github时，通常你需要忽略一些自动生成的文件、编译输出和用户配置文件。以下是一个基本的 `.gitignore` 文件示例：

```gitignore
# Visual Studio相关
.vs/
*.user
*.suo
*.userosscache
*.sln.docstates

# 编译输出
bin/
obj/

# NuGet包
*.nupkg
**/packages/*
!**/packages/build/
!**/packages/repositories.config

# 锁文件
project.lock.json
project.fragment.lock.json

# 样式和排版
*.ide/workspace.xml

# 临时文件
*.tmp
*.temp

# 部署相关
publish/

# 外部工具
_ReSharper.Caches/

# 文件历史
.history/

# 本地环境设置
*.local.json
```

根据项目的特殊需求，你可能需要调整或添加额外的规则。
