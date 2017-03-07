.. _`sphinx_soft`:

==================================================
sphinxのインストールメモ
==================================================

sphinxのインストール手順は以下となります。

pythonのインストール 
----------------------------

ここでは最新版のpython27をインストールした
インストール方法は `このURL <http://uxmilk.jp/37145>`_ に参考する。

インストールする時、customize installationを選定する |br|
※ インストール中path追加のチェックボックスをチェックすれば、環境設定が不要。

インストール後、バージョン確認：
 
 .. code-block:: python

      python -V

* ライブラリとかのインストール

1. `ez_setup.py <http://peak.telecommunity.com/dist/ez_setup.py>`_ をダウンロードして、コマンドラインから実行。

 .. code-block:: python
  
     python ez_setup.py

2. pip（パッケージマネージャ）のインストール

 .. code-block:: python
  
     easy_install pip

3. sphinxのインストール

 .. code-block:: python
  
     easy_install sphinx

以下のコマンドで、Sphinxのプロジェクトが作成できればインストールは成功している。

 .. code-block:: python
  
     sphinx-quickstart

実行すると、プロジェクトの詳細設定を聞かれるメッセージがでるが、
とりあえずEnterを押していく。途中、以下の３つの項目が入力必須項目。

 * プロジェクト名: sphinx
 * バージョン番号: 1.0
 * 著者の名前: ko
 

javasphinxのインストール
----------------------------

 .. code-block:: python
  
     pip install javasphinx

javasphinxをうまくインストールできない場合、エラーを確認して、必要なライブラリを追加する。

たとえば：lxmlの問題なら、lxmlのインストールが必要。
 
 .. code-block:: python
  
     pip install lxml
     
.. tip::
 lxmlのインストールエラーが出たら、次の方法でインストールする
 
 `ここから <http://www.lfd.uci.edu/~gohlke/pythonlibs/#lxml/>`_ lxmlのファイルを取得する
  
 例：lxml-3.7.3-cp27-cp27m-win_amd64.whl
  
 以下のコマンドを実行する(win7 64bit)

 .. code-block:: python
  
     pip install lxml-3.7.3-cp27-cp27m-win_amd64.whl


うまくインストールできるかをいかのコマンドで確認する

 .. code-block:: python
  
     pip freeze

問題がなければ、javasphinxを再インストールする

最後htmlファイルを生成する
----------------------------

 .. code-block:: python
  
     make html





.. |br| raw:: html

  <br />






