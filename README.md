底辺ライブラリ(Teihen Library)
==============================

これは何?
---------

競技プログラミングで使ってるライブラリ(Java)です.

底辺でもコピペして使える, CI環境のあるライブラリを目指してます.

このライブラリの特徴
--------------------

### HTML形式(library.html)

-   目次(サイドバー)
    -   ページ内リンクが効く
    -   レスポンシブル対応(隠れるだけ)
    -   スクロールに追随する
-   シンタックスハイライト対応
    -   コードは4スペースのインデントに
-   リンク
    -   ページ内リンクで移動
    -   ページ外リンクは別窓
-   単独で配置可能(オフラインも)
    -   HTMLファイルだけしか置けなくてもOK. (Dropboxとか)

### PDF形式(library.pdf)

-   ページ内リンク対応
    -   リンク先のページ番号も表示
-   シンタックスハイライト対応
    -   listingsなのでしょぼい

### Markdown形式(library.md)

-   (Githubで)Previewできる

このライブラリの構成
--------------------

とりあえず木構造で書くと, このような感じになってます.

``` shell
root
└─teihen_library (このリポリトジはココ!)
   │  index.html    (github-pages用. 基本的にlibrary.htmlと同じ)
   │  library.html  (ライブラリのHTML出力結果. HTML単体で持ち運び可能)
   │  library.md    (ライブラリのgithub-markdown出力結果.　githubで見れる)
   │  library.pdf   (ライブラリのpdf出力結果. ページ内リンクもばっちり)
   │  README.md     (この説明文)
   │
   ├─2DimIntGeometry
   ├─...(それぞれ, セクションごとのgithub-markdown)
   └─Template
```

このライブラリのビルド方法
--------------------------

そんなものは無い. (このリポリトジでは管理してません)

実際には, 以下のような構成になっていて, このリポリトジでは一番上だけ入れている.<br> 下の部分が無いとビルド出来ないよ!

``` shell
root
├─teihen_library (このリポリトジはココ!)
│  │  index.html   (github-pages用. 基本的にlibrary.htmlと同じ)
│  │  library.html (ライブラリのHTML出力結果. HTML単体で持ち運び可能)
│  │  library.md   (ライブラリのgithub-markdown出力結果.　githubで見れる)
│  │  library.pdf  (ライブラリのpdf出力結果. ページ内リンクもばっちり)
│  │  README.md    (この説明文)
│  │  
│  ├─2DimIntGeometry
│  ├─...(それぞれ, セクションごとのgithub-markdown)
│  └─Template
│          
├─Library(コード以外の部分の管理. コードの貼り付け先)
│  │  ...(Pandoc に依存する物をここで管理. TeX, HTMLのテンプレとか)
│  │  
│  ├─2DimIntGeometry
│  ├─...(それぞれ, セクションごとのpandoc-markdown)
│  └─Template
│              
├─source(コードのCI環境の管理. コードの貼り付け元)
│  │  pom.xml (mavenで管理してます)
│  │  
│  └─src
│     ├─main
│     │  └─java
│     │      └─library
│     │          └─...(通した問題の管理)
│     │                          
│     └─test
│         └─java
│             └─library
│                 └─...(テスト用のコードの管理. )
│                      
└─Tools(埋め込んだりするためのツール)
```

参考にしました
--------------

-   [AlgoLib\_Pandoc](https://github.com/tomoki/AlgoLib_Pandoc) ※基本思想, Pandoc
-   [この tkDocs をどう作ったか](http://docs.tatsuya-koyama.com/dev-log/how-to-make-tkdocs/) ※思想, デザイン関連
-   今まで見た競技プログラミング用のライブラリ, ソースコード
