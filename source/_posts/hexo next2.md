---
title: hexo next 設定優化
date: 
description: 博客設定優化
tags: 
- [教學]
mathjax: true
---

## 前言

這是基於第一篇教學的優化，還沒看過第一篇可以點這裡

<div class="text-center"><a class="btn" href="/2023/03/23/hexo%20next/" title="閱讀"><i class="fa fa-arrow-left fa-fw fa-lg"></i>前篇教學</a></div>

## Scheme 設定

到 `hexo\themes\next\_config.yml` 找到以下語法

```yml
# ---------------------------------------------------------------
# Scheme Settings
# ---------------------------------------------------------------

# Schemes
scheme: Muse
#scheme: Mist
#scheme: Pisces
#scheme: Gemini

# Dark Mode
darkmode: false
```

將 `scheme: Gemini` 註解打掉並將 `scheme: Muse` 加上註解 `#`

開啟黑暗模式的話就把 `darkmode: false` 改成 `darkmode: true`

## 設定頁尾作者鏈結

到 `hexo\config_yml` 找到以下代碼 :

```yml
# Site
title: Hexo 
subtitle: '' 
description: '' 
keywords: 
author: John Doe 
language: en 
timezone: '' 
```

將 author 改成你的名字

![](https://img.guiblogs.com/hexo30-6/footer-author-text.jpg)

到 `hexo\themes\next\_config.yml` 找到以下這段語法：

```yml
# If not defined, `author` from Hexo `_config.yml` will be used.
copyright:
```

如果想插入連結，撰寫 HTML a 鏈結語法，設定完成後就可以看到頁尾作者文字變成了鏈結

```
copyright: "<a href='指定鏈結'>你的名字</a>"
```

![變更頁尾作者名字，順便設定成超鏈結](https://img.guiblogs.com/hexo30-6/footer-author-link.jpg)

### 去除強力驅動

到 `hexo\themes\next\layout\_partials\footer.swig` 找到以下代碼 :

```html
{% if theme.footer.powered %}
  <div class="powered-by">{#
  #}{{ __('footer.powered', '<a class="theme-link" target="_blank" href="https://hexo.io">Hexo</a>') }}{#
#}</div>
{% endif %}
```

直接把上面所展示的代碼全部刪掉就可以了

## 圖片點擊放大插件

到 `hexo\themes\next\source\lib` 開啟 cmd 

輸入以下指令

```powershell
git clone https://github.com/theme-next/theme-next-fancybox3 fancybox
```

到 `hexo\themes\next\_config.yml` 找到以下代碼 :

```yml
# FancyBox is a tool that offers a nice and elegant way to add zooming functionality for images.
# For more information: https://fancyapps.com/fancybox
fancybox: 
```

更改為 `fancybox: true` ，重新 `hexo clean`, `hexo s` 就可以了

## 主選單設置

<img src="https://i.imgur.com/ohpaBfP.png" alt="Next 主選單設置" style="zoom:70%;" />

### 新增自訂頁面

```powershell
hexo new page "頁面名稱（網址用）"
```

例如我就新增了

```powershell
hexo new page about
```

### 存放位置與頁面資訊

有別於文章與草稿有各自不同的目錄存放，**頁面檔案是獨立存放於一個目錄中的**，像是我剛剛建立了 about 頁面，頁面存放位置於 `hexo\source\about` 內，而檔案名稱為 `index.md`。

因此如果你要將草稿建立成頁面，假設你的頁面叫做「message」，就要在 source 目錄內建立一個名為 message 的目錄，將草稿檔案移進去目錄後，將檔案名稱改為 `index.md` 即可。

如果我們想使頁面不能留言，就再加上 `comments: false `

```
title: about
date: 2021-08-28 18:46:39
comments: false 
```

### 利用主選單連到頁面

開啟 `hexo\themes\next\_config.yml` 檔案並找到以下語法：

```yml
menu:
  home: / || fa fa-home
  #about: /about/ || fa fa-user
  #tags: /tags/ || fa fa-tags
  #categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
  #schedule: /schedule/ || fa fa-calendar
  #sitemap: /sitemap.xml || fa fa-sitemap
  #commonweal: /404/ || fa fa-heartbeat
```

我們只要將 `#about` 那一行解除註解即可。不過如果你的關於頁面不是設定成 about（或許可能是你的英文名字），那就改成你設定的名稱即可。

### 標籤頁面優化

待補

### 搜尋功能

待補

## 閱讀進度條

頂部或是底部有個進度條，隨著你的閱讀進度進行滑動。

在 `hexo\themes\next\_config.yml` 找到以下這段語法：

```yml
# Reading progress bar
reading_progress:
  enable: false
  # Available values: top | bottom
  position: top
  color: "#37c6c0"
  height: 3px
```

- enable：設定是否開啟進度條，開啟則設定 true
- position：設定進度條在頂部還是底部顯示
- color：進度條背景顏色
- height：進度條高度

將 `enable: true` 即可

## 回到頂部按鈕

![](https://i.imgur.com/9rtDXiJ.png)

在 `hexo\themes\next\_config.yml` 找到以下這段語法：

```yml
back2top:
  enable: true
  # Back to top in sidebar.
  sidebar: false
  # Scroll percent label in b2t button.
  scrollpercent: false
```

- 將 sidebar 設定為 true：設定在側邊欄的個人資訊區塊中，Social Links 下，顯示回到頂部按鈕
- 將 scrollpercent 設定為 true：回到頂部按鈕旁加上閱讀進度百分比。

## 閱讀全文按鈕

在文章想切斷的地方加入以下這行(獨立的一行)

```markdown
<!-- more -->
```

{% note info no-icon %}

### 如何始點擊「閱讀全文」自動跳到最頂層?

{% note default %}

如果你覺得點擊閱讀全文就應該從切斷的地方繼續讀那可以跳過這裡

{% endnote %}

到 `hexo\themes\next\lauout\_macro\post.swig` 裡面找到以下語法

```
   <!--/noindex-->
{% elif post.excerpt %}
        {{ post.excerpt }}
        <!--noindex-->
        {%- if theme.read_more_btn %}
    <div class="post-button">
            <a class="btn" href="{{ url_for(post.path) }}#more" rel="contents">
        {{ __('post.read_more') }} &raquo;
            </a>
    </div>
        {%- endif %}
        <!--/noindex-->
```

<img src="https://i.imgur.com/lfp2wYE.png" alt="刪除反白的 #more" style="zoom: 33%;" />

將 `#more` 刪掉即可 (上面圖片有反白)

{% endnote %}

## 程式碼區塊樣式

在 `hexo\themes\next\_config.yml` 找到以下這段語法：

```yml
codeblock:
  # Code Highlight theme
  # Available values: normal | night | night eighties | night blue | night bright | solarized | solarized dark | galactic
  # See: https://github.com/chriskempson/tomorrow-theme
  highlight_theme: normal
  # Add copy button on codeblock
  copy_button:
    enable: false
    # Show text copy result.
    show_result: false
    # Available values: default | flat | mac
    style:
```

將 `highlight_theme: normal` 改成 `highlight_theme: night bright`

## 加上數學式

在 `hexo\themes\next\_config.yml` 中：

```yml
# Math Formulas Render Support
math:
  # Default (true) will load mathjax / katex script on demand.
  # That is it only render those page which has `mathjax: true` in Front-matter.
  # If you set it to false, it will load mathjax / katex srcipt EVERY PAGE.
  per_page: true

  # hexo-renderer-pandoc (or hexo-renderer-kramed) requi#FC4E4E for full MathJax support.
  mathjax:
    enable: true
    # See: https://mhchem.github.io/MathJax-mhchem/
    mhchem: false

  # hexo-renderer-markdown-it-plus (or hexo-renderer-markdown-it with markdown-it-katex plugin) requi#FC4E4E for full Katex support.
  katex:
    enable: false
    # See: https://github.com/KaTeX/KaTeX/tree/master/contrib/copy-tex
    copy_tex: false
```

在 window powershell 打上以下指令

```powershell
npm uninstall hexo-renderer-marked --save
npm install hexo-renderer-pandoc --save
```

另外需要注意，如果置 `mathjax: true`，且使用了 `hexo-renderer-kramed` 渲染引擎，會遇到一行只能使用一個行內公式的情況。

解決方法是到路徑 `hexo\node_modules\kramed\lib\rules\inline.js` 將

```js
var inline = {
  escape: /^\\([\\`*{}\[\]()#$+\-.!_>])/,
  // ...
  em: /^\b_((?:__|[\s\S])+?)_\b|^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
  // ...
};
```

修改為

```js
var inline = {
  escape: /^\\([`*\[\]()#$+\-.!_>])/,
  // ...
  em: /^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
  // ...
};
```

最後，記得在想使用 latex math 的檔案下，加上 `mathjax: true`

<img src="https://i.imgur.com/UmFMIeL.png" style="zoom:67%;" />

就可以使用 $\LaTeX$ 了

## 添加作者頭像

到 `hexo\themes\next\_config.yml` 找到下面這行

```yml
# Sidebar Avatar
avatar:
  # Replace the default image and set the url here.
  url: 
  # If true, the avatar will be dispalyed in circle.
  rounded: false
  # If true, the avatar will be rotated with the cursor.
  rotated: false
```

- url : 網址
- rounded: 是否圓框
- rotated: 是否在鼠標移到上面時旋轉一圈

將自訂的圖片傳到 `hexo\themes\next\source\images` 然後在 `url: ` 後面打上 `\images\檔案名稱 + 格式`

例如我加入了一張名為 `coffee.jpg` 的圖片，以下是我的 code

```yml
# Sidebar Avatar
avatar:
  # Replace the default image and set the url here.
  url: /images/coffee.jpg
  # If true, the avatar will be dispalyed in circle.
  rounded: true
  # If true, the avatar will be rotated with the cursor.
  rotated: false
```

## 增設留言區

代補

 ## 在文章撰寫特殊區塊

### note

```jinja
{% note [class] [no-icon] %}
文章內容
{% endnote %}
```

- `[class]`  :  note 格式，有六種選項 : `default` , `primary`, `success`, `info`, `warning` , `danger`
- `[no-icon]` : 打上 `no-icon` 即可將 icon 去除

以下是範例

````jinja
{% note  success no-icon %}

#### 標題

這裡是內容
> 支援引用區塊
```
也支援程式碼區塊
```

{% endnote %}
````



{% note  success no-icon %}
#### 標題

這裡是內容



```
也支援程式碼區塊
```
> 支援引用區塊
{% endnote %}

#### 更改 note 樣式

到 `hexo\themes\next\_config.yml` 中找到以下代碼

```yml
# Note tag (bs-callout)
note:
  # Note tag style values:
  #  - simple    bs-callout old alert style. Default.
  #  - modern    bs-callout new (v2-v3) alert style.
  #  - flat      flat callout style with background, like on Mozilla or StackOverflow.
  #  - disabled  disable all CSS styles import of note tag.
  style: flat
  icons: true
  # Offset lighter of background in % for modern and flat styles (modern: -12 | 12; flat: -18 | 6).
  # Offset also applied to label tag variables. This option can work with disabled note tag.
  light_bg_offset: 0
```

- 更改 `style: flat` 為以下選擇
  -  `style: modern `
  -  `style: simple `
  -  `style: flat `

### 頁籤功能

看一下範例 :

{% tabs mytab,2 %} 將 tab 取名為 mytab，預設會選取第二個頁籤，使用 -1 會不選取
<!-- tab -->
#### 頁籤一

因沒有特別命名，所以此頁籤會用 `mytab` 加上流水號。
<!-- endtab -->
<!-- tab -->
#### 頁籤二

開無痕進來會先看到我。
<!-- endtab -->
<!-- tab 這是頁籤三 -->
#### 頁籤三

這裡有命名，會看到頁籤名不一樣。
<!-- endtab -->
<!-- tab -->
#### 頁籤四

可以看到這裡的流水號是從 4 開始，應該是抓 array index 作為流水號。
<!-- endtab -->
<!-- tab 個人資料 @user -->
#### 頁籤五

這裡有加 icon，有什麼 icon 可以來[這裡](https://fontawesome.com/icons)找。
<!-- endtab -->
{% endtabs %}

在文件中打上 :

```markdown
{% tabs mytab,2 %} 將 tab 取名為 mytab，預設會選取第二個頁籤，使用 -1 會不選取
<!-- tab -->
### 頁籤一

因沒有特別命名，所以此頁籤會用 `mytab` 加上流水號。
<!-- endtab -->
<!-- tab -->
### 頁籤二

開無痕進來會先看到我。
<!-- endtab -->
<!-- tab 這是頁籤三 -->
### 頁籤三

這裡有命名，會看到頁籤名不一樣。
<!-- endtab -->
<!-- tab -->
### 頁籤四

可以看到這裡的流水號是從 4 開始，應該是抓 array index 作為流水號。
<!-- endtab -->
<!-- tab 個人資料 @user -->
### 頁籤五

這裡有加 icon，有什麼 icon 可以來[這裡](https://fontawesome.com/icons)找。
<!-- endtab -->
{% endtabs %}
```

### spoiler

在 `hexo` 開啟 `cmd` ，打上以下指令

```powershell
npm install hexo-sliding-spoiler --save
```

修改 `hexo\node_modules\hexo-sliding-spoiler\assets\spoiler.css` 為以下 code

{% spoiler code %}

```css
.spoiler {
    margin: 5px 0;
    padding: 0 15px;
    border: 3px solid rgb(105, 105, 105);
    position: relative;
    clear: both;
    border-radius: 3px;
}

.spoiler .spoiler-title {
    background: rgb(105, 105, 105);
    opacity: 1;
    margin: 0 -15px;
    padding: 5px 15px;
    color: rgb(200, 200, 200);
    font-weight: bold;
    font-size: 14px;
    display: block;
    cursor: pointer;
}

.spoiler .spoiler-title:before {
    font-weight: bold;
}

.spoiler.collapsed .spoiler-title:before {
    content: "▲ ";
}

.spoiler.expanded .spoiler-title:before {
    content: "▼ ";
}

.spoiler .spoiler-content {
    padding-top: 0;
    padding-bottom: 0;
    margin-top: 0;
    margin-bottom: 0;
    -moz-transition-duration: 0.3s;
    -webkit-transition-duration: 0.3s;
    -o-transition-duration: 0.3s;
    transition-duration: 0.3s;
    -moz-transition-timing-function: ease-in-out;
    -webkit-transition-timing-function: ease-in-out;
    -o-transition-timing-function: ease-in-out;
    transition-timing-function: ease-in-out;
}

.spoiler.collapsed .spoiler-content {
    overflow: hidden;
    max-height: 0;
}

.spoiler.expanded .spoiler-content {
    max-height: 3000px;
    overflow: hidden;
}

.spoiler .spoiler-content p:first-child {
    margin-top: 0 !important;
}
```

{% endspoiler %}

用法就是跟 note 差不多，在 markdown 文件打上

```markdown
{% spoiler 顯示文字 %}
隱藏內容
{% endspoiler %}
```

以下是範例

````markdown 範例
{% spoiler "點擊隱/顯內容" %}

隱藏的內容
支持 markdown 語法，代碼塊，數學式

```c++
#include <bits/stdc++.h>
using namespace std;
int main() {
	cout << "Hello World!" << '\n';
	return 0;
}
```

$$
e^{ix} = cosx+isinx
$$

{% endspoiler %}
````

{% spoiler "點擊隱/顯內容" %}

隱藏的內容
支持 markdown 語法，代碼塊，數學式

```c++
#include <bits/stdc++.h>
using namespace std;
int main() {
	cout << "Hello World!" << '\n';
	return 0;
}
```

$$
e^{ix} = cosx+isinx
$$

{% endspoiler %} 

## 加入 emoji

在 `hexo` 資料夾開啟 `cmd` 打上 :

```powershell
npm install hexo-filter-emoji
```

然後就可以在 markdown 檔案用了

用法 : `:emoji_name:` 跟 discord emoji 的用法一樣

## 自訂樣式

### 建立 styles.styl

{% note info %}

若要進行下面的設置，請務必要先看怎麼建立 `styles.styl` 檔案 

{% endnote %}

 在 `hexo\themes\next\_config.yml` 中找到

```yml
# Define custom file paths.
# Create your custom files in site directory `source/_data` and uncomment needed files below.
custom_file_path:
  #head: source/_data/head.swig
  #header: source/_data/header.swig
  #sidebar: source/_data/sidebar.swig
  #postMeta: source/_data/post-meta.swig
  #postBodyEnd: source/_data/post-body-end.swig
  #footer: source/_data/footer.swig
  #bodyEnd: source/_data/body-end.swig
  #variable: source/_data/variables.styl
  #mixin: source/_data/mixins.styl
  #style: source/_data/styles.styl
```

將 `#style: source/_data/styles.styl` 的註解弄掉

然後去 `hexo\source` 裡面新建一個名為 `_data` 的資料夾 (名稱一定要是 `_data` 不可自行更換)

進入你建立的 `_data` 資料夾內，建立名為 `styles.styl` 的文件

### 連結顏色更改

在 `hexo\source\_data\styles.styl` 加上：

```css
// 修改選中文字底色
/* webkit, opera, IE9 */
::selection { 
    background: #00c4b6;
    color: #f7f7f7; 
}
/* firefox */
::-moz-selection { 
    background: #00c4b6;
    color: #f7f7f7;    
}
```

如果想修改 note 裡面的連結顏色，加上 :

```css
.post-body .note p a, .post-body .note p span.exturl {
  color: #0593d3;
  border-bottom: none;
  border-bottom: 1px solid #0593d3;
  &:hover {
    color: #fc6423;
    border-bottom: none;
    border-bottom: 1px solid #fc6423;
  }
}
```

### 反白顏色更改

在 `hexo\source\_data\styles.styl` 加上

```css
::selection {
    background: #3390FF;
    color: white;
}
```

上面只包含了文章的反白顏色 (不含 `note`)

以下是 `note` 的反白顏色，一樣加在 `hexo\source\_data\styles.styl` 

```css
.post-body .note {
  ::selection {
    background: #C4E7E8;
    color: black;
  }
}
```

### 加上背景圖片

在 `hexo\source\_data\styles.styl` 加上

```css
body {
      background:url(圖片網址);
      background-size: cover;
      background-repeat: no-repeat;
      background-attachment: fixed;
      background-position:center center;
}
```

- 如果是在網路上的圖片，複製圖片位址，然後將 「圖片網址」改成你複製的圖片位址
- 如果是在本地的圖片，存在 `hexo\source\images` (如果沒有此資料夾自己創建一個)，然後把「圖片網址」改成 `/images/檔案+格式`
  - 例如 `/images/img.jpg`

### 文章透明

在 `hexo\source\_data\styles.styl` 加上

```css
.content-wrap {
  opacity: 0.95;
}

.side bar {
  opacity: 0.95;
  color: white;
}

.popup {
  opacity: 0.95;
}
```

其中的 `opacity: 0.95` 是透明度，可以自己調整

### 修改字體顏色

在 `hexo\source\_data\styles.styl` 加上

```css
body {
    color: #EBEBEB; // 全局字體顏色
}
```

這裡修改了文章的字體顏色，如果想進一步修改 note 的顏色，請加上

```css
.post-body .note {
  color: black; // note 字體顏色
}
```

### 行內代碼塊顏色

在 `hexo\source\_data\styles.styl` 加上

```css
code {
  padding: 2px 4px;
  word-wrap: break-word;
  color: #c7254e;
  background: #f9f2f4;
  border-radius: 3px;
  font-size: 18px;
}
```
