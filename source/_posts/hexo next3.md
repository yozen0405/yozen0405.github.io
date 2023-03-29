---
title: hexo next 備份原始檔到 github
date: 
description: 在不同的電腦上同步更新博客
tags: 
- [教學]
- [github]
- [hexo next]
mathjax: true
---

## 前言

這是「第 3 篇 : 備份原始檔到 github」的教學，讓你可以在不同電腦都可以編輯，以下是全部教學篇的總覽

{% note info no-icon %}

### <i class="fa fa-bars"></i> 總覽
- <a href="/2023/03/23/hexo%20next/">第 1 篇 : 架設博客</a>
- <a href="/2023/03/25/hexo%20next2/">第 2 篇 : 博客設定優化</a>
- <a href="/2023/03/27/hexo%20next3/">第 3 篇 : 備份原始檔到 github</a>

{% endnote %}

## 備份到 github

我們先進入到你的博客根目錄 (例如我的是名為 `hexo` 的資料夾)

到這個根目錄開啟 `cmd`

<img src="https://i.imgur.com/oBbc0ej.png" alt = "在 hexo 開啟 cmd" style="zoom:73%;" />

打上以下指令

```
git init
```

接著去你的 github.io，按下 `Code` 這個按鈕，然後按複製

<img src="https://i.imgur.com/PFy0FYG.png" alt="按下 Code 這個按鈕，然後按複製" style="zoom:50%;" />

```
git remote add origin 你剛剛複製的把它覆蓋在這裡
```

例如我的就是 

```
git remote add origin https://github.com/yozen0405/yozen0405.github.io.git
```

再來繼續在 cmd 打上以下指令，會顯示很多 warnings，是正常的，不用理他

```
git add .
```

然後再打上

```
git commit -m '自訂訊息'
```

「自訂訊息」的部分可以自己取，代表的是現在你目前是第幾個 update，或是第幾個 version 等等

例如我們是第一次傳到 github 所以我就把它叫做

```
git commit -m 'Initial commit'
```

然後再打上

```
git push -u origin master
```

然後你就去你的 github.io 的 github file 介面點擊 master (如圖)

![點擊左上角的 gh-pages 再點 master](https://i.imgur.com/FT5GBzb.png)

就可以看到你 clone 的 file 了

## 從 github 拉到本地端

### 已有套件

如果在電腦上已經寫過博客，那麼可以在已有的工作目錄下同步之前寫的博客
在你博客根目錄 (我的根目錄叫 `hexo` 的資料夾)下開啟 cmd，輸入以下指令

> 記得如果你有裝什麼新的插件而這台電腦沒有的話要再安裝一下

```
git pull
```

{% note info %}

因為你已有套件，所以直接跳到[成果這裡](/2023/03/27/hexo%20next3/#成果)

{% endnote %}

### 沒有套件

#### clone 到本地端

去你的 github.io 的 github file 頁面，按下 `Code` 這個按鈕，然後按複製

<img src="https://i.imgur.com/PFy0FYG.png" alt="按下 Code 這個按鈕，然後按複製" style="zoom:50%;" />

> 如果你是新電腦，那也還需要重新下載我<a href="/2023/03/23/hexo%20next/">第一篇</a>教學所提到的軟體，git 也要重新登入

開一個新的資料夾，名字自取，然後在這個資料夾開啟 cmd 輸入以下指令 

```
git clone 你剛剛複製的把它覆蓋在這裡
```

例如我的就是

```
git clone https://github.com/yozen0405/yozen0405.github.io.git
```

然後你會看到裡面出現了一個「你的名字.github.io」的資料夾，我們要輸入以下指令

```
cd 你的名字.github.io
git checkout master 
```

切換好後，如果檔案由原先的各個被產生的靜態網頁變成像是過去在本機設定 Hexo 時的那些檔案，就代表切換成功囉！

#### 將套件與佈景安裝回來

node_modules 目錄放置的是我們平常安裝的套件，因為備份時沒有備份到它，此時我們要重新安裝回來。

```
npm install
```

執行完指令後，開啟根目錄下的 `package.json` 檔案，紀錄我們過去安裝的一些套件，也請將這些套件安裝回來。

```
git install 套件名稱 --save
```

重新將 Next 主題下載回來：

```
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

### 成果

在你博客根目錄 (我的根目錄叫 `hexo` 的資料夾)下開啟 cmd，輸入以下指令

```powershell
hexo g
hexo s
```

就可以看看是否有還原成功囉！不過一些設定可能還是要再做一下，並且檢查是否還有一些地方需要進行修正。