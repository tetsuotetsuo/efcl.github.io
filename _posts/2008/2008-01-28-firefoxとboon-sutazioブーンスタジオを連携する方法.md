---
title: FirefoxとBOON SUTAZIO(ブーンスタジオ)を連携する方法
author: azu
layout: post
permalink: /2008/0128/res37/
SBM_count:
  - '00001<>1355420397<>0<>0<>1<>0<>0'
dsq_thread_id:
  - 300801298
categories:
  - Firefox
tags:
  - Firefox
  - アドオン
---
<p>FirefoxとBOON SUTAZIO(ブーンスタジオ)を連携させて、Firefoxの右メニュー<br />
(上のボタンにも)にBOON SUTAZIOでダウンロードさせる方法の紹介です。</p>
<p><a href="https://addons.mozilla.org/ja/firefox/addon/81/" class="no">Launchy</a>というアドオンを使い行います。</p>
<p><a href="http://mozilla.seesaa.net/article/2085037.html">電網探題 日本語Locale同梱版</a><br />
<a href="https://addons.mozilla.org/ja/firefox/addon/81/" class="no">Mozilla Add-ons &#8211; Launchy</a></p>
<p>バージョンは同じなので日本語版でもいいかと思います。<br />
インストールしてFirefoxを再起動したら、</p>
<p><a href="http://efcl.info/wp-content/uploads/2008/01/launchy.png" title="launchy.png"><img src="http://efcl.info/wp-content/uploads/2008/01/launchy.thumbnail.png" alt="launchy.png" /></a><br />
設定のアプリケーションの自動検出のチェックを外してください。(なんかうまくいかなかったのでそうした。)<br />
<a href="http://gemal.dk/mozilla/launchy-xmlfile.html">launchy.xml generator</a>で<a href="http://efcl.info/wp-content/uploads/2008/01/launchy.xml" title="launchy.xml">l</a>aunchy.xmlを作成します。(どんなアプリを起動するかの設定ファイル)<br />
起動用の名前、アプリの絶対パス、タイプはブラウザのままで<br />
The arguments of the application:は<strong><br />
url</strong><br />
と入れれば大丈夫です。<br />
そして出てきたコードをエディターかなんかに貼り付けて<a href="http://efcl.info/wp-content/uploads/2008/01/launchy.xml" title="launchy.xml">l</a>aunchy.xml という名前で保存します。<br />
(<strong>このときUTF-8の文字コードで保存してください</strong>)<br />
保存場所は<br />
C:Documents and Settings<span class="keyword">ユーザー</span>名Application Data<span class="keyword">Mozilla</span><span class="keyword">Firefox</span>Profilesランダム英数.defaultchrome<br />
におけば認識されます。</p>
<p>Firefoxを再起動させれば完了。<br />
ダウンロードしたページでlaunchyのメニューから開けばBOON-SUTAZIOが起動して自動でダウンロードを開始します。<a href="http://piro.sakura.ne.jp/xul/ctxextensions/"></a></p>
<p><a href="http://piro.sakura.ne.jp/xul/ctxextensions/">ContextMenu Extensions</a> を使いやる方法もありますが、こちらは多機能なので、<br />
これだけのために入れるのはもったいない気がするのでスルー。</p>
