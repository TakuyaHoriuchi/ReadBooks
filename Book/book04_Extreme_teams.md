# 一部　Web概論
集中システム　分散システム
telnet　UNIXホストにリモート接続するためのソフト
FTP　ファイル交換ソフト
ハイパーテキスト・・・文字を送り合う
ハイパーメディア・・・動画なども扱う
RPC リモートサーバで実行しているプログラムをクライアントから呼び出せる。
ただ汎用的なオブジェクトを生成しようとした時に複雑な構想になってしまった。

リンクは単方向
１９９４にHTML　CSSなどの仕様を策定
REST　ネットワークシステムのアーキテクチャスタイル
WebのアーキテクチャはRESTでもありClientServerでもある。
クライアント・ステートレスサーバ　Ex：CookieなどはRESTからは離れたアーキ
Cashe・・・古いキャッシュ」で情報の信頼性を損なう恐れ

Code On demand…プログラムコードをサーバからDL、それをクライアントで実行するアーキスタイル➜JSなどがあてはまる
Demerit・・・プロトコルの可視性が低下

RESTとは６つを組み合わせたアーキスタイル
１クライアント・サーバ
２ステートレスサーバ
３キャッシュ
４統一IF　IF固定
５階層化システム　システムを階層に分離
６CodeOnDemand

でもサーバを介さずPeer同士で通信するP2PなどはRESTが向いていない。

アプリケーション状態・・・Bookmarkなどを開いているなどのアプリの状態示す
で状態遷移はハイパーメディアリンクで遷移する。

# ２部URI
URI・・・URIスキーム　ホスト名　パス
takuya:hoeiuchi・・・ゆーざi
8080    ポート　
?1=2&2=3 クエリパラメータ　
~ #n10 URIフラグメント・・・HTML内部のIDの場所
相対URI時はURIスキーム・ホスト名省略
<font color=purple size=4>・ベースURIを指定する方法(html, xml)</font>
➜htmlヘッダー内のBaseタグで記述、XMLならbase属性でいつでも付けられる

URIはASCIIのみ基本的に使える。ひらがなとかは%Encodingしないとだめ
あ➜UTF-8で９文字、％エンコードは、もととなるフォームの文字Encodingで解釈

URI・・・IEで２０３８Byte






<font size=4 color=green>Cool URIの例：
- cgi-binなど特定の技術によるものを除く
- .plなど言語が指定されている
- 大文字
- メソッド名なセッションIDを含めない。
-> リソースを表現する名詞であるよう表現

Ex:login form,login page -> login

URIを変更する時はなるべくRedirect
仕組みはHTTPサーバが用意。Apacheならmod_rewriteというModuleを使用

コンテントネゴシエーション：使用しているOSから言語を選別する方法。P60
これだと違う言語設定にするのがめんどい➜.jaとかで明示的なURIを設定する（プレのとき）

URIにマトリクス指定も可能。

URIの不透明さ（バレない仕組み）
Architecture of the World Wide Web.Vol1 2.5説


# 第三部　HTTP
TCP/IPの基礎ー写真参照

HTTPはReqRes型のプロトコル・帰るまで待つから同期型のプロトコルでもある。

HTMLのMIMEメディアタイプ(app/xhtml+xml)

res status+header+body
body can use binary data.
state lessは前の処理と疎結合になることがメリット。
でもTransaction管理したい時は向かない
GETではURIに含めていたクエリをPOSTではRequestBodyに入れられる
POSTとPUTの使い分け　➜　PUTはURIをクライアントが設定したいとき有効This is密結合
でもなるべくPOST
リソースが更新されてたらGETするというOPTIONも付けられる
POSTは安全でもべき等でもないのでブラウザバックなどで処理すると注文が２回発生するなどの問題がある。慎重にテストする必要あり。
べき等(何回やっても同じレスポンスが返ってくること)を維持する必要がある。
TOSE：POSTはリソースを作ってしまうものなのか、インスタンスみたいな？


StatusCode
1-- 処理中
2--　成功
3--　リダイレクト　ResメッセージのLocationヘッダを見て新しいリソースにアクセスする。
4--　Clientエラー
5--　サーバエラー
key 200 301 303 400 404 500
201 リソース作成成功
503　メンテ
404 などを200で返すと検索エンジンのロボットが正式なリソースであると勘違いし
インデックス処理を行う可能性あり

HTTPヘッダー
日時DateやExpires
- Date：生成日時
- Expires：ResponsEのCashe期限
MINE MediaType　メッセージの表現種類を決める。
- application/xhtml+xml　タイプ/サブタイプ
- type -> text,image,audio,video,multipart,message,model,example
- サブタイプは色々
- charsetParamはデフォルトだと文字化けを引き起こす恐れ。
- encodingでUTF-8とかにするならちゃんとヘッダにCharsetParamつける、またContentTypeはtextはあまり使わずApplication。
- Content-Language：ISO639、３１６６
- Accept：処理出来るメディア・タイプを決めるヘッダ
- qvalueを用いて優先度の記載が可能。非対応タイプなら406が返る。
- 文字版がAccept-Charset, Languageもある
- Transfer−Encoding: chunkedで最終的なさいずが分からずとも中身を少しずつ転送出来る。
- HTTP認証方式はBasic認証・Digest認証というものがある。
- WWWww-Authoenticate：でサポートしている認証を知ることが出来る。
- Authorization: Basic　user:passwordでOK
- ただそのままだと平文で流れるのでSSLやTLSを使ってHTTPS通信する必要がある。
- SSL/TLSによって　暗号化・認証・改ざん検知　の機能を賄う。
- Digest認証のメリデメ：
- パスが盗まれにくい、パスをサーバに預ける必要がない。
- Cashe用ヘッダ
- Pragma:no-cache　キャッシュ出来ない
- Expires：~~ キャッシュが新鮮さを保つ期限、最長でも一年を推奨。
- Cache-COntrol: no-cache , max-age:86400 (sec) including prag&expi
- If-Modified-Since: 18/1/1 13:00 それ以降更新してたら取得
TOSE:ETag

Keep-Aliveヘッダで接続し続ける設定が出来る。
Connection:closeで切断
Content-Disposition　ファイル名を指定する

# ４部　ハイパーMediaFormat

XMLで記述する際は特別文字は実態参照という機構を用いて入力。
２つの同じタグを区別したい場合は名前空間を活用する
<em>強調</em> <strong>sd</strong> <dfn>sdfghj</dfn> 
<code>asdfasd</code>　<samp>例</samp> <kbd>w</kbd>
<var>x=32</var>
<a href="http://www.google.com">aタグはリンク</a>
linkはWebページ毎の関係性を示す。relをnext prev indexなどのように指定する。
relでよく使われているのはstylesheet 外部cssを適用出来る。
上はGet。FORMならPOSTも遅れる。
画像はimg, それ以外はobjectタグを使用

Microformat
aタグのrel-license
TOSE:メタデータとは

AtomFormat
author,content,categoryなどいろいろなタグが使える

Json
Ajaxで使える。
ISO 8601Formatで日付表記オススメ
JSだとIE時の表記が変わってしまう。P236

基本的にはクロスドメイン通信は出来ない仕様にしている。
ただ、スクリプトタグで複数サイトからJSが読める。
JSONP・・・クロスドメイン通信するための手法


# 第五部　Webサービス設計
エラー検討　例
存在しないURL 404
パラメータNotSet 400
UnSupportedMethod 405

PUT MethodにはPartialUpdate機能がある。通常はバルクアップデート
POSTで複数リソースを更新する時はエラーが起きると一部成功などもありうる
WebDavを使えば一個一個のStatusCodeが見れる。　XMLではなく自分で定義したJSONでも可能。
Transactionもコンテンツ形式を書き換えて、Commit＝Trueにすることで可能
排他制御もWebDAVのLOCK機能を使う事で可能。
Lock時は423
IFヘッダを挿入することでLockTOけｎを指定出来る。
UNLOCK HTTP Methodを仕様してUNLOCKする。
UNLOCKヘッダを適用
LOCKについては編集出来ないデメリットが大きいので排他ロックより楽観的ロックを実装したほうが良い➜　ETag使用
４１２競合

リソース設計として主キーを１リソースとするのが良い。URIを
Tableはなるべくわけない。

# 感想
RESTの理解が難しい中わかりやすく書かれていて、HTTPプロトコルを一通り学ぶには
よい勉強になった。ヘッダで指定出来るOPTIONなどがまとめられていて、その部分は特に参考になった。
