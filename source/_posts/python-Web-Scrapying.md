---
#此區稱為front-matter
title: 利用Python達到網路爬蟲的應用
description: 紀錄利用爬蟲應用於股票資訊 #butterfly.yml中 index_post_content 調整, 文章封面會顯示此段文字
date: 2022-10-11 14:00:00
categories: 
  - Project
  - Python
cover: /image//python-Web-Scrapying/python-Web-Scrapying.jpg
tags:
keywords:
abbrlink:
top_img:
#此區稱為front-matter
---

# 前言
相信大家在看股票都要自己想看的資訊，此專案希望可以達到LINE連動python爬蟲讓我每個早晨只需要去LINE按下一個按鍵就可以整理出我想要的股票資訊。
## 環境配置
可以參考兩篇大神的文章: 
1. [1號大神](https://ithelp.ithome.com.tw/articles/10212365)，設定完環境變數記得重新開機才能使變數生效。
2. [2號大神](https://www.learncodewithmike.com/2019/11/python2-visual-studio-code-python.html)，1號大神設定的.json方式，可以透過2號大神的VSCODE裡的settings達成。

Python Requests套件
對網路發動請求的套件，可實作對網頁做get、post等HTTP協定的行為，以後會有詳細的介紹。
'''shell
pip install requests
'''
Python Beautifulsoup4套件
借助網頁的結構特性來解析網頁的工具，只需要簡單的幾條指令就可以提取HTML標籤裡的元素。
'''shell
pip install beautifulsoup4
'''