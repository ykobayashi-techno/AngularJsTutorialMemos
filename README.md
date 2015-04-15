# AngularJsTutorialMemos #
AngularJsTutorialやりながらのメモ書き

## 前準備 ##

gitからangular phonecatのクローン
node.jsのインストール (v0.10.27+)
npmインストール
bowerインストール

npm installで入るはずのchromeDriverがYosemite環境で解凍できず、以下からChromeDriver2.15をDLして配置
https://sites.google.com/a/chromium.org/chromedriver/downloads

動作確認したところ大丈夫

### サーバースタート ###

    npm start

http://localhost:8000/app/index.html
  
### ユニットテスト ###

    npm test

Karmaというtest runner

### E2Eテスト ###

    npm run protractor
  
protractor

## Tutorial / 0 - Bootstrap(始める) ##

    <html ng-app>
    +
    <script src="bower_components/angular/angular.js">

* {{}} *を使用したバインディングの方法
* 

## Tutorial / 1 - Static Template

angularJS、バインディングの仕組みを使用しない通常のHTMLの書き方

## Tutorial / 2 - Angular Templates

angularJS、バインディングの仕組みを利用した動的なページ
controllerの中身、bodyタグに記述するngControllerディレクティブ要素

コントローラのUnitTest
書き方はJasmineという方法
* Jasmine使い方メモ *
http://qiita.com/opengl-8080/items/cf3acafda9756f4b04c9

phoneCtrlの中身を1件追加してテスト失敗となる
テストを修正し、lengthの結果を4件としてテスト成功
