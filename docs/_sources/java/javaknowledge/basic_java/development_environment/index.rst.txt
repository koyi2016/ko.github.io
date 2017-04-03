

==================================
第１章：Java実装環境と流れ
==================================


・ Javaプログラムの作成から実行まで
-----------------------------------

.. image:: ../images/jdk.png

.. tip::
  一つのソースファイル内に複数のクラス定義を行った場合、ソースファイル内の全てのクラス定義に基づいてクラスファイルが生成される。

  例：sample.javaの中、三つのクラスsample, test, passを定義した場合、コンパイル時、sample,test,passのclassファイルが生成される。

 .. image:: ../images/sampleJava.png

.. important::
 一つのJavaソースファイルでは複数のpublicクラスを定義することができないため、public修飾子を指定した場合、ソースファイル名とクラス名を同じにしなれけばならない。

Javac Test.javaを実行する時、もしソースコードの中に、日本語がある場合、エラーになりますので、以下のように実行が必要。

.. code-block:: python
   
   Javac -encoding UTF-8 Test.java

文字コードを指定するには「-encoding」オプションを使います。


・ Javaプログラム動作環境
---------------------------------

特徴：Javaで一つのプログラムを作成することで、どのコンピュータ上でも動作させることができます。

#. JVM（Java Virtual Machine）Java仮想マシンとは：バイトコードのJavaプログラムを解釈し実行するソフトウェア。
#. JRE（Java Runtime Environment）とは：Java実行環境。JVMおよびプログラムの実行に必要なライブラリがまとめられた。
#. JDK（Java Development Kit）とは：Java開発環境と言います。Javaでプログラムを作成する時必要です。


JVM、JREとJDKの範囲は以下の図で示します。

.. image:: ../images/jdkHani.png

.. important::
 JDKにはJREが含まれています。つまり、Java開発環境ではJDKのインストールとPath設定が必要です。

 参考URL:　http://www.task-notes.com/entry/20140810/1407599796



・ Javaプラットフォーム各エディションの特徴と説明
----------------------------------------------------

Javaプラットフォームは、Javaで記述されたプログラムの開発および実行を行うことのできるソフトウェア群の総称。

#. Java SE（バージョン5.0までは Java Platform, Standard Edition または J2SE）は基礎と一部機能を提供する。
#. Java Platform, Enterprise Edition (Java EE) は、Javaの企業用機能セット。Java SE の拡張機能の形で提供される。
#. Java Platform, Micro Edition (Java ME)は携帯電話、PDA、テレビのようなのリソースが制限されたデバイスにおけるJavaの小型セット。


.. tip::
 #. Java EEを利用するために、JavaSEが必要です。|br|
 #. Java EEはGUI関連のライブラリ（java.awtやjava.swing）以外にも、ネットワーク、スレッド、データベースアクセスなどのライブラリが用意されている


・ 注意点
------------------

Java開発する時、注意点をここでまとめます。

#. Javaでは大文字と小文字は区別される。　|br|
#. Javaプログラムはmainメソッドから実行する。　|br|
#. Javaのコメント注釈は「//」、「/* */」を使う。　|br|
#. 出力方法：改行の時　System.out.println()、改行しないの時　System.out.print()。　|br|
#. 特殊な文字の入力(エスケープシーケンス)　|br|
  
    .. list-table:: 例
     :header-rows: 1
     :class: white-space-normal
     :widths: 16,24

     * - 使用例
       - 意味
    
     * - ¥t
       - タブスペース

     * - ¥n
       - 改行

     * - ¥¥
       - ¥

     * - ¥"
       - "

#. Javaアプリケーションはmain()メソッドから実行する。(必ず一つ定義される) |br|
   
   定型句： 

    .. code-block:: python

         public static void main(String[] args)








     
.. |br| raw:: html

  <br />

