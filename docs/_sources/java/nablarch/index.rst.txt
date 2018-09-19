

==================================
メモ
==================================

1. Nablarchログ
---------------------------------------

ログ出力にはレベルがあり、レベルによって表示するエラーの量が変わります。

BeanExceptionはログレベル「DEBUG」として出力されているようなので、設定ファイル（log.properties）を書き換えてログレベルを変えれば出なくなると思います。

`【参考】7.1.6. ログレベルの定義 <https://nablarch.github.io/docs/LATEST/doc/application_framework/application_framework/libraries/log.html#log-log-level>`_ 

 
  
2. universalDaoの利用
------------------------------------------

検索条件が単項目・複数項目の場合、new Object[] {項目１, 項目2} ::

   UserDto dto = UniversalDao.findBySqlFile(UserDto.class, "SEARCH_USER_DETAIL", new Object[] {form.getUserId()});


検索条件がbeanの場合（form dto entityなど）、new Objectが不要 ::

   List<UserDto> searchResult = UniversalDao.page(searchCondition.getPageNumber()).per(20L).findAllBySqlFile(UserDto.class, "SEARCH_USER", searchCondition);  


3. List、Set、string配列の変更
----------------------------------------------------

リストをStringに変更 ::

   String [] samples = sampleList.toArray(new String[sampleList.size()]);


セットをStringに変更 ::

   String [] samples = sampleSet.toArray(new String[sampleSet.size()]);

セットからリストに変更 ::

   List<String> sampleList = new ArrayList<String>sampleSet;

リストからセットに変更 ::

   Set<String> sampleSet = new HashSet<String>sampleList;


4. <pre>タグの役割
--------------------------------------------------------

 * 連続する半角スペースはまとめて1つの半角スペースとして扱われる
 * タブ文字は半角スペース1つとして扱われる
 * 改行コードは半角スペース1つとして扱われる
 * テキストが表示領域の横幅に達すると、そこで折り返して表示される

HTMLで</pre>タグを使用すると、直後に1行空行が入るのですが、これを入らなくするために、スタイルシートでmarginを0に設定する

 .. code-block:: python
 
     <pre style="margin:0; padding:0">
     aaa
     bbb
     </pre>

`参考URL <https://dekiru.net/article/12888/>`_ 



5. spring のリストに対して精査方法
---------------------------------------------------------

入力フォームにリストを精査する時、こんな感じて作って、

 .. code-block:: python
 
     @Digits(integer = 9, fraction = 0)
     private List<Integer> userIdList;

で、実際に動かしてみると、エラーになっる ::
  
    javax.validation.UnexpectedTypeException: HV000030: No validator could be found for constraint 'javax.validation.constraints.Digits' validating type 'java.util.List'. Check configuration for 'userIdList'

対応方法として、以下の二つがある

1. メインフォームに対応するサブフォームを作って@Validと組み合わせる方法。

 .. code-block:: python
 
     @Valid
     private List<UserIdList> userIdList;
 
     public class UserIdList {
       @Digits(integer = 9, fraction = 0)
       private int userId;
     }

jsp側の書き方(nabalrchのタグを利用する場合)：

 .. code-block:: python
 
     <n:checkboxes name="form.userIdList" listName="userIds" elementLabelProperty="userName" elementValueProperty="userId" listFormat="span" elementLabelPattern="$LABEL$" />
     <c:forEach begin="0" end="${userIds.size()-1}" varStatus="status">
       <n:error name="form.userIdList[${status.index}].userId" errorCss="message-error" />
     </c:forEach>


2. Validを利用してリスト中に一つずつ精査する

 .. code-block:: python
 
     @Valid
     private List<@Digits(integer = 9, fraction = 0) Integer> userIdList;


jsp側の書き方：

 .. code-block:: python
 
     <form:checkboxes path="userIdList" items="${userIds}" itemLabel="userName" itemValue="userId"/>
     <form:errors path="userIdList" cssClass="message-error" element="div"/>



6. Springプロジェクトのソースコード修正後、コンパイルだけで反映するための依存関係
-------------------------------------------------------------------------------------------------------------

springプロジェクトに対して、サーバ起動のままソースコードの修正したら、サーバ再起動しないと変更点が反映できない。

サーバの再起動をせず、コンパイルだけで変更点を反映できるために、pomに以下の依存関係を追加する。

・Spring bootのバージョンが1.3以下の場合、springloadedを追加

 .. code-block:: python
 
     <plugin>		
       <groupId>org.springframework.boot</groupId>		
       <artifactId>spring-boot-maven-plugin</artifactId>		
       <dependencies>		
         <dependency>		
            <groupId>org.springframework</groupId>		
            <artifactId>springloaded</artifactId>		
            <version>1.2.8.RELEASE</version>		
         </dependency>		
       </dependencies>		
     </plugin>		

・Spring bootのバージョンが1.3以上の場合、spring-boot-devtoolsを追加

 .. code-block:: python
 
     <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-devtools</artifactId>
     </dependency>

※それでは、デバックができなく。もう一つのプラグインを紹介する：Jrebel（変更したファイルだけをliveReloadする） |br|
参考： https://www.zybuluo.com/weiys/note/1141626




7. 正規表現
----------------------------------------------

分かりやすく参考のURL |br|
https://java-reference.com/java_string_regex.html



8. doma-spring-bootのSQL例外変換
--------------------------------------------------------------

doma-spring-bootを利用すると、Doma2の例外クラス（JdbcException）をSpring Transactionの例外クラス（DataAccessException）に変換してくれます。

例えば、doma2の排他制御が行う時、基本的にOptimisticLockExceptionがスローされますが、
doma-spring-bootを利用される場合、実際にOptimisticLockingFailureExceptionがスローされる

詳細は以下のURLを参考 |br|
https://int128.hatenablog.com/entry/2017/01/07/020030




9. String.isEmpty()とStringUtils.isEmplty()の区別
------------------------------------------------------------------

StringのisEmpty()は対象変数のlength()が0（つまり空文字の場合）trueを返す。|br|
StringUtilsのisEmpty()は対象変数がnullまだは空文字の場合trueを返す

.. code-block:: java
 
     String str1 = null;
     String str2 = " ";
     
     str1.isEmpty()  ⇒ NullPointerExceptinが発生
     str2.isEmpty()  ⇒ true
     
     StringUtils.isEmpty(str1)  ⇒ true
     StringUtils.isEmpty(str1)  ⇒ true



10. Bean Validationのメモ
------------------------------------------------------------------

Bean Validation （JSR-303）は、JavaBeans のプロパティが取り得る値や条件を、精査する仕組み。Java EE6 から追加され、Java EE7 でのバージョンは1.1である。|br|
Bean Validationの標準アノテーションのパッケージはjavax.validation.*

Hibernate ValidatorはBean Validationで定義されたアノテーションに加え、独自の検証用アノテーションを提供している。|br|
Hibernate Validatorの代表的なアノテーションのパッケージはorg.hibernate.validator.constraints.*

Spring は、Java標準であるBean Validationをサポートしている。 単項目チェックには、このBean Validationを利用する。 
相関項目チェックの場合は、Bean ValidationまたはSpringが提供しているorg.springframework.validation.Validatorインタフェースを利用する


Nablarchでは、2種類のバリデーション機能を提供されている。|br|
* `Java EE7のBean Validation(JSR349)に準拠したバリデーション機能 <https://nablarch.github.io/docs/LATEST/doc/application_framework/application_framework/libraries/validation/bean_validation.html>`_  |br|
* `Nablarch独自のバリデーション機能 (Nablarch Validation) <https://nablarch.github.io/docs/LATEST/doc/application_framework/application_framework/libraries/validation/nablarch_validation.html>`_ 


参考URL: |br|
`Nablarchの入力チェック <https://nablarch.github.io/docs/LATEST/doc/application_framework/application_framework/libraries/validation.html>`_   |br|
`Springの入力チェック <http://terasolunaorg.github.io/guideline/5.4.1.RELEASE/ja/ArchitectureInDetail/WebApplicationDetail/Validation.html>`_ 


 .. tip::
  @Validatedは、Bean Validation標準ではなく、Springの独自アノテーションである。 
  Bean Validation標準のjavax.validation.Validアノテーションも使用できるが、
  @Validatedは@Validに比べて、 バリデーションのグループ(順序関係)を指定できる点で優れているため、@Validatedを使用することを推奨する。


11. セロ埋め、半角スペース埋める方法
---------------------------------------------------------------------------

    .. list-table:: 記述例
     :header-rows: 1
     :class: white-space-normal
     :widths: 16,32,50

     * - 用途
       - 記述例
       - 備考

     * - 文字列の先頭を空白埋めする
       - String.format("%6s", "abc")
       - 指定文字列を最大6桁まで文字列の左側に空文字を追加します。

     * - 文字列の後ろへ空白埋めする
       - String.format("%-6s", "abc")	
       - 指定文字列を最大6桁まで文字列の右側に空文字を追加します。

     * - 数字の先頭を０埋めする
       - String.format("%06d", 123)
       - 指定数字を最大6桁まで文字列の左側にゼロパディングします。

     * - 数字を3桁ごとにカンマ区切りする
       - String.format("%,d", 123456789)	
       - 指定数字を3桁毎にカンマ区切りします。






     
.. |br| raw:: html

  <br />

