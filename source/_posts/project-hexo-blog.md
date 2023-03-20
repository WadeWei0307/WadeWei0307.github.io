---
#此區稱為front-matter
title: 第一次架設個人網站(部落格)就上手 (Hexo + GitHub Pages)
date: 2022-10-11 14:00:00
categories: 
  - Project
  - Hexo
cover: https://augustushsu.github.io/uploads/hexo-cover.png
tags:
keywords:
description: 
abbrlink:
top_img:
#此區稱為front-matter
---

# 前言
*原本使用Hackmd當作筆記，但後來想要有自己的網站，可以自定義其他東西、可以記錄自己學過的所有東西、又可以稍微了解一些網站的架設及語法，故興起了我想架設個人網站的念頭。*

![blog post](https://images.unsplash.com/photo-1546074177-ffdda98d214f?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1974&q=80)

## 架設步驟

### 1. 前置作業

在正式安裝 Hexo 之前，要先確保電腦內已經安裝以下軟體。
1. Node.js: 
Hexo 基於 [Node.js](https://nodejs.org/en/) 製作，需要 Node.js 的開發環境。
{% asset_img nodejs.png node js download %}
使用 `$ node -v` 可以查看目前的版本，我這邊使用的是 `v14.16.0` 版本。

2. Git:
需要使用到 [Git](https://git-scm.com/) 來將檔案發佈到 GitHub Pages。

{% asset_img git.png git download %}

### 2. 安裝 Hexo

根據[官方文件](https://hexo.io/zh-tw/docs/)，在終端機(cmd)透過 npm 即可完成 Hexo 的安裝。

``` Shell
$ npm install -g hexo-cli
```

安裝完成後，可以透過cmd並輸入: `hexo -v` 查看 Hexo 版本，並確認是否安裝成功。

## Hexo建立基本專案
### 1. 建立 Hexo 專案

一旦 Hexo 安裝完成後，需要初始化 Hexo 並生成一個 Hexo 專案。

* 切換到你想建立 Hexo 專案的路徑下。

``` Shell
$ cd ~
```

* 初始化 Hexo 並產生一個名叫`blog`的資料夾。

``` Shell
$ hexo init blog
```

* 切換到產生的 Hexo 專案資料夾。

``` Shell
$ cd blog
```

* 安裝 Hexo 所需要的套件。

``` Shell
$ npm install
```

### 2. Hexo 目錄結構

接下來讓我們來介紹一下剛剛建立的 Hexo 專案，在安裝完所需的 npm 套件之後，檔案和資料夾呈現的樣子。

```Text
.
├── .github
├── node_modules
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
├── themes
├── _config.landscape.yml
├── _config.yml
├── .gitgnore
├── db.json
├── package-lock.json
└── package.json
```

* .github 與部署相關。

* node_modules 存放所有安裝的套件。

* scaffolds 會根據這裡的三個檔案`draft.md`、`post.md`、`post.md` 初始化一篇文章。

* source 是存放原始檔案的地方。舉凡 Markdown 和 HTML 檔案都是放在這裡，可以使用 `_` (下底線) 來隱藏資料夾和檔案，避免他們被 Hexo 編譯或是被 copy 到 public 資料夾。 *( `_post` 不受影響)*

* themes 是放置 Hexo 主題的資料夾。預設官方就有提供一個主題  `landscape`，也就是根目錄內的 `_config.landscape.yml`。

* _config.yml 是 Hexo 的主要網站[設定檔](https://hexo.io/zh-tw/docs/configuration)。通常 Hexo 本身會有一個 `_config.yml`，而主題本身也有一個 `_config.yml` 檔案，兩者是不同的。

* .gitgnore 是含有那些不會被上傳至 Git 的檔案和資料夾的名稱。

* db.json 為緩存文件，可以使用 `hexo clean` 清除。

* package-lock.json 記錄當前狀態安裝的每一個套件版本。

* package.json 放置並管理我們透過 npm 下載回來的檔案，也可以將部分指令直接寫在裡面，方便開發。

### 3. 主題選擇

Hexo 提供了上百個[主題](https://hexo.io/themes/)可以讓大家挑選，大家可以從中挑選自己喜歡的主題，並且跟著該主題 Github 的 Installation 安裝即可。

### 4. 建立一篇新的文章

使用 `hexo new [layout] <title>` 來建立一篇新的文章，若標題包含空格，需要用引號括起來。

```shell
$ hexo new post "我的第一篇文章 By Hexo"
```

輸入指令之後，會發現 `source` 的 `_posts` 資料夾多了一個 `我的第一篇文章-By-Hexo.md` 的檔案，接著可以進入該檔案，開始進行文章內容的編輯。

### 5. 標題、日期...

在程式碼最上方由上下兩個 `---` 包夾的區塊為 Front-matter，用來敘述文章的屬性，可以參考官方網站的 [Front-matter](https://hexo.io/zh-tw/docs/front-matter) 取得這些設定值，並加以利用。

```Markdwon
---
title: 第一次架設個人網站(部落格)就上手 (Hexo + GitHub Pages)
date: 2022-10-11 14:00:00
---
```

### 6. 啟動伺服器

透過 `hexo server` 啟動本地伺服器，輸入指令後，終端機會跳出 ` Hexo is running at http://localhost:4000/ `。

這時在瀏覽器的網址頁輸入`http://localhost:4000/`，就可以看到網頁成功出現啦！

### 7. 清除暫存檔案

有時候可能會遇到一些奇怪的問題，例如完成修改樣式之後，部落格樣式卻沒有跟著改變，或是部署完成之後，輸入網頁卻仍然找不到資料...問題，這時候輸入 `hexo clean` 就可以解決掉，主要會清除掉快取檔案 (`db.json`) 以及編譯檔案 (`public`)。

## 部署至 Github 靜態網址

### 1. 建立 GitHub 專案

新增一個公開的 Repsoitory，並且命名為 `[你的 GitHub 帳號].github.io`，這邊注意必須要是<font color="red">[你的 GitHub 帳號]</font>。

以我的部落格為例，respository 的名稱就會是 `WadeWei0307.github.io`，並且需要<font color="red">設定為公開</font>。

{% asset_img new_repository.png repository %}

這樣我們就成功建立了一個網域  `[你的 GitHub 帳號].github.io` 。

### 2. 將檔案發佈到 Git

#### a. 安裝 Git 相關套件

部署前需要安裝一個套件，因為預設 Hexo 並沒有安裝。

```shell=
$ npm install hexo-deployer-git --save
```

#### b. 修改 _config.yml 設定檔

接著需要修改根目錄下的[_config.yml 設定檔](https://hexo.io/zh-tw/docs/one-command-deployment#Git)，有關 deploy 的設定。

{% asset_img deploy_repo.png deploy_repo %}

基本上都是根據上圖中的網址去部署以下的兩個部分：
* Deploy:
```
# Deployment
## Docs: https://hexo.io/docs/one-command-deployment

deploy:
  type: git
  repo: https://github.com/winnielinn/winnielinn.github.io.git 
    # https://github.com/[你的 GitHub 帳號]/[你的 GitHub 帳號].github.io.git

  branch: master # 預設分支名稱
  message:
```

* URL:

```
# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'

url: https://winnielinn.github.io
  # http://yoursite.com
```

#### c. 依序輸入git相關指令

```shell=
git init //先initial git環境
git add . //將該路徑下的專案加到一個節點的存儲區
git commit -m "first commit" //commit到
git branch -M main
git remote add origin https://github.com/WadeWei0307/WadeWei0307.github.io.git
git push -u origin main
```

#### 輸入部署指令

接著輸入 `hexo deploy` 即可部署檔案到網站上 🚀

可以回到 Git 的 Repsoitory 內的 Setting 的 Pages 確認是否部署成功。

{% asset_img deployment.png deployment %}

如果出現 **Your site is published at https://winnielinn.github.io**，那就代表部落格上線成功囉！

如果沒有出現，則需要手動切換 Soucre 到 `master` 並 `save` 後，就可以看到 Hexo 的網站順利地架在 Github 的 Page 上囉✌️

{% asset_img init.png init %} 

#### 修改後的部署

通常在每次完成修改後，會依序輸入 `clean` -> `generate` -> `deploy` 三行指令，避免更新不夠完全：

```
$ hexo cl    // 清除之前建立的靜態檔案
$ hexo g     // 建立靜態頁面
$ hexo d     // 部署至 GitHub
```

## 那些想忘也忘不掉的 Hexo 指令

Hexo 已將所有[指令](https://hexo.io/zh-tw/docs/commands)進行整理，這裡僅列出幾個非常常用的指令，常用到你想忘也忘不掉。

## 心得紀錄

實際在使用 Hexo 框架時，能夠快速套用不同的主題和套件，架設的速度比想像中還要快很多。主要還是在如何修改網站樣式來符合自己的需求上，花了比預期還要多的時間。

目前[網站](https://winnielinn.github.io/)還有很多需要調整的，之後會持續摸索不同的功能，也會慢慢豐富部落格內的文章。

一直以來都想架設一個屬於自己的部落格，想記錄這段時間吸收的知識，畢竟持續的 output 與 input 同等重要，也希望自己整理的技術性文章，能夠幫助到與我同樣在轉職路上前行的人。

>  參考資料如下：
> [Hexo 官方文件](https://hexo.io/zh-tw/docs/)
> [試著學 Hexo - 序章](https://ithelp.ithome.com.tw/articles/10236742)
---
