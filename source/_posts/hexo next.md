---
title: hexo next 教學
date: 
description: 架設博客教學
tags: 
- [教學]
mathjax: true
---

## 下載軟體

> ### Node.js
> 
> 下載位置：[下載 | Node.js](https://nodejs.org/zh-tw/download/)

<img src="https://i.imgur.com/ub2U0xs.png" alt="安裝介面" style="zoom:33%;" />

windows 用戶點<font color="#FC4E4E">紅色</font>圈起來的，mac 用戶點<font color="#00A2E8">藍色</font>圈起來的

下載好之後開起下載的檔案然後安裝，基本上只要一直點 next 就好了

> ### Git
> 
> 下載位置：[Git - Downloads](https://git-scm.com/downloads)

<img src="https://i.imgur.com/v6LwRcv.png" style="zoom:33%;" />

windows 用戶點<font color="#FC4E4E">紅色</font>圈起來的 `Download for Windows`

下載好之後開起下載的檔案然後安裝，基本上只要一直點 next 就好了

> ### Vscode
>
> 下載位置：[Download Visual Studio Code](https://code.visualstudio.com/download)



<img src="https://i.imgur.com/xToEIWN.png" style="zoom:33%;" />

直接下載就可以用了

windows 用戶點<font color="#FC4E4E">紅色</font>圈起來的，mac 用戶點<font color="#75F94D">綠色</font>圈起來的

> ### 文章編輯器 Typora
>
> 下載位置：[Typora — a markdown editor, markdown reader.](https://typora.io/#download)

<img src="https://i.imgur.com/DW5u5sE.png" style="zoom:33%;" />

點<font color="#FC4E4E">紅色</font>圈起來的

這個軟體使用起來是免費的，所以不用擔心，如果之後看到以下畫面

<img src="https://i.imgur.com/uZJS8rH.png" style="zoom:50%;" />

就點 `不是現在` 即可

## 架設 hexo

### 建立博客根目錄

#### For win11

我們先建立一個名為 `hexo` 的資料夾(在哪裡建立都 ok)

接著對你建立的名為 `hexo` 的資料**左鍵點一下** $\rightarrow$ 接著再點擊右鍵 $\rightarrow$ 點擊在終端中開啟

> 注意: 如果沒有先用左鍵點**一下**資料夾他是不會顯示「在終端中開啟」這個選項的

<img src="https://i.imgur.com/fitXCVt.png" alt = "點擊「在終端中開啟」" style="zoom:50%;" />

#### For else

在搜尋攔搜尋 cmd，按 enter 開啟，接著就按照你 `hexo ` 資料夾的位置去 `cd <folder>` ，直到進到 `hexo` 資料夾內

例如我目前在 `C:\Users\yozen` 

而我有安裝 onedrive 所以我的 hexo 路徑在 `C:\Users\yozen\Onedrive\桌面\projects\hexo` 

以下就是我需要 cd 的路徑

<img src="https://i.imgur.com/aq7kdxd.png" alt="範例" style="zoom: 67%;" />

### 檢查

在終端機(以下都稱作 `cmd` 內) 輸入以下指令

```powershell
node -v
npm -v
```

- `node -v` 查詢安裝的 node 版本
- `npm -v` 查詢安裝的 npm 版本
- 正確的話系統就會回報版本給你

> 記得要先按裝好上面的軟體下載再來檢查，不然一邊下載一邊開著 cmd 是不會成功的

如果都沒有出現 <font color="#FC4E4E">error(紅字)</font> 代表 ok

### 利用 npm 下載 Hexo

- 接著繼續在 `cmd` 內輸入以下指令

- 在執行完 `npm install hexo-cli -g` 後，看到 `cmd` 顯示 `INFO Start blogging with Hexo!`，代表有安裝到

```powershell
npm install hexo-cli -g
hexo init
```

{% note danger no-icon %}

#### 如果出現以下警告



![](https://i.imgur.com/yi9JAA0.png)

---

在搜尋欄搜尋 `Windows PowerShell`，對他點擊右鍵

$\rightarrow$ 點擊以**「系統管理員身分執行」**，如下圖

<img src="https://i.imgur.com/UGSTxmq.png" style="zoom:50%;" />

開啟後打上以下指令
```powershell
Set-ExecutionPolicy RemoteSigned
```

![](https://firebasestorage.googleapis.com/v0/b/welcomewebworld-4097b.appspot.com/o/blogImg%2Fother%2F2020-05-10_22-38-18.png?alt=media&token=68a6e168-1ee6-4864-a4d3-73d576e74e24)

按下(輸入 A) [A] 就可以了

你就可以再回去試試看執行 `npm`  指令了

{% endnote %}

### 在自己的電腦上啟動 Hexo

輸入以下指令來啟動 Hexo

```powershell
hexo s
```

- 執行指令後，若有看到這行字的話，就表示我們安裝成功了

```powershell
INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop
```

- 之後我們打開瀏覽器 (Chrome, Firefox)，在網址列輸入 http://localhost:4000/ 就可以看到 Hexo 的畫面了 (如下圖)。

<img src="https://ycjhuo.gitlab.io/assets/img/20-01.8ceaf1f7.png" style="zoom: 50%;" />

## 建立文章

- 要建立新文章的話，在這個資料夾底下 `hexo\source\posts` 建立 `檔名.md` (檔名自訂) 即可
- 你會看到內建有一篇 `hello world.md` 那個可以刪掉，或者你直接用他去改都 ok
- 至於裡面的內容，一定要先至少打上

```yml
---
title: 
date: 
description: 
tags: 
---

```

- title : 文章的標題
- date : 發布文章的時間 (可以留空)
- description: 在博客主頁面會顯示的簡述 (可留空)
- tags : 標籤

在下面的部分 (第 6 行之後) 就可以開始撰寫文章的正文了，以下提供一個範例
```yml
---
title: My first blog
date: 2020-09-17 21:18:00
description: whats up guys
tags: 
- [blog]	
- [test]
---

This is my first post.
```

- 寫好後，重新整理 http://localhost:4000/ 即可看到變化

## 加上 NexT 主題

```powershell
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

<img src="https://i.imgur.com/zaU56V9.png" style="zoom:60%;" />

再來到 `hexo\_config.yml`  (這裡的 `hexo` 是指網站一開始的資料夾)

可以用 vscode 來開啟檔案 

下載完後在 vscode 用 `ctrl + F`  搜尋  `# Extensions`，並進行以下設置：

```yml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next 
```

改 `theme: next `

再來我們在打上 

```powershell
hexo clean
hexo s
```

再去  http://localhost:4000/ 就可以看到變化了，如果要停止網站在 `cmd` 按 `ctrl+c` 即可

之後每次開啟本機端的博客都是先 `hexo clean` 再 `hexo s` 就可以啟動了

<img src="https://img.guiblogs.com/hexo30-5/demo-next.jpg" alt="Next 佈景主題樣式" style="zoom: 50%;" />

## 網站資訊設定

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

- title : 你的部落格標題
- subtitle : 你的部落格副標題
- description : 部落格簡介
- keywords :  網站關鍵字，多個關鍵字用逗號隔開
  - 例如 `keywords : '關鍵字1', '關鍵字2'`
- author : 作者名字
- language : 語言，繁體中文請改成 `language: zh-TW`
- timezone : 使用系統時間即可

記得更改完後要 `hexo clean`, `hexo s` 才能看到更動

## 將頁面上傳到 github.io

### 新增儲存庫

如果你本身已經有 Github 帳號或是剛辦好的，那就可以新增儲存庫了。首先來到已經為登入狀態的 Github 任一頁面，右上角會有個「+」按鈕，按下去後會出現下拉式選單，點擊第一個「New repository」。

![點擊新增儲存庫](https://i.imgur.com/iuCXGcf.png)

此時請在你的 Reponsitory name 輸入「你的 Github 帳號.github.io」

例如我就是 `yozen0405.github.io`

![填寫網址](https://i.imgur.com/gJDSfqc.png)

填寫完成往下滑按下「Create repository」後，如果看到以下畫面就代表成功囉！此時，右上角是否有看到一個 HTTPS 的網址？請將它複製起來，待會會用到。

![儲存庫建立成功](https://i.imgur.com/MXgtC5S.png)

### 設定 Hexo 連結儲存庫

部署前要先設定 Hexo 的 `_config.yml` 檔案中連接到 Github 儲存庫的相關設定，首先要找到 `# Deployment` 這段（基本上預設會在檔案最下面）：

```yml
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git # 使用 Git 部署
  repo: https://github.com/Github帳號/Github帳號.github.io.git # 你的儲存庫 clone
  branch: gh-pages # 儲存庫分支
  message: "First Commit" # Commit 訊息
```

- type：部署類型
- repo：儲存庫 clone (就是剛剛要你複製的那串，貼上去)
- branch：儲存庫分支 
- message：Commit 訊息

這是我的設定，可以參考

```yml
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: git # 使用 Git 部署
  repo: https://github.com/yozen0405/yozen0405.github.io.git
  branch: gh-pages # 儲存庫分支
  message: "First Commit" # Commit 訊息
```

- 預設可能只有 type 而已，然而**必須加上 repo、branch 等資訊才能進行部署**（畢竟要設定部署的儲存庫嘛），message 不是必要的，不過我建議還是加，這樣整體在看的時候比較能夠一目了然每一次的部署是為了什麼而更新

- 再來就是 **冒號後必須空一個空白在接設定值！**

### 上傳到 github

在 `hexo` 資料夾用終端機開啟 (`cmd`)

輸入以下指令

```
hexo clean
```

部署 Hexo 必須要安裝 `Hexo-deployer-git Git` 部署套件，因此需要執行以下指令安裝：

```powershell
npm install hexo-deployer-git --save
```

再來就要執行 `hexo d` Hexo 的部署指令，就會開始將我們前面產生的靜態網頁部署到 Github Pages 

```powershell
hexo d 
```

{% note danger no-icon %}

#### 如果顯示一大堆警告



在 `cmd` 輸入以下指令

```powershell
git config --global user.name github_user_name
git config --global user.email github_user_email
```

其中 `github_user_name` 與 `github_user_email` 需替代成你 github 的名稱與榜定的 email

例如我就是

```powershell
git config --global yozen0405
git config --global yozen0405@gmail.com
```

{% endnote %}

如果執行後如圖這樣，恭喜你成功部署上去啦！打上 `https://你的github名字/你的github名字.github.io` 即可看到

<img src="https://i.imgur.com/OSjiRTi.png" alt="Hexo 檔案成功部署到 Github" style="zoom:50%;" />

### 公開部落格頁面

<img src="https://i.imgur.com/znpEkeJ.png" style="zoom:33%;" />

點擊 `Settings`

<img src="https://i.imgur.com/Z0B2kFS.png" style="zoom:33%;" />

點擊 `Pages`

<img src="https://i.imgur.com/Jo7fktP.png" style="zoom:33%;" />

點擊紅色框起來的部分就可以看到妳的網站了

{% note danger no-icon %}

#### 怎麼沒有顯示紅色框起來的部分 ?

因為你目前的博客還在部署中，要再等一段時間才可

以下圖片框起來的地方可以看到目前部署的狀態，若是<font color="EF9B0F">黃色</font>代表部署中，<font color="green">綠色</font>代表已完成部署

![](https://i.imgur.com/Rslfrvw.png)

{% endnote %}

{% note info %}

之後每次要從本地端將你的資料丟到 github.io 上就直接 `hexo clean`, `hexo d` 即可

{% endnote %}

## 備註

優化 hexo next 設定的部分，我把它寫在另一個文章，可以點下面的按鈕過去

<div class="text-center"><a class="btn" href="/2023/03/25/hexo%20next2/" title="閱讀"><i class="fa fa-arrow-right fa-fw fa-lg"></i>後篇教學</a></div>