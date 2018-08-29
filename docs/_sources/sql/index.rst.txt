


sql
==========

作成予定


・oracleシステムユーザーがロックされた際の解除
---------------------------------------------------------------

自分設定されたシステムユーザーがロックされた際、解除方法は以下となる

１. 別の管理者ユーザーとしてoracleにログイン
  
cmdでコマンドを開く、以下のコードを実行
  
※別の管理者がログインできないと、解除ができない。その時、oracleの再インストールしかないと考える。

 .. code-block:: python
 
     SQLPLUS /NOLOG
     connect sys/password as sysdba
 

2. ロックされたユーザーの解除

この例のユーザーはTEST。

 .. code-block:: python
 
     alter user TEST account unlock;


3. 自分設定されたユーザーのパスワード変更

 .. code-block:: python
 
     ALTER USER system IDENTIFIED BY oracle;


     
.. |br| raw:: html

  <br />

