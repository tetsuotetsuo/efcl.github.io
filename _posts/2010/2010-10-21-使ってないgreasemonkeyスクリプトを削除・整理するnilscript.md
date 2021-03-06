---
title: 使ってないGreasemonkeyスクリプトを削除・整理するNILScript
author: azu
layout: post
permalink: /2010/1021/res2008/
SBM_count:
  - '00008<>1354689237<>4<>0<>1<>3<>0'
dsq_thread_id:
  - 300802770
categories:
  - NILScript
tags:
  - Firefox
  - Greasemonkey
  - NILScript
---
Greasemonkeyはとても便利ですが、使用してないけどアンインストールするのが面倒で使わないスクリプトが貯まっていったりします。使わないスクリプトが貯まると猿アイコンを右クリックしたときに画面いっぱいになったり、管理画面が見づらくなったりしてとても邪魔になります。  
そこで、今無効となっているスクリプトを適当なフォルダに移動して、Greasemonkeyスクリプトを整理する[NILScript][1]を書いてみました。  
(タイトルが削除とかなってますが、実際は移動させるだけ)

### 使い方

最初に**gm_scriptsをバックアップして下さい**(おかしな動作をして失敗しても大丈夫なように)  
Firefoxが起動してないときに実行して下さい。

*   ngスクリプト([remove\_noused\_Greasemonkey.ng][2])をダウンロード
*   ngスクリプトをエディタで開いて、 *var saveDirPath = &#8220;C:\path\to\dir\&#8221;;* 移動先のディレクトリパスを書き換える
*   ngスクリプトを[Firefoxのプロファイルフォルダ][3]にある**gm_scripts**フォルダ内に置きます。
*   Firefoxが起動してるならばFirefoxを終了しましょう
*   必ず**gm_scriptsをバックアップしてから**ngスクリプトを実行しましょう

ngスクリプトの実行方法は[NILScriptの使い方と書き方][4]やreadme.txtを見ると良いでしょう。  
一応ログっぽいのも表示してるのでダブルクリック実行が手軽でしょう。  
完了すると&#8221;無効になっているスクリプト m/n を移動しました&#8221;というメッセージが出て終わりです。  
[<img class="alignnone size-medium wp-image-2009" title="2f8a54482fcfe8a7e5952a8ef2b2d7f8" src="http://efcl.info/wp-content/uploads/2010/10/2f8a54482fcfe8a7e5952a8ef2b2d7f8-300x232.png" alt="" width="300" height="232" />][5]

猿アイコンのコンテキストメニューがスッキリして気持ち軽くなりました(実際に動作が軽くなるかは知りません)  
各Greasemonkeyがpref.jsに保存していた情報は消えてないので、完璧に綺麗になったわけではありません。  
戻すときはバックアップしていたものを上書きすればもどせると思います。

**utilityTools/Greasemonkey at master from azu/NILScript &#8211; GitHub**
:   [https://github.com/azu/NILScript/tree/master/utilityTools/Greasemonkey][6]

**NILScript**
:   [http://lukewarm.s151.xrea.com/nilscript.html][7]

<div id="_mcePaste" style="position: absolute; left: -10000px; top: 0px; width: 1px; height: 1px; overflow: hidden;">
  var saveDirPath = &#8220;C:\Users\azu\Web\Greasemonkeys\&#8221;;// 移動先のディレクトリパス
</div>

 [1]: http://lukewarm.s151.xrea.com/nilscript.html
 [2]: https://github.com/azu/NILScript/raw/master/utilityTools/Greasemonkey/remove_noused_Greasemonkey.ng
 [3]: http://support.mozilla.com/ja/kb/%E3%83%97%E3%83%AD%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB
 [4]: http://efcl.info/2010/0816/res1888/
 [5]: http://efcl.info/wp-content/uploads/2010/10/2f8a54482fcfe8a7e5952a8ef2b2d7f8.png
 [6]: https://github.com/azu/NILScript/tree/master/utilityTools/Greasemonkey "utilityTools/Greasemonkey at master from azu/NILScript - GitHub"
 [7]: http://lukewarm.s151.xrea.com/nilscript.html "NILScript"