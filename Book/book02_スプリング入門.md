
分散ミドルウェア・・・XML、CORBA
この本を呼んで、DI,AOPが何で設計をどう助けるのか、RDBアクセス方法
ベスト・プラクティス。-
agileより？

TOSE：Springのメリット・デメリットの整理


１．SpringとWebアプリケーションの概要

Spring情報：Pivotal者管理の元OSSとしてApacheライセンスV2.0のもと利用可能。
SSH：Struts,SpringFreamwork,Hibernateで構成するWebアプリケーション
➜現在はSpringMVCで構成することが多くなってきた。

前はBeanだったものがJavaConfigとAnnotationでできるようになった。

Spring系統の周辺プロジェクトも理解すべき
：https://pivotal.io/jp/oss, https://spring.io
SpringFreamwork:
DIxAOP, Spring MVC, Spring JDBC)
Cache, Security, Data, Batch, Boot
UNISYSもMaiaでSpringを使用している。

WWW仕組み
静的コンテンツ：
　クライアントマシン上のWebブラウザから
　ネットワークの先にあるWebサーバから要求したHTMLを読み込んで表示する。
　HTML - CGI


動的コンテンツ：
　Webサーバからアプリケーションサーバに処理要求を行い、たいていはRDBから
　データを読み取ったり、加工しながらその処理結果をWebさーばで受取Webブラウザに表示する。
　現在ではブラウザ上でAjaxが動きリッチな画面を実現。
　JSP - EJB - Springで実装

CGI：HTTPReqによって起動するプログラム　➜同じ要求で異なるレスポンスを返せるようになった。
問題：HTTPreq呼び出しごとに起動する。セッション管理が出来ない　➜　処理要求が多いとき、PF劣化・ドランザクション管理が難しいデメリット
➜解決したのがJSP＋Servletの構造。画面生成ロジックとビジネスロジックの分離が出来るようになった。

↓
EJB：分散処理の融合コンポーネント➜BackEnd処理担当。ローカルアクセスできないのが問題。
    　その隙にSpring＋Hibernate登場

TOSE：EJB

J2EE：登場➜重い
　➜DIｘAOPコンテナの考案：POJPを利用してオブジェクト間の依存関係を解決。
    DBアクセスもPOJOにORMを適用することで可能。EJBと違い、POJOを利用しているためテストが容易

エンジニアの心構えで
「リファレンス、仕様書を元にCoding出来るのは半人前、
アプリケーションアーキテクチャまで理解して一人前」
という言葉が強く刺さった。

アプリアーキは目標を元に設計。
１．ユーザ向け目標：機能要求・レスポンスなどの非機能要求
２．保守向け目標　：開発期間・システムの変更に対する柔軟性・テスト容易度　など

Tier：物理層, View　Controller　Dataアクセス
Layer：論理層
MVC形態を取る時は、お互いの関係が相互依存ではなく片方向の依存

Presen層
TOSE：UMLの線の意味
凹型レイヤの特徴：DA層で扱うDBがRDB➜NoSQLになったとしてもBL層に影響が無い
　　　　　　　　　➜レイヤ間にInterfaceを適用している。
TOSE：IFの概念

QUESTION：P21　ゼロからコントローラを自作するのは無駄　とはどういう作業か？
TOSE：AJAX　
Ajax　は非同期通信
UIの多様化によって入力チェックなどの処理は、JSPとServletで実装しているものに比べ、
非同期通信を含むWebAPなどだと、場合によってはクライアント層を作るなどしてPresentation層付近で行う実装も見えてきた。
最適な構成はあーきによる。

BL層パターン
・トランザクションスクリプト
DB操作のみなら全部サービスクラスに含める。
・ドメインモデル
複雑な操作の時にトラスクを使うとBLが複雑になる。Springはこれにはあまり役に立たない。
　➜挙動がDIｘAOPコンテナではなく、DA層にいそんするから。

トランザクションはACID特性を守る必要がある。
A：原子性（トランザクション内の全ての処理が行われたか否かに当てはまる➜コミットとROLLBACK）
C：データ一貫性
I：トランザの独立性
D：データの永続性
Aを守るために、Compositeメソッドを作ってやる。
そのコンポジット内でFreWoを使わずSourceで書くのを明示的トランザクション・FreWo使うのを宣言的Trという

DA層
Object-RelationalTable間のマッピングをORマッピングという。
DBアクセスFreWoを使うのが一般的
O➜R：Entityを元にTable作成。R➜Oはオブジェクト生成。
ORはHibernate。ROはSpring JDBC（SQL利用）

Springはレイヤとは独立したものと認識しておく
TOSE:マイクロサービスアーキテクチャ　とは（分け方P40）

２
DIのメリットはNewが消えるだけ　→　POJOをインスタンス化しないため
DIはRDBから持ってきてインスタンス化する作業には向かない。
固定の作業を行うものなら得意
→コントローラtoサービス、サービスtoDAOは得意
 サービスとドメイン、DAOとドメインは苦手













感想：PerfectJava１章レベルの知見の読破後に読むと良いかも。
なぜSpringが必要なのかに基いて書かれているため、言ってる意味が分かりやすい。




エンジニアの心構えP13として
「リファレンス、仕様書を元にCoding出来るのは半人前、
アプリケーションアーキテクチャまで理解して一人前」
という言葉が強く刺さった。










