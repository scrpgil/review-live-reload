# Re:VIEW Live Reload

Re:VIEWファイルを編集すると同時にブラウザでライブリロードするサンプル。  
同梱のCSSによって見開きの本のような見た目でプレビューすることができます。  

## Demo
![screenshot](https://raw.githubusercontent.com/yoshiko-sandbox/images/master/review-live-reload/demo.png)


## Setup
```
git clone https://github.com/yoshiko-pg/review-live-reload.git
cd review-live-reload
bundle install --binstubs=bin --path .bundle
```

別途ブラウザへguard-livereload用の拡張機能をインストール  
http://feedback.livereload.com/knowledgebase/articles/86242-how-do-i-install-and-use-the-browser-extensions  

Chromeの場合、インストール後に拡張機能の設定([chrome://extensions/](chrome://extensions/))でLiveReloadの「ファイルのURLへのアクセスを許可する」にチェックを入れないと動作しませんでしたので忘れずに。  


## Run
```
bundle exec rake server
bundle exec guard
```

http://localhost:5000/ch01.html を表示  
Browser Extensionを有効化(Chromeの場合、拡張機能ボタンを押して中央の四角が黒くなればOK)  

上記の状態でsrc/\*.re もしくは src/main.cssを修正すると変更がリアルタイムにブラウザへ反映されます。  
プレビュー表示は右側に続いていくので下ではなく右にスクロールしてください。  


## Attention
本のような見た目を表現するためにCSSにcolumn-countというスタイルを指定していますが、これがあるとePub出力する際にコンテンツが途中で途切れてしまいます。  
ePub出力の際はbodyについているcolumn関連のスタイルをコメントアウトしてください。


## Thanks
このリポジトリは以下のリポジトリの内容を合体させて手を加えたものです。  

#### src/以下
https://github.com/takahashim/review-sample-book  

#### Gemfile, Guardfile, Rakefile  
https://github.com/xoyip/review-livereload  
