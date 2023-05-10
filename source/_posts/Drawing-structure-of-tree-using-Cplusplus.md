---
title: Drawing structure of tree using C++
description: #butterfly.yml中 index_post_content 調整, 文章封面會顯示此段文字
date: 2023-03-29 22:38:41
categories:
  - Project
  - C++
tags:
keywords:
abbrlink:
top_img:
#此區稱為front-matter
---

# 前言
可以透過輸入root畫出自己建的樹狀圖，讓我們可以在寫程式時可以圖像化自己建造的data structure，以至於更容易想像及應用在後續的程式發展。
# 環境配置
## include graphics.h
1. 先擁有[Visual Studio](https://visualstudio.microsoft.com/zh-hant/vs/features/cplusplus/)。
2. 下載[graphics.h](https://github.com/ahuynh359/Graphics)相關檔案。
3. 下載完後，將檔案解壓縮至C++ project folder。
{% asset_img project_folder.jpg project_folder img %}
4. 打開專案檔，並`對專案點擊右鍵`，然後`選取屬性`。
{% asset_img project_property.png project property img %}
並且點選`組態管理員`，然後做以下的設定：
{% asset_img configuration_manager.png configuration manager img %}
5. 然後import header file `graphics.h`，`winbgim.h`。
6. 最後要link graphics.lib檔，必須在.cpp上面加上以下程式碼。
```c=
#pragma comment(lib,"graphics.lib")
```
如此就大功告成了！
