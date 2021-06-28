---
title: 【JS】webpack 筆記
date: '2021-06-22 00:00:02'
tags: [webpack]
cover: https://i.imgur.com/XRZbeN4.jpg
---

![【JS】webpack 筆記](https://i.imgur.com/XRZbeN4.jpg)

# 版本資訊
- webpack：^5.9.0
- webpack-clil：^4.2.0
- webpack-dev-server：^3.11.0

<br/>

# module.exports 架構
紀錄 webpack.config.js 內的
module.exports 相關設定

- entry：打包檔案執行的進入點，在 SPA 中通常是 index.html 或 index.js
	- main
- output：打包編譯的輸出資訊
	- filename：編譯完的檔名
	- path：編譯完放置的位置
- resolve
	- alias：別名路徑。將特定路徑重新命名
		- stream
- plugins：陣列，放入 webpack 使用的套件與設定其參數。請見 [webpack 套件](#webpack-套件)</a>
- module：載入官方提供的API，定義如何編譯檔案模組
	- rules：模組陣列，有順序性，從上到下依序編譯檔案
		- test：指定編譯檔案的副檔名，使用正規表示式
		- exclude：指定不進行編譯的路徑
		- use：指定使用哪種套件來編譯此種類型檔案
			- loader：指定進行編譯之套件
			- options
				- presets
- devServer：運行 webpack-dev-server 執行本地伺服器
	- port：指定伺服器 port
	- open：是否自動開啟瀏覽器
	- inline：熱加載，程式內容改變後，自行 reload 頁面。
	- hot：熱替換，即 Hot Module Replacement，只替換有改變的部分，不重新加載整個網頁（瀏覽器console會顯示一行 `[HMR] Waiting for update signal from WDS...` 就是這東西在背景執行）
	- stats：控制顯示的編譯訊息層級，預設為 normal（其他等級：errors-only、minimal、verbose）
	- publicPath
	- contentBase
	- watchOptions
		- aggregateTimeout
		- poll
	- watchContentBase
	- historyApiFallback：SPA 使用 html5 history api 時要開啟才能正常使用
	- host
- target：指定編譯目標環境，預設為「web」

<br/>

> ## [Node.js] __dirname 與 path.resolve
> 範例程式碼如下：
> ```
> // webpack.config.js 
> 
> const path = require('path'); 
> module.exports = {
>    output: {
>        path: path.resolve(__dirname, './'),
>    },
> };
> ```
> `__dirname` 是回傳該 js 檔所在資料夾絕對路徑的一個變數，path.resolve 則是 Node.js讀取路徑用的一個方法。
> 
> `path.resolve( RootPath , RelativePath )`方法中，第一個參數是一個絕對路徑，第二個參數則是第一個參數的相對位置，兩者結合回傳一個完整路徑。
> 
> 上面程式碼中，絕對路徑抓取了 webpack.config.js 檔案所在資料夾的絕對路徑，相對路徑則回傳根目錄，兩者結合後， output 的路徑即是 webpack.config.js 檔案所在的資料夾。

<br/>

# webpack 指令&參數
- webpack：編譯部署檔
- webpack serve：啟動本地伺服器
	- --config webpack.config.js：指定config檔，用以區分 develop 檔和 production 檔（讀取 dev 檔可更換為 webpack.dev.js）
	- --mode development：以開發環境編譯，可節省效能與時間
	- --watch：監看程式碼的變更

<br/>

# webpack 套件
> webpack5 已不支援 polyfill

## ● webpack
- webpack
	- [什麼是Webpack? 能吃嗎？](https://medium.com/i-am-mike/%E4%BB%80%E9%BA%BC%E6%98%AFwebpack-%E4%BD%A0%E9%9C%80%E8%A6%81webpack%E5%97%8E-2d8f9658241d)
- webpack-cli：webpack 管理套件
- webpack-dev-server：本地開發用伺服器（協助開發，如自動刷新瀏覽器、HMR 熱加載、指定本地 port 等）

## ● HtmlWebpackPlugin
讓 html 自動加載 webpack 編譯完成的檔案
```
plugins:[
	new HtmlWebpackPlugin({
		title: 'DocumentName',
		template: './src/index.html',
		filename: 'index.html',
	}),
]
```
- title：html 文件名稱，可省略。
	- 如果要使用的話，將 index.html 裡面的 Document Title 改成 `<title><%= htmlWebpackPlugin.options.title %></title>`，即可套用此變數
- template：使用哪個 html 作為基礎模板
- filename：輸出的 html 檔案名稱

## ● CleanWebpackPlugin
每次編譯檔案前，都先刪除前次編譯所有成果，可避免留下之前的舊設定。

## ● Babel
<table>
<tr><th>套件名稱</th><th>說明</th></tr>
<tr><td>babel-loader</td><td>使用 babel 編譯與統整 JavaScript 文件，如 js、jsx 檔等</td></tr>
<tr><td>@babel/core</td><td>babel 核心，轉換 ES6+ 以後的新語法成為多數瀏覽器能夠兼容的語法</td></tr>
<tr><td>@babel/preset-react</td><td>讓 babel 能夠讀懂並編譯 react 語法</td></tr>
<tr><td>@babel/preset-env</td><td>一個你使用了哪些新版 JS 語法，就自動幫你加載相關需求套件的神奇東西</td></tr>
<tr><td colspan="2">以下說明尚不完整，或無實際用過：</td></tr>
<tr><td>babel/plugin-proposal-class-properties</td><td>Babel 專門提供來處理 Class 語法的套件</td></tr>
</table>

## ● Browserify
允許開發人員在瀏覽器上使用 Node.js 擴充模組的套件。

<br/>
<hr>

# 參考資料
[Webpack 前端打包工具 - 使用 webpack-dev-server 實現以 Live Reload 或 HMR 方式進行開發](https://awdr74100.github.io/2020-03-26-webpack-webpackdevserver/)
[Node.js 中的 __dirname、__filename，以及使用相對路徑產生的問題](https://dylan237.github.io/nodejs-dirname-and-filename.html)
[webpack-dev-server 中 inline 和 HMR 的区别](https://juejin.cn/post/6844903481124323341)
[webpack 看我就够了（三）](https://www.jianshu.com/p/b5248d441d9e)
<br/>