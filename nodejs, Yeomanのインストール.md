## nodejs, Yeomanのインストール

### nodeJs

0.12.2インストール
最新の0.12など入れているとKarmaなどの対応バージョンが合わずに怒られる?
好きなバージョンに変更できるnodebrewをインストールしてバージョン変更


### npm

nodeJsのパッケージマネージャ
アプデ方法

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
