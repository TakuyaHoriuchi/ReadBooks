## scala 入門
d3scala
@takezoen
@gakuzzzz 16/10/5
いわまつさん
TDKR

# refference
Scalaスケーラブルプログラミング
Dwangoの研修資料
Scala99 : 基本文法問題[1-28osusume
Scala逆引きレシピ

# TOSE
dockTyping

# Contents
Scalaは学ぶほどいける。
関数型プログラミングに寄せない使い方もある。

var, mutable, return, null, exception
Scalaではval再代入不可能なもので実装しやすくなる。

mutable使いがちなケース
メソッドの中でなら使っても良い

ScalaのReturnはちょっと特殊
returnの書き方次第では例外で実装されることがあるされる恐れもある。
returnもOK→Throwableでキャッチしなければ良い

nullは使わない
非Null３原則
Optional・switchで判定。
val user = findUser(id)
user match {
    case None =>
    case SOme(user) =>
}
NullチェックではなくメソッドのSignitureで判断出来る

例外
関数型プログラミングではあまり良くない
Either[]という方で処理
Right,Leftで返す
result match
case Right(user)
case Left(e)
どこで例外が発生するか分からない
Eitherの戻り値なのに

For内包表記が必要だったりする。
呼び出し元でハンドリングするときにはEither使って良い
そうでない場合は例外で良いのでは。

Better Jacaなら　Kotlinなどの選択肢もあり。
関数型プログラミングを積極的に取り入れるべき。

次回予告：
教養としてのモナド



新卒一年目でトークしている。

コレクション操作をする。
コレクション操作→List操作？
ひしだまさんのサイトを参考に便器
コレクション操作を作る
scala.collection.immutable.List

MatchCase重要

Scalaの良いところ
方安全・関数型・〜〜

１０
・scalaコンパイルが遅い→sbtは常駐させる。
・REPLで変更部分をすぐ確認出来る。
・???　→　Scapsで調べるとわかる。

Scala 年収でググる。
サイバーではペアプロよくやってる。

# エラーハンドリング

-1,nullではなんのエラーかわからない→例外処理しよう
制御フローが２つ・Catchし忘れる。
正常系異常系をEitherで返す。

正確に処理したい例外をハンドリング






