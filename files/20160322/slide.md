## 島根支社勉強会

2016.3.22

清水　祐太

---
## Electron

---
### Electron(旧Atom-Shell) とは
* デスクトップアプリケーション FW

* HTML / CSS / JS

* Chromium 内臓

* 開発は GitHub

* Windows、Mac、Linux

---
### Electron 製アプリ
* Atom

* Slack

* Visual Studio Code

* Kobit(Qiita)

---
### 類似の FW
* NW.js(node-webkit)

* PhoneGap / Cordova

* Adobe AIR

---
## 作成

---
```
$ npm -g install electron-prebuilt
$ mkdir electron-sample
$ cd electron-sample
$ npm init
```

---
### package.json
```
...
"description": "",
"main": "dist/main.js",
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1"
},
...
```

---
### main.coffee
```
# アプリモジュール
app = require('app')

# ウィンドウモジュール
BrowserWindow = require('browser-window')

# クラッシュレポート
require('crash-reporter').start()

# GCされないようにグローバルで宣言
mainWindow = null

# 全てのウィンドウが閉じたら終了
app.on 'window-all-closed', ->
  if process.platform != 'darwin'
    app.quit()

# Electronの初期化完了後に実行
app.on 'ready', ->
  mainWindow = new BrowserWindow(
    width: 1000
    height: 800)
  mainWindow.loadUrl 'file://' + __dirname + '/index.html'

  # ウィンドウが閉じられたらアプリも終了
  mainWindow.on 'closed', ->
    mainWindow = null
```

---
### index.html
```
<!DOCTYPE html>
<html>

<head>
  <meta charset="UTF-8">
  <title>Sample</title>
  <link href="app.css" rel="stylesheet">
</head>

<body>
  <div id="stopwatch">
    <div id="timer_text">{{text}}</div>
    <div id="start" class="btn" :class="{'active': isStart}" @click="start">Start</div>
    <div id="stop" class="btn" :class="{'active': isStop}" @click="stop">Stop</div>
    <div id="reset" class="btn" :class="{'active': isReset}" @click="reset">Reset</div>
  </div>
</body>
<script src="app.js"></script>
</html>
```

---
## npm、bower 設定

---
### index.coffee
```
window.jQuery = window.$ = require 'jquery'
window.Vue = require 'vue'

new Vue
  el: '#stopwatch'
  data:
    startTime: null
    timerId: null
...
```

---
## デモ

---
## パッケージ化

---
```
$ npm install electron-packager -g
$ electron-packager . stopwatch --platform=darwin --arch=x64 --version=0.37.2
```

* platform ･･･ all / linux / win32 / darwin
* arch ･･･ all / ia32 / x64
* version ･･･ Electron のバージョン

---
### まとめ
* ウェブ開発とほぼ同じ

* Windows / Linux でも動くはず。。

* Chromium 内臓のためかサイズ大

* メニューや通知をしてみたい
