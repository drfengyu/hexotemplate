---
title: 配置结构
date: "2024-10-12 09:15:03"
categories: 
- 网站
tags:
- 主题
#sticky:
#cover:
comments: true
toc: true
excerpt: "主题的配置字段详解"
---
主题的配置分为以下几大部分：系统配置、重要功能配置、样式配置、娱乐功能配置、评论与访问量统计、额外的注入代码，以下是分别的解释。

注意这几个层级并属于配置文件的层级结构，而是语义化的分类整理。这篇文档主要也是语义化的解释，具体到每一项精确的控制请参见完整配置文件 [_config.yml](https://github.com/Candinya/Kratos-Rebirth/blob/master/_config.yml) 里的注释内容。

{% collapse "简化的 YAML 语法" %}

由于 YAML 层级较为丰富，在书写的过程中，有时为了简化，您可能会看到一些使用 `.` 分割的配置选项，例如 `vendors.npm_cdn` 这种。

这并不是指有一个配置项就是长这样，而是以下写法的缩略：

```yaml
vendors:
  npm_cdn: # 配置项的值
```

即，如果说将它设置为什么，这其实代表这个结构中 `# 配置项的值` 这一块设置为什么。请注意不要错误地设置到它的上级块去。

{% endcollapse %}

## 系统配置

系统配置主要负责管理与主题底层行为相关的选项。

### 依赖文件

这个是主题使用的资源文件的基础。为了避免最新的依赖文件被投毒导致出现供应链攻击，我们会在主题中留存一份对应版本的依赖文件，并锁定其版本以避免升级时可能带来的混乱。

一般来说，您不需要调整这里的内容。但如果您需要使用 CDN 而不是站点直接提供这些依赖文件，您可以将 `vendors.npm_cdn` 设置为对应 CDN 的路径基础，例如：

- unpkg: "https://unpkg.com/"
- jsdelivr: "https://cdn.jsdelivr.net/npm/"

如果某些依赖出现了较为严重的问题，而我们又没能及时更新这些文件时，您可以手动修改 `vendors.packages` 中对应项的版本（请注意补充对应的文件），来提前使用没有问题的依赖。

### 重要功能配置

这里主要管理几个重要的站点功能。

#### 更新检查、 PJAX 与 ViewerJS

更新检查功能是指在站点运行时，通过公开的 API 检查是否有更新版本的发布。如果有新版本出现，会在控制台打出一行字。如果您需要关闭这个功能（例如出于特殊原因无法使用最新版本），设置 `check_update` 为 `false` 即可。

pjax 是一种网页的动态刷新技术，可以通过脚本来控制替换需要更新的内容，来避免对一些其他有状态内容（例如站点音乐播放器）产生影响。如果您需要关闭这个功能，设置 `pjax` 为 `false` 即可。

ViewerJS 是一个将文章中的图片放大预览的工具，有点类似于 V2 版本中使用的 fancybox ，但不依赖于 jQuery 。如果您需要关闭这个功能，设置 `viewerjs` 为 `false` 即可。

#### 搜索

搜索主要管理的是站点的搜索功能。

主题内置一个简单的本地搜索引擎，即先下载包含所有内容的索引文件，再在浏览器中执行匹配。如果您需要使用这个引擎，那么不需要进行其他额外的配置。如果您需要使用其他的自定义引擎，为了避免这个引擎的影响，请记得将 `search.provider` 改成 `external` ，这样主题就不会注入搜索脚本和生成搜索索引文件，而只会提供一个搜索页面方便您使用自定义的搜索解决方案。如果您不需要站点搜索功能，设置成 `none` 即可禁用掉整个搜索系统。

搜索功能启用时，会生成一个搜索页面；使用本地搜索引擎时，还会同时生成一个搜索索引文件。您可以自定义这两个路径，即修改 `search.path` 中对应的内容即可。

您可以选择搜索功能启用的范围 `search.includes` ，包含可选的 `post` 和 `page` ，分别表示针对文章和页面启用搜索。 `search.content` 则表示是否包含这些范围的具体内容，设置为 `false` 则表示仅包含标题。

## 样式配置

样式配置主要管理站点表现出来的样子。

### 图片配置

图片配置主要是指一些固定的媒体资源，例如图标、头像、横幅、背景和关于小挂件的背景图片的配置。

针对横幅和背景还提供了亮色模式和暗色模式下的两种配置方案可供切换，如果只想使用一种的话则设置为一样的值即可。

请注意，文章的默认封面配置不在这里。

### 导航栏配置

这里管理的是站点的导航栏（桌面端在顶部，移动端通过右上角的按钮打开）的样式和显示的内容。

在桌面端时，为了避免导航栏挡住视线，当页面向上滚动时导航栏会被控制向上收缩。如果需要禁用掉这个功能以让导航栏一直固定住，那么可以将 `nav,auto_hide` 设置为 `false` 。

`nav.items` 是导航栏具体显示的项目内容，其遵循这样的格式定义：

```ts
interface NavItem {
  label: string;
  icon?: string;
  url: string;
}

interface NavItemWithSubmenu extends NavItem {
  submenu?: NavItem[];
}

type NavItems = NavItemWithSubmenu[];
```

其中，仅有一级菜单的项目可以配置 submenu ，二级菜单的子菜单会被忽略（即不存在三级菜单）。

icon 可以使用 [FontAwesome Icons 4.7.0](https://fontawesome.com/v4/icons/) 中的图标，例如想要用 home 的话输入 `home` 即可。如果没有合适的图标，也可以自行粘贴对应的 HTML 内容，例如可以从 [Tabler Icons](https://tabler.io/icons) 寻找并复制 SVG 。

{% alertbar info "

没有引入更大的图标库是因为浏览器加载也是需要消耗性能的，引入的图标库过大（例如 Tabler ），使用 WebFont 格式加载时候就会导致整个页面的渲染阻塞，从而影响访客的浏览体验。

" %}

### 文章的列表配置

这个主要调整首页的文章布局。目前只能设置 `index.style` 这一个选项，可选 `card` 或是 `half` 。

- 当设置为 `card` 模式时，首页文章会以经典的 Kratos 卡片样式来展示；
- 设置为 `half` 模式时，会以 Hexo 经典的展开一半，点击阅读更多来查看后续部分的样式来展示（可以参考默认主题 landscape）。选择您最喜欢的样式就好。

### 页脚配置

这个主要调整页脚部分的显示内容。页脚主要分为上下两部分，上部分显示一些链接与对应的图标，下部分显示站点的基础信息。

链接 `footer.links` 遵循这样的格式定义：

```ts
interface FooterLink {
  icon: string;
  link: string;
  addition?: string;
}

type FooterLinks = FooterLink[];
```

addition 一般情况下可以不用设置。

站点的基础信息也分为两大块：固定显示的内容和扩展显示的内容。

固定显示的内容有两行：

1. 第一行为站点的版权信息和运行时间信息。 `footer.components.uptime` 可以配置运行时间信息的详细内容，包括建站时间和提示文本。
2. 第二行为使用的主题和站点作者的信息。其中主题信息不可更改，个人主页链接可以通过 `footer.components.author.homepage` 来配置，未配置则仅显示文字而不创建链接。

扩展显示的内容为二维数组，第一维决定扩展的行，第二维决定行内的顺序。以下是一个简单样例（请注意是二维数组）：

```yaml
footer:
  components:
    additional:
      - - 由 <a href="https://hexo.io" target="_blank" rel="nofollow">Hexo</a> 强力驱动
        - 在 <a href="https://github.io" target="_blank">Github Pages</a> 暖心托管
      - - 这里是另一行追加的信息
        - 这里是这个追加信息的第二部分
```

### 文章配置

文章配置主要管理文章页渲染时的样式，包含 `card` 模式下的默认图片配置、文章内页的默认功能配置、字数统计配置和文章目录渲染配置。

`posts.default_cover` 控制的是没有头图的文章在使用 card 模式下的默认图片。如果您有配合随机图片工具使用的需要，您可以使用一张加载中的图标以避免让访客感到疑惑。

`posts.donate` 和 `posts.share` 控制的是当文章没有具体设置时，是否启用对应的功能。一种适用场景例如设置为 true 作为所有文章的默认，然后再在搬运翻译的文章内部设置 [模板参数](/posts/site-build/template-variables/) 为 `false` 来指定停用。

`posts.word_count` 管理的是字数统计功能相关的配置，即在文章页标题栏下方显示的元数据中，是否包含文章本身的字数统计信息。如果不需要这个功能，直接设置 `posts.word_count.enable` 为 `false` 即可。

`posts.toc` 控制的是文章目录的显示。对于桌面端来说，文章目录组件是侧边栏上的小挂件；对于移动端来说，则是文章顶部的一个固定结构。

### 一般页面配置

这里目前只有 `pages.donate` 和 `pages.share` 两项，功能与文章配置中的相同，此处就不多赘述了。

### 代码高亮

这个配置的是代码高亮工具相关的参数。例如 `syntax_highlighter.theme` 配置的是具体应用的高亮主题样式。

对于 highlight.js 来说，目前有这几个内置的主题可供选择：

- `light`
- `night`
- `night-blue`
- `night-bright`
- `night-eighties`

对于 prismjs 来说，目前有这几个内置的主题可供选择：

- `atom-dark`

如果您不喜欢这些内建的主题，而是想要引入其他的主题对应的样式表文件，可以将这个选项设置为 `false` 。也非常欢迎您提交一个 PR 来引入其他的主题配色样式。

### 侧边栏与小挂件

这个配置的是窗口宽度大于 991px 时，主题的侧边栏与侧边栏里对应的小挂件的样式。

`sidebar.location` 管理的是侧边栏的模式（位置）。主题有三种侧边栏模式：左侧边栏 `left`、右侧边栏 `right` 和无侧边栏 `false`。

`sidebar.widgets` 管理的是启用的小挂件和对应的顺序。其中各个小挂件如下：

- `about` 关于
- `toc` 文章目录
- `category` 分类列表
- `tagcloud` 标签聚合
- `posts` 最新文章

另外还有一个不属于挂件的特殊配置 `splitter` 分割线，决定当页面向下滚动时，从哪里开始变为粘滞位置（即固定在页面上）。

其中 `toc` 挂件因为涉及到文章的内容，所以仅会在启用了这个功能的文章页出现，在首页和一般页面不会出现。

一个默认推荐的侧边栏配置样式如下：

```yaml
sidebar:
  widgets:
    - about
    - splitter
    - toc
    - category
    - tagcloud
    - posts
```

您也可以自行调整对应组件的顺序，或是改变侧边栏的位置等。

### 分享与打赏

这两个功能的结构类似但又有些不同。相似的部分有：都在文章或页面的底部，都是弹出窗口，都会显示文字，都有一个二维码区域。不同的地方在于分享功能的二维码固定为文章的链接，而打赏的二维码随着平台选择不同而改变；分享功能设置的链接是一串会被注入页面信息的模板，而打赏功能设置的是具体的指向平台的链接。

一个简单的分享平台配置样例如下所示，这个分享包含了两个平台：微博和 Twitter (X) 。它展示了两种不同的图标用法，以及特殊的模板注入字符串。

```yaml
share:
  platforms:
    - name: "微博"
      icon: "weibo"
      color: "#e6162d"
      link: "https://service.weibo.com/share/share.php?url=$URL&title=$TITLE"
    - name: "X"
      icon: |
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="icon icon-tabler icons-tabler-outline icon-tabler-brand-x">
          <path stroke="none" d="M0 0h24v24H0z" fill="none" />
          <path d="M4 4l11.733 16h4.267l-11.733 -16z" />
          <path d="M4 20l6.768 -6.768m2.46 -2.46l6.772 -6.772" />
        </svg>
      color: "#000"
      link: "https://x.com/intent/tweet?text=$TITLE&url=$URL"
```

模板字符串中可以使用的变量有：

| 变量     | 解释     | 样例                                             |
| -------- | -------- | ------------------------------------------------ |
| $URL     | 页面路径 | https://eco.krt.moe/posts/other-share/index.html |
| $TITLE   | 页面标题 | 分享平台                                         |
| $SUMMARY | 页面描述 | 为 Kratos : Rebirth 主题添加自定义分享平台支持   |
| $SITE    | 站点名称 | Kratos : Rebirth                                 |

对于打赏来说，如果使用 QR Code 来在页面上展示，那么在对应项的 `qrcode` 处需要填写二维码的具体文本内容。可以使用一些基础的工具从二维码中提取文本信息，例如 [SecScanQR](https://github.com/Fr4gorSoftware/SecScanQR) 。

一个简单的打赏配置样例如下所示：

```yaml
donate:
  platforms:
    - name: "支付宝"
      icon: |
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="icon icon-tabler icons-tabler-outline icon-tabler-brand-alipay">
          <path stroke="none" d="M0 0h24v24H0z" fill="none" />
          <path d="M19 3h-14a2 2 0 0 0 -2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2 -2v-14a2 2 0 0 0 -2 -2z" />
          <path d="M7 7h10" />
          <path d="M12 3v7" />
          <path d="M21 17.314c-2.971 -1.923 -15 -8.779 -15 -1.864c0 1.716 1.52 2.55 2.985 2.55c3.512 0 6.814 -5.425 6.814 -8h-6.604" />
        </svg>
      color: "#1677ff"
      qrcode: "example_alipay_qrcode"
    - name: "微信支付"
      icon: "wechat"
      color: "#38ad5a"
      qrcode: "example_wechatpay_qrcode"
```

### 版权提示

主题支持两种版权提示配置：固定在内容页面底部的提示行，和在复制内容时自动追加的补充说明文本。

要启用固定提示行，需要在 `copyright_notice.in_page.enable_at` 中设置对应的部分，例如 `post` 和 `page` 。一个简单的样例如下所示：

```yaml
copyright_notice:
  in_page:
    enable_at:
      - post
      - page
```

针对复制时追加内容的模板，有这些变量可供使用：

| 变量     | 解释     |
| -------- | -------- |
| $NEWLINE | 换行符   |
| $AUTHOR  | 站点作者 |
| $TITLE   | 页面标题 |
| $LINK    | 当前链接 |

## 评论与访问量统计

为避免官方维护不及时导致评论系统老旧过时，主题不再内置的评论与访问量系统支持，而是使用灵活的配置方案和高度自定义的注入代码功能来引入不同的提供平台。

评论系统分为两大模块：评论区和评论数量统计。评论区是实际用于加载评论功能的组件，而评论数量统计则是在首页或页面元数据处用于展示数量使用的。针对不同的评论解决方案，我们提供了一个专门的分区来索引，您可以参考 [分类：评论](https://eco.krt.moe/categories/%E8%AF%84%E8%AE%BA/) 。如果您有新的评论系统支持，非常欢迎向对应仓库开启一个 PR 。

访问数量统计则只有一个模块，有点类似于评论数量统计。我们同样提供了一个索引分区 [分类：访问统计](https://eco.krt.moe/categories/%E8%AE%BF%E9%97%AE%E7%BB%9F%E8%AE%A1/) 。

有些评论或访问统计工具对唯一 ID 的长度有限制，使用默认不定长的路径作为 ID 可能会导致其工作不正常，此时您可以使用提供的 `path_hasher` 来引用指定的数据摘要算法，对路径进行摘要计算以生成一个定长的十六进制唯一标识。默认的算法是 `md5` ，如果您有使用其他算法的需要，可以参考 [crypto.createHash](https://nodejs.org/api/crypto.html#cryptocreatehashalgorithm-options) 节的内容。

以上配置中模板里的字符串遵循这样的规则：

1. 在启用了对应功能的不同页面中，注入使用的模板字符串会使用 `template._shared` 和 对应页面的模板进行拼接。
2. 注入器会替换掉模板中的一部分变量字符串：
   - `$PATH` 包含站点次级目录的相对路径
   - `$PATH_HASH` 相对路径的摘要
   - `$PATH_FULL` 包含站点源的完整 URL

## 额外的注入代码

主题支持往已有的结构中注入一些自定义的组件，例如额外的追加样式表、额外追加的脚本文件等，主题的扩展功能也是主要依靠这些来实现的。对于一般使用来说这部分内容不需要太多深究，直接参考生态项目中给出的对应实现即可；如果您想要为主题开发周边的生态支持，可以参考 [周边开发流程](/posts/ecosystem-develop-workflow/) 里的描述。
