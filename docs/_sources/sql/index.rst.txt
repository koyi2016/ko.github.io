


sql
==========

作成予定


1. oracleシステムユーザーがロックされた際の解除
---------------------------------------------------------------

自分設定されたシステムユーザーがロックされた際、解除方法は以下となる

* 別の管理者ユーザーとしてoracleにログイン
  
cmdでコマンドを開く、以下のコードを実行
  
※別の管理者がログインできないと、解除ができない。その時、oracleの再インストールしかないと考える。

 .. code-block:: python
 
     SQLPLUS /NOLOG
     connect sys/password as sysdba
 

* ロックされたユーザーの解除

この例のユーザーはTEST。

 .. code-block:: python
 
     alter user TEST account unlock;


* 自分設定されたユーザーのパスワード変更

 .. code-block:: python
 
     ALTER USER system IDENTIFIED BY oracle;




2. SQLで文字列を連結する場合、各DBによって仕様が異なる
----------------------------------------------------------------------------

    .. list-table:: 例
     :header-rows: 1
     :class: white-space-normal
     :widths: 16,50

     * - DBMS
       - SQL
    
     * - Access
       - 文字列１+ 文字列２

     * - SQLServer
       - 文字列１+ 文字列２

     * - Oracle
       - CONCAT(文字列1, 文字列2) |br| 
         文字列1││文字列2

     * - MySQL
       - CONCAT(文字列1, 文字列2, 文字列3)
     
     * - PostgreSQL
       - 文字列1││文字列2



3. NVL関数メモ
------------------------------------------------------
OracleではNULL値を別の値に変換するには、NVL関数を使用します。
SQL Serverの場合はISNULL関数を使用します。使い方はNVLとISNULLは同じです。

.. code-block:: python
 
     NVL(a, b)
     
aがNULL値でない場合はaを返し、aがNULL値の場合はbを返す。



4. Oracleの桁数の書き方
--------------------------------------------------------

* NUMBER 精度３８桁の浮動小数点型です。

* NUMBER(桁数) 桁数の整数型です。

例：NUMBER(10)の場合、10桁の整数を定義する

* NUMBER(合計桁数, 小数点以下の桁数)

例：NUMBER(4, 2)の場合、整数部は2桁、小数部は2桁




     
.. |br| raw:: html

  <br />

