---
title: 'Objective-CのLintツールについて &#8211; xctoolとOCLintの連携方法'
author: azu
layout: post
permalink: /2013/0616/res3315/
dsq_thread_id:
  - 1405379392
categories:
  - iOS
tags:
  - iOS
  - Tool
---
Xcodeプロジェクトのビルドツールである[xctool][1]とC,C++,Objective-CのLintツールである[OCLint][2]を簡単に連携する方法について。

*   [OCLint &#8211; 0.7dev Documentation &#8211; Using OCLint with xctool][3]

に書いてあることなので、こちらを読むのが楽だと思います。

## [xctool][1]のインストール

homebrewでインストールするのがお手軽です

<div class="highlight">
  <pre>brew install xctool --HEAD
</pre>
</div>

## [OCLint][2]のインストール

*   [OCLint &#8211; Downloads][4]

OCLint 0.7はまだリリースされてないのでビルドする必要がありますが、面倒なので今回は0.6のバイナリをダウンロードしてパスを通します。

*   [OCLint &#8211; 0.7dev Documentation &#8211; Installation][5]

## 連携方法

OCLintはOCLint単体でLintもできますが、xctoolの[Reporters][6]にはOCLintに使える `json-compilation-database` というフォーマットが用意されます。

> xctool -> json-compilation-database -> OCLintでjson-compilation-databaseを読み込む 

という感じの流れです。

    xctool -reporter json-compilation-database:compile_commands.json test
    

というように`-reporter json-compilation-database`を指定してテストを動かすと、`compile_commands.json`ファイルを生成してくれます。

このファイルはビルドコマンドやファイル等がまとまってるだけで、これをOCLintに読み込ませてLint結果を取得する`oclint-json-compilation-database` というコマンドが用意されています。(OCLintに)

シェルスクリプトにまとめると以下のような感じです。

    #!/bin/sh
    
    OCLINT_HOME=~/local/oclint/bin
    export PATH=$OCLINT_HOME/bin:$PATH
    xctool -reporter json-compilation-database:compile_commands.json clean
    xctool -reporter json-compilation-database:compile_commands.json test
    # -i is include , -e is exclude
    oclint-json-compilation-database -i Lib/ -e Tests/ | sed 's/(.*.m{1,2}:[0-9]*:[0-9]*:)/1 warning:/'
    



## 何が嬉しいの?

*   よくわかりません

上記のスクリプトは [OCLint &#8211; 0.7dev Documentation &#8211; Using OCLint in Xcode][7] に書かれているものを大体そのままつかったものです。

`warning:` に置換してるのをみてピンとくる人もいるかも知れませんが、これをXcode上で実行すると  
OCLintのwarningをXcodeのエディタ上に表示することができます。

<img src="http://efcl.info/wp-content/uploads/2013/06/oclint_on_xcode.png" alt="NewImage" title="oclint_on_xcode.png" border="0" width="600" height="183" />

やり方については[OCLint &#8211; 0.7dev Documentation &#8211; Using OCLint in Xcode][7]を読んで下さい。

OCLintは自体はまだ分かりにくく、使いにくい感じのするツールですが、  
[Documentation][8] を見ると、他のツールとの連携や[Customizing Rules][9]、[Customizing Reports][10]など柔軟に出来そうな気がします。

*   [頑張ってOCLintを使ってみた結果 &#8211; blog.ishkawa.org][11]

現在(0.6)はエラー内容が分かりにくく、メトリクスな感じが強いのであんまり気軽に使えない感じがしてますが、  
[OCLint &#8211; 0.7dev Documentation &#8211; Rule Index][12] を見ると0.7では[Literal][13]に対するLintや[BrokenNilCheck][14]等、現実的にチェックしたほうがよさそうなものが色々追加されています。

Xcodeにも文法のチェックはありますが見逃しなども多いです。  
また、[AppCode][15] には同じような静的な文法チェックが結構充実していますがIDEに結合しているので、[OCLint][2]のように一つのツールとしてこのような機能があるのは色々と便利です。

JavaScriptではJSLint/JSHint/gjslint/JSONLint/WebStormのLint等、Lint系のツールは多いです。

これらのツールは[JSLint][16]のように強制力が強い(エラーがガンガン出るようなもの)より、[JSHint][17]のように明らかに悪いパターンの指摘や柔軟な設定ができるようになると一気に使われるようになった気がします。

また、[JSLint Error Explanations &#8211; Making Your Feelings Better][18]のような表示される警告についても納得できるような解説等がでてくると、このようなツールが使われるのが当たり前になってくると思うので(特に動的型付け言語とかこういうの合ったほうがいいはず)、OCLintはツール間の連携も意識されてるみたいなので今後に期待しています。

最近は開発も活発で、0.7もそろそろ出るはずなのでチェックしておくといいかもしれないですね(0.8ブランチもあります)

*   [oclint/oclint · GitHub][19]

## おまけ

*   OCLintはLinuxでも動く

[System Requirements][20] を見ると分かるようにLLVMベースなので、Linuxなどでも静的解析が行えます。

*   [Clang Static Analyzer][21]

XcodeのAnalyzeのような感じのを単独で使えるClang Static Analyzeというアプリもあります。  
(こちらはMacのみです)

 [1]: https://github.com/facebook/xctool "facebook/xctool · GitHub"
 [2]: http://oclint.org/ "OCLint, A static source code analysis tool to improve quality and reduce defects for C, C++ and Objective-C"
 [3]: http://docs.oclint.org/en/dev/guide/xctool.html "OCLint - 0.7dev Documentation - Using OCLint with xctool"
 [4]: http://oclint.org/downloads.html "OCLint - Downloads"
 [5]: http://docs.oclint.org/en/dev/intro/installation.html#option-1-directly-add-to-path "OCLint - 0.7dev Documentation - Installation"
 [6]: https://github.com/facebook/xctool "Reporters"
 [7]: http://docs.oclint.org/en/dev/guide/xcode.html "OCLint - 0.7dev Documentation - Using OCLint in Xcode"
 [8]: http://docs.oclint.org/en/dev/index.html "Documentation"
 [9]: http://docs.oclint.org/en/dev/customizing/rules.html "Customizing Rules"
 [10]: http://docs.oclint.org/en/dev/customizing/reports.html "Customizing Reports"
 [11]: http://blog.ishkawa.org/blog/2013/06/09/oclint/ "頑張ってOCLintを使ってみた結果 - blog.ishkawa.org"
 [12]: http://docs.oclint.org/en/dev/rules/index.html "OCLint - 0.7dev Documentation - Rule Index"
 [13]: http://docs.oclint.org/en/dev/rules/migration.html "Literal"
 [14]: http://docs.oclint.org/en/dev/rules/basic.html#brokennilcheck "BrokenNilCheck"
 [15]: http://www.jetbrains.com/objc/ "AppCode"
 [16]: http://www.jslint.com/ "JSLint"
 [17]: http://www.jshint.com/ "JSHint"
 [18]: http://jslinterrors.com/ "JSLint Error Explanations - Making Your Feelings Better"
 [19]: https://github.com/oclint/oclint "oclint/oclint · GitHub"
 [20]: http://docs.oclint.org/en/dev/devel/requirements.html?highlight=linux "System Requirements"
 [21]: http://clang-analyzer.llvm.org/ "Clang Static Analyzer"