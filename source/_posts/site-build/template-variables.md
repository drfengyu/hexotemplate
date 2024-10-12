---
title: 模板参数
date: "2024-10-12 09:31:31"
categories: 使用
tags:
- 教程
#sticky:
#cover:
comments: true
toc: false
excerpt: "主题特有的 FrontMatter 参数"
---
目前主题有以下特殊参数：

## 仅对 post 生效

```ts
sticky: number; // 文章是否置顶。数值越大权重越高，置顶越靠前。对于不需要置顶的文章，请注释掉这个参数。默认为不启用。
cover: string; // 文章的封面图片。包含参数但不含值、值为 null 或值为空字符串都会认为是没有封面的文章。对于使用默认封面的文章，请注释掉这个参数。
toc: boolean; // 文章是否生成目录。默认为 false 。
expire: number; // 文章是否会过期，单位是 天 。针对具有时效性的内容，为避免读者没有意识到其时间局限，可以启用这个参数来在指定时间后给出提示。
show_in: ("home" | "category" | "tag")[] ; // 限定文章展示的位置
```

## 对 post 和 page 都生效

```ts
comments: boolean; // 文章/页面是否开启评论区。默认为 true 。
donate: boolean; // 在站点级打赏功能启用时，单独控制文章/页面是否开启打赏功能。默认为 true 。
share: boolean; // 在站点级分享功能启用时，单独控制文章/页面是否开启分享功能。默认为 true 。
```

## 样例

一个完整的 Front-Matter 区样例如下，您可自行删去不必要的内容：

```yaml
title: 样例文章
date: 2018-03-24 15:31:36
categories: 
- 分类层级1
- 分类层级2
- 分类层级3
tags:
- 标签1
- 标签2
- 标签3
sticky: 1
cover: "https://wiki.krt.moe/images/default.webp"
toc: true
expire: 15
show_in:
- home
- category
- tag
comments: true
donate: true
share: true
```
