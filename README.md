# AngularJsTutorialMemos #
AngularJsTutorialやりながらのメモ書き

## 前準備 ##

gitからangular phonecatのクローン
node.jsのインストール (v0.10.27+)
npmインストール
bowerインストール

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

phoneCtrlの中身を1件追加してテスト失敗となる
テストを修正し、lengthの結果を4件としてテスト成功
