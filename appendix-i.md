# Appendix I. Markdown & GitBook

Markdown 的目标是实现「易读易写」。  
Markdown是一种可以使用普通文本编辑器编写的标记语言，通过简单的标记语法，它可以使普通文本内容具有一定的格式。  
同时**Markdown也兼容HTML标签**。

> Markdown 旨在简洁、高效，也由于 Markdown 的易读易写，人们用不同的编程语言实现了多个版本的解析器和生成器，这就导致了目前不同的 Markdown 工具集成了不同的功能（基础功能大致相同），例如流程图与时序图，复杂表格与复杂公式的呈现，虽然功能的丰富并没有什么本质的缺点，但终归有些背离初衷，何况在编写的过程中很费神，不如使用专业的工具撰写来的更有效率，所以如果你需实现复杂功能，专业的图形界面工具会更加方便。当然，如果你对折腾这些不同客户端对 Markdown 的定制所带来高阶功能感到愉悦的话，那也是无可厚非的。

## Markdown 语法

### 标题

标题是每篇文章都需要也是最常用的格式，在 Markdown 中，如果一段文字被定义为标题，只要在这段文字前加 \# 号即可。

`\# 一级标题`  
`\## 二级标题`  
`\### 三级标题`

以此类推，总共六级标题，建议在**\#**后加一个空格，这是最标准的 Markdown 语法。

### 列表

熟悉 HTML 的同学肯定知道有序列表与无序列表的区别，在 Markdown 下，列表的显示只需要在文字前加上 - 或 \* 即可变为无序列表，有序列表则直接在文字前加1. 2. 3. 符号要和文字之间加上一个字符的空格。

* 列表1
* 列表2

* 列表1

* 列表2 

### 引用

如果你需要引用一小段别处的句子，那么就要用引用的格式。

> 例如这样  
> 这样

只需要在文本前加入 &gt; 这种尖括号（大于号）即可

### 图片与链接

插入链接与插入图片的语法很像，区别在一个 !号

```

图片为：![](){ImgCap}{/ImgCap}

链接为：[]()

插入图片的地址需要图床

```
### 粗体与斜体

Markdown 的粗体和斜体也非常简单，用两个 * 包含一段文本就是粗体的语法，用一个 * 包含一段文本就是斜体的语法。
例如：**这里是粗体** *这里是斜体*
### 表格

表格是我觉得 Markdown 比较累人的地方，例子如下：

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

### 代码框
`行内代码`

```

代码块示例

```
### 分割线

分割线的语法只需要三个 * 号，例如：
***

## 参考文档
[Markdown语法说明](http://wowubuntu.com/markdown/#list)

[Markdown入门指南](http://www.jianshu.com/p/1e402922ee32/)

## GitBook
GitBook is a command line tool (and Node.js library) for building beautiful books using GitHub/Git and Markdown (or AsciiDoc).
### GitBook.com

[GitBook.com](https://www.gitbook.com) 是进行GitBook管理、编写发布图书的在线版本。使用GitBook.com可以免去本地安装GitBook、编辑图书、发布的一系列操作，转而在线上完成。

[GitBook Editor](https://www.gitbook.com/editor) 是GibBook.com的本地可视化编辑工具。

### 本地安装GitBook

##### 必备工具

Installing GitBook is easy and straightforward. Your system just needs to meet these two requirements:

* NodeJS (v4.0.0 and above is recommended)
* Windows, Linux, Unix, or Mac OS X

##### 使用 NPM 安装

The best way to install GitBook is via **NPM**. At the terminal prompt, simply run the following command to install GitBook:

```
$ npm install gitbook-cli -g
```

`gitbook-cli` is an utility to install and use multiple versions of GitBook on the same system. It will automatically install the required version of GitBook to build a book.

##### 创建Book

GitBook can setup a boilerplate book:

```
$ gitbook init
```

If you wish to create the book into a new directory, you can do so by running `gitbook init ./directory`

首先，创建如下目录结构：

```
book/
├── README.md
└── SUMMARY.md
```

README.md 和 SUMMARY.md 是两个必须文件，README.md 是对书籍的简单介绍：

```
This is a book powered by [GitBook](https://github.com/GitbookIO/gitbook).
```
SUMMARY.md 是书籍的目录结构。内容如下：
```
* [Chapter1](chapter1/README.md)
  * [Section1.1](chapter1/section1.1.md)
  * [Section1.2](chapter1/section1.2.md)
* [Chapter2](chapter2/README.md)
```
创建了这两个文件后，使用 `gitbook init`，它会为我们创建 SUMMARY.md 中的目录结构。

```
.
├── README.md
├── SUMMARY.md
├── chapter1
│   ├── README.md
│   ├── section1.1.md
│   └── section1.2.md
└── chapter2
    └── README.md
```


预览:

```
$ gitbook serve
```

生成静态Website:

```
$ gitbook build
```

##### Install pre-releases

`gitbook-cli` makes it easy to download and install other versions of GitBook to test with your book:

```
$ gitbook fetch beta
```

Use `gitbook ls-remote` to list remote versions available for install.

##### Debugging

You can use the options `--log=debug` and `--debug` to get better error messages (with stack trace). For example:

```
$ gitbook build ./ --log=debug --debug
```

### Configuration

GitBook allows you to customize your book using a flexible configuration. These options are specified in a `book.json` file. For authors unfamiliar with the JSON syntax, you can validate the syntax using tools such as [JSONlint](http://jsonlint.com).

#### General Settings

| Variable | Description |
| -------- | ----------- |
| `root` | Path to the root folder containing all the book's files, except `book.json`|
| `structure` | To specify paths for Readme, Summary, Glossary etc. See [Structure paragraph](#structure). |
| `title` | Title of your book, default value is extracted from the README. On GitBook.com this field is pre-filled. |
| `description` | Description of your book, default value is extracted from the README. On GitBook.com this field is pre-filled. |
| `author` | Name of the author. On GitBook.com this field is pre-filled. |
| `isbn` | ISBN of the book |
| `language` | [ISO code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) of the book's language, default value is `en` |
| `direction` | Text's direction. Can be `rtl` or `ltr`, the default value depends on the value of `language` |
| `gitbook` | Version of GitBook that should be used. Uses the [SemVer](http://semver.org) specification and accepts conditions like `">= 3.0.0"` |

#### Plugins

Plugins and their configurations are specified in the `book.json`. See [the plugins section](plugins/README.md) for more details.

Since version 3.0.0, GitBook can use themes. See [the theming section](themes/README.md) for more details.

| Variable | Description |
| -------- | ----------- |
| `plugins` | List of plugins to load |
| `pluginsConfig` |Configuration for plugins |

#### Structure

In addition to the `root` variable, you can tell Gitbook the name of the files for Readme, Summary, Glossary, Languages (instead of using the default names such as `README.md`).
These files must be at the root of your book (or the root of every language book). Paths such as `dir/MY_README.md` are not accepted.

| Variable | Description |
| -------- | ----------- |
| `structure.readme` | Readme file name (defaults to `README.md`) |
| `structure.summary` | Summary file name (defaults to `SUMMARY.md`) |
| `structure.glossary` | Glossary file name (defaults to `GLOSSARY.md`) |
| `structure.languages` | Languages file name (defaults to `LANGS.md`) |

#### PDF Options

PDF Output can be customized using a set of options in the `book.json`:

| Variable | Description |
| -------- | ----------- |
| `pdf.pageNumbers` | Add page numbers to the bottom of every page (default is `true`) |
| `pdf.fontSize` | Base font size (default is `12`) |
| `pdf.fontFamily` | Base font family (default is `Arial`) |
| `pdf.paperSize` | Paper size, options are `'a0', 'a1', 'a2', 'a3', 'a4', 'a5', 'a6', 'b0', 'b1', 'b2', 'b3', 'b4', 'b5', 'b6', 'legal', 'letter'` (default is `a4`) |
| `pdf.margin.top` | Top margin (default is `56`) |
| `pdf.margin.bottom` | Bottom margin (default is `56`) |
| `pdf.margin.right` | Right margin (default is `62`) |
| `pdf.margin.left` | Left margin (default is `62`) |

### Plugins

Plugins are the best way to extend GitBook functionalities (ebook and website). There exist plugins to do a lot of things: bring math formulas display support, track visits using Google Analytic, etc.

#### How to find plugins?

Plugins can be easily searched on [plugins.gitbook.com](https://plugins.gitbook.com).


#### How to install a plugin?

Once you find a plugin that you want to install, you need to add it to your `book.json`:

```
{
    "plugins": ["myPlugin", "anotherPlugin"]
}
```

You can also specify a specific version using: `"myPlugin@0.3.1"`. By default GitBook will resolve the latest version of the plugin compatbile with the current GitBook version.

#### GitBook.com

Plugins are automatically installed on [GitBook.com](https://www.gitbook.com). Locally, run `gitbook install` to install and prepare all plugins for your books.

#### Configuring plugins

Plugins specific configurations are stored in `pluginsConfig`. You have to refer to the documentation of the plugin itself for details about the available options.

### 主题插件
用户可以通过在 NPM 上搜索 `gitbook-theme` 来查找主题插件
#### ComScore
ComScore 是一个彩色主题，默认的 gitbook 主题是黑白的，也就是标题和正文都是黑色的，而 ComScore 可以为各级标题添加不同的颜色，更容易区分各级标题。

### 实用插件
gitbook 也有很多实用性插件，用户可以在 GitHub 或者 NPM 上搜索 `gitbook-plugin` 来查找。
#### Disqus
Disqus 是一个非常流行的为网站集成评论系统的工具，同样，gitbook 也可以集成 disqus 以便可以和读者交流。
首先，需要在 disqus 上注册一个账号，然后添加一个 website，这会获得一个关键字，然后在集成时配置这个关键字即可。
##### 安装 disqus 插件

可以参考 插件项目主页 来安装，命令如下：
```
$ npm install gitbook-plugin-disqus -g
```
然后，修改 book.json 配置文件，添加插件的配置内容：
```
{
    "plugins": ["disqus"],
    "pluginsConfig": {
        "disqus": {
            "shortName": "introducetogitbook"
        }
    }  
}
```
>注意：上面的 shortName 的值就是你在 disqus 上创建的 website 获得的唯一关键字。

#### multipart
multipart 插件可以将书籍分成几个部分，例如：
```
GitBook Basic
GitBook Advanced
```
对有非常多章节的书籍非常有用，分成两部分后，各个部分的章节都从 1 开始编号。

## 示例



```
book.json
{
    "title": "Webpack 中文指南",
    "description": "Webpack 是当下最热门的前端资源模块化管理和打包工具，本书大部分内容翻译自 Webpack 官网。",
    "language": "zh",
    "plugins": [
    "disqus",
    "github",
    "editlink",
    "prism",
    "-highlight",
    "baidu",
    "splitter",
    "sitemap"
    ],
    "pluginsConfig": {
        "disqus": {
            "shortName": "webpack-handbook"
        },
        "github": {
            "url": "https://github.com/zhaoda/webpack-handbook"
        },
        "editlink": {
            "base": "https://github.com/zhaoda/webpack-handbook/blob/master/content",
            "label": "编辑本页"
        },
        "baidu": {
            "token": "a9787f0ab45d5e237bab522431d0a7ec"
        },
        "sitemap": {
            "hostname": "http://zhaoda.net/"
        }
    }
}

```
安装插件：
```

gitbook install ./

```

```

editlink

内容顶部显示 编辑本页 链接。

ad

在每个页面顶部和底部添加广告或任何自定义内容。

splitter

在左侧目录和右侧内容之间添加一个可以拖拽的栏，用来调整两边的宽度。

image-captions

抓取内容中图片的 alt 或 title 属性，在图片下面显示标题。

github

在右上角显示 github 仓库的图标链接。

anchors

标题带有 github 样式的锚点。

chart

使用 C3.js 图表。

styles-sass

使用 SASS 替换 CSS。

styles-less

使用 LESS 替换 CSS。

ga

添加 Google 统计代码。

disqus

添加 disqus 评论插件。

sitemap

生成站点地图。

latex-codecogs

使用数学方程式。

mermaid

使用流程图。

book-summary-scroll-position-saver

自动保存左侧目录区域导航条的位置。

sharing

默认的分享插件。

fontsettings

默认的字体、字号、颜色设置插件。

search

默认搜索插件。

tbfed-pagefooter

自定义页脚，显示版权和最后修订时间。

prism

基于 Prism 的代码高亮。

atoc

插入 TOC 目录。

ace

插入代码高亮编辑器。

highlight

默认的代码高亮插件，通常会使用 prism 来替换。

github-buttons

显示 github 仓库的 star 和 fork 按钮。

sectionx

分离各个段落，并提供一个展开收起的按钮。

mcqx

使用选择题。

include-codeblock

通过引用文件插入代码。

fbqx

使用填空题。

spoiler

隐藏答案，当鼠标划过时才显示。

anchor-navigation

锚点导航。

youtubex

插入 YouTube 视频。

redirect

页面跳转。

expandable-chapters

收起或展开章节目录中的父节点。

baidu

使用百度统计。

duoshuo

使用多说评论。

jsfiddle

插入 JSFiddle 组件。

jsbin

插入 JSBin 组件。

```

### 参考文档

[GitBook官方说明](https://github.com/GitbookIO/gitbook)

[GitBook简明教程](http://www.chengweiyang.cn/gitbook/index.html)

[GitBook使用教程](http://blog.csdn.net/axi295309066/article/details/61420694)
