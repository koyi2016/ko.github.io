.. _`github`:

==================================================
githubの利用メモ
==================================================


github Pagesを使ってドキュメントを公開方法
--------------------------------------------------------

github Pagesを使えば、個人や組織のウェブサイト、リポジトリのウェブサイトを作ることができます。

参考URL:

 http://sphinx-users.jp/cookbook/hosting/ |br|
 http://qiita.com/key-amb/items/4f799fed51734987f3c5 |br|
 http://qiita.com/syui/items/c429277ad4d357032d5e |br|
 https://github.com/nablarch/nablarch.github.io


必要なもの

 * githubのアカウント
 * sample用リポジトリ
 * gitまだはsourceTree


* 個人や組織のウェブサイトの公開手順

 1. github上ユーザ名.github.ioという名前のリポジトリを作成する、ローカルにタウンロード |br|
    (ここのユーザ名は個人のアカウント名、もしくは組織名です)。

 2. Sphinxでビルドしたsampleリポジトリ中のファイルをユーザ名.github.io/docsにコピーする。

 3. .nojekyllという空のファイルをユーザ名.github.ioの配下に作成する。
 
 4. masterブランチにpushします。
 
 5. http://アカウント名.github.io/docsにアクセスすると、HTMLドキュメントが見られる。
 
 サンプル例： https://koyi2016.github.io/docs/  |br|
 ソース： https://github.com/koyi2016/koyi2016.github.io

 .. tip::
   gitHub Pages で使われている Jekyll の仕様で _static/ 配下の画像やCSSが読み込むために、.nojekyll というファイルを配置しておきました。

 .. important::
  何で以下のURLでアクセス不可、その理由は？ 
  
  ・https://koyi2016.github.io
  
  ※nablarchでは https://nablarch.github.io/ でアクセスできる







.. |br| raw:: html

  <br />






