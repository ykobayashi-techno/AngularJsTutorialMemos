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

## Tutorial / 3 - Filtering Repeaters ##
inputタグ、queryを使用して現在の要素にフィルターをかける

        <div class="col-md-2">
            <!--Sidebar content-->
        
            Search: <input ng-model="query">
        </div>
        <div class="col-md-10">
            <!--Body content-->
            <ul class="phones">
                <li ng-repeat="phone in phones | filter:query">
                    {{phone.name}}
                    <p>{{phone.snippet}}</p>
                </li>
            </ul>
        </div>
    </div>
    
E2Eテストの方法

## Tutorial / 4 - Two-way Data Binding ##
双方向のバインディングについて
HTML側から変数を参照するのではなく、Controller側からHTMLへ
Selectタグを使用し、Controller側でデフォルト値をセットする

HTML：

        Search: <input ng-model="query">
        Sort by:
        <select ng-model="orderProp">
          <option value="name">Alphabetical</option>
          <option value="age">Newest</option>
        </select>
        
        <ul class="phones">
          <li ng-repeat="phone in phones | filter:query | orderBy:orderProp">
            <span>{{phone.name}}</span>
            <p>{{phone.snippet}}</p>
          </li>
        </ul>

JS：

        $scope.orderProp = 'age';

## Tutorial / 5 - XHRs & Dependency Injection ##

httpサービスを利用して取得したデータの表示
successに関数を渡して処理する

### Testについて ###
通常テスト用に$httpを実装するが、Angularでは*$httpBackend*に擬似的なレスポンスを設定して使用できる

        var scope, ctrl, $httpBackend;
        
        beforeEach(module('phonecatApp'));
        beforeEach(inject(function(_$httpBackend_, $rootScope, $controller) {
            $httpBackend = _$httpBackend_;
            $httpBackend.expectGET('phones/phones.json').
            respond([{name: 'Nexus S'}, {name: 'Motorola DROID'}]);
        
            scope = $rootScope.$new();
            ctrl = $controller('PhoneListCtrl', {$scope: scope});
        }));

## Tutorial / 6 - Templating Links & Images ##

リンクと画像について
画像はそのままsrcではなく、ng-src="{{source}}"と書くことで初期化前に存在しない場所へのアクセスを防ぐ

        <ul class="phones">
          <li ng-repeat="phone in phones | filter:query | orderBy:orderProp" class="thumbnail">
            <a href="#/phones/{{phone.id}}" class="thumb"><img ng-src="{{phone.imageUrl}}"></a>
            <a href="#/phones/{{phone.id}}">{{phone.name}}</a>
            <p>{{phone.snippet}}</p>
          </li>
        </ul>

Testでng−srcをsrcに変更し、存在しない場所へアクセスしたことを確認

## 7 - Routing & Multiple Views ##

angular-route.jsを読み込み、ngRouteモジュールと必要なControllerを渡す

index.html以外へテンプレートを移動  
PhoneListCtrlとPhoneDetailCtrlという、一覧と詳細用ビューのコントローラを作成

    var phonecatApp = angular.module('phonecatApp', [
        'ngRoute',
        'phonecatControllers'
    ]);

## 8 - More Templating ##

端末の詳細ビューの作成

### テスト ###

Nexus-Sの画像の取得を行い画像が四件存在するか確認

    var imageList = element.all(by.repeater('img in phone.images'));
    expect(imageList.count()).toBe(4);

## 9 - Filters ##

カスタムフィルタ。true falseを✔、×に置き換え

フィルタを作成してDIに加える

controller

    angular.module('phonecatApp', ['ngRoute','phonecatControllers','phonecatFilters']);

html

    <dl>
        <dt>Infrared</dt>
        <dd>{{phone.connectivity.infrared | checkmark}}</dd>
        <dt>GPS</dt>
        <dd>{{phone.connectivity.gps | checkmark}}</dd>
    </dl>

## 10 - Event Handlers ##

クリックイベントで画像を置き換える処理
関数をControllerに用意し、HTML側で呼び出す

controller:

    $scope.setImage = function(imageUrl) {
      $scope.mainImageUrl = imageUrl;
    };
    
html

    <img ng-src="{{mainImageUrl}}" class="phone">
    ...
    <ul class="phone-thumbs">
      <li ng-repeat="img in phone.images">
        <img ng-src="{{img}}" ng-click="setImage(img)">
      </li>
    </ul>
    
html側でmainImageUrlをバインドしているので、setImageが呼ばれて変更されると
表示されている画像も変わる
