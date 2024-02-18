---
#此區稱為front-matter
title: 教你如何申請Line Bot，簡單又實用
description: #butterfly.yml中 index_post_content 調整, 文章封面會顯示此段文字
date: 2022-10-11 14:00:00
categories: 
  - Project
  - Python
cover: /image//Apply-Line-Bot/Line Bot.png
tags:
keywords:
abbrlink:
top_img:
#此區稱為front-matter
---

# Line Bot帳號申請步驟
1. 首先可以先至此網址 https://developers.line.biz/zh-hant/ 申請開發者帳號，可以直接使用個人帳號登入。
2. 進入之後可以從右上角頭像進入 <font color="red">LINE Developers Console</font>。
3. 若第一次建立Line Bot，可以從Provider直接新增一個新的Provider。
{% asset_img Line_bot_apply.png Line bot apply image %}
4. 再來就是選取我們要用的Channel服務種類，這裡我們選取訊息服務。
{% asset_img Choosing_Meassaging_API.png Choosing Meassaging API image %}
如此一來，我們就順利建立了屬於我們自己的LINE Bot啦！
# 重要資訊
* Channel secret 可於下圖中 <font color = "red">Basic settings</font> 中找到。
* Channel access token 可於下圖中 <font color = "red">Messaging API settings</font> 中找到。
{% asset_img Line_Channel_home_page.png Line Channel home page image %}
<font size = 5>**最後，此兩個資訊於之後的程式中都會用到，所以要自行保護好，不得讓他人得知。**</font>