## nodejs, Yeomanのインストール

### nodeJs

最新の0.12など入れているとKarmaなどの対応バージョンが合わずに怒られる
好きなバージョンに変更できるnodebrewをインストールしてバージョン変更

node.jsのversionを管理するためにnodebrewを利用する
http://qiita.com/sinmetal/items/154e81823f386279b33c

0.10系なら大丈夫らしいので現時点で最終である0.10.38をインストール

### npm

nodeJsのパッケージマネージャ
0.10.38インストール時には1.4になっている
yeomanインストール時に2.1.0以上対応と注意がでるので事前にアップデートする

    npm update -g npm

### yeoman

    npm install -g yo bower grunt-cli gulp

nodeJSやnpmのバージョンがあっていればすんなり入る

### gruntでprotractorの実行をするためにrunnnerが必要

    npm install -g grunt-protractor-runner
  
### IDE

WebStormの体験版を使用する。Gruntと連携してユニットテストやデバッグなどやりやすくなる
https://www.jetbrains.com/webstorm/

nodebrewを入れている場合nodebrewの環境変数を通さないと連携できない
