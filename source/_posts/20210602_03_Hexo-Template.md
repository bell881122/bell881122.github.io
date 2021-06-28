---
title: 【Hexo】套用樣式
date: '2021-06-02 00:00:03'
tags: [Hexo, blog]
cover: https://cdn.pixabay.com/photo/2016/08/22/12/02/butterfly-1611794_1280.jpg
---

![【Hexo】套用樣式](https://cdn.pixabay.com/photo/2016/08/22/12/02/butterfly-1611794_1280.jpg)

# 目錄
### [Hexo 套用樣式](#Hexo-套用樣式-1)
[下載並套用樣式](#下載並套用樣式)
[Hexo 樣式設定方式](#Hexo-樣式設定方式)
### [使用 Submodule 管理樣式](#使用-Submodule-管理樣式-1)
[使用方法](#使用方法)
[Submodule 持續部署設定](#Submodule-持續部署設定)
### [(補充) Butterfly 參數](#補充-Butterfly-參數-1)
### [參考資料](#參考資料-1)

<br/>

# Hexo 套用樣式
以 Butterfly 為例

## 下載並套用樣式
> 如果要使用 submodule 引進樣式專案，以下程式碼先不要執行

將 GitHub 上的樣式專案複製至 themes/butterfly 路徑
```cmd
git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```
安裝 butterfly 必要插件 hexo-renderer-pug 與 hexo-renderer-stylus
```cmd
npm install hexo-renderer-pug hexo-renderer-stylus --save
// 重啟專案 Ctrl+C
hexo s
```
將根目錄的 _config.yml
theme 屬性改成 butterfly
```yml
# Extensions
theme: butterfly
```
之後就跑 hexo s 執行
開啟 localhost 查看是否成功安裝了

## Hexo 樣式設定方式
> ※此方法只支持 Hexo 5.0.0 以上版本
> butterfly 官方建議使用此方式

butterfly 自己的根目錄內
有一個 _config.yml 檔案
是拿來做 butterfly 設定使用

可以將其複製到 hexo 專案根目錄
取名為 _config.butterfly.yml
Hexo 會以根目錄的 yml 檔為優先
這樣每次套件更新
就不用重新客製化設定檔案

<br/>

# 使用 Submodule 管理樣式
安裝樣式後
有個大煩惱是 Hexo 樣式
本身就是一個 Git Repository
在 Git 裡面直接包 Git
怎樣都感覺怪怪的

此時一個好用的解決方法
是使用 Git Submodule
來加入該樣式

如此 Hexo 主體和樣式便能分開管理
各自更新內容而互不影響
在日後如果要客製化自己的樣式
也可以 fork 該專案
自己管理自己的 Hexo 樣式

## 使用方法
使用 Git Submodule 的方法十分簡單
把 git clone 的 command 改成如下
其他指令按照上面的步驟跑即可
```cmd
git submodule add -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```

主要的 Hexo 專案
可以選擇只紀錄 Git Submodule 版本
並 push 到遠端
如此在多人編輯的狀況下
有另一人更新了 Submodule 版本
也能夠同時吃到該版本

如果要客製化樣式內容
也可以先 Fork 原始樣式專案
同樣加成主專案的 Submodule
這樣即使是客製化的樣式內容
template 跟 Hexo 主專案也能分開管理

## Submodule 持續部署設定
如果是以 Submodule 引入樣式
hexoAcions.yml 檔案裡面
也需要新增部署 submodule 的命令

以下新增在 npm install 指令的前面
```
- name: Update themes
  run: |
  git submodule init
  git submodule update
```

之後再次 commit 推送至遠端
有設定 GitHub Action 的話
應該就會自動部署安裝的 template 囉

> 關於使用 GitHub Action 部署
> 請見 {% post_link 20210602_02_Hexo-CDCI 此篇文章 %}

<br/>

# (補充) Butterfly 參數
樣式的方便性
就在於大部分的東西
都有人幫忙寫好框架
剩下的的東西
只要改一行參數就能簡單解決

以下紀錄自己有使用到的設定
參數全部都在根目錄的以下設定檔中
`_config.butterfly.yml`

參數名稱 | 簡述
--|:--
highlight_theme | 程式碼樣式
highlight_lang | 顯示程式碼語言
social | 社群連結（放在個人頭像底下的 icon），直接使用 Font Awesome 的圖標作為 key，value 則是網址
avatar | 頭像設定，img 是頭像連結，effect 為 true 的話，頭像會持續轉圈圈，預設為 false，只有 hover 時會觸發效果
index_img | 首頁圖片
default_top_img | 如文章無設定封面，將使用此預設圖片
post_copyright | 文章底部預設的版權聲明，enable 預設為 true
addThis / sharejs / addtoany | 分享文章的套件，只能選一種使用，預設是使用 sharejs
index_site_info_top | 主頁標題距離頂部距離
index_top_img_height | 主頁 top_img 高度
footer_bg | footer 背景
global-font-size | 全站文字大小
subtitle | 主頁副標，enable 設為 true 後即可設定副標，effect 為打字效果，副標內容寫在 sub 裡面，用 array 格式 [ 行一, 行二, 行三 ] 分隔多行
aside | 圖像介紹，link 可以修改按鈕連結
card_announcement | 是否顯示公告區，enable 預設為 true，content 為公告內容

<br/>
<hr>

# 參考資料
[hexo-theme-butterfly](https://github.com/jerryc127/hexo-theme-butterfly)
[Butterfly 安裝教學](https://butterfly.js.org/posts/21cfbf15/)
[在 hexo 中使用 git submodules 管理主題](https://juejin.cn/post/6844903751908605965)
<br/>