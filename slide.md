#### [CombNaf x 学生LT] 第12回 学生エンジニアLT大会！！！
- - -
## Ruboty で
## Discord-Bot をつくろう

---

### 自己紹介
- - -

<div class="prof">
  <img src="https://pbs.twimg.com/profile_images/882685064659611648/hoPsIEDh_400x400.jpg" style="width:10%;"/>
</div>
* なまえ  : おしょー（学生ではない）
* Twitter : [@pink_bangbi](https://twitter.com/pink_bangbi)
* github  : [osyo-manga](https://github.com/osyo-manga)
* ブログ  : [Secret Garden(Instrumental)](http://secret-garden.hatenablog.com)
* Rails エンジニア、日々 Rails と戦っている
* たまに Ruby のパッチを書いたり
* エディタは Vim

---

### 今日話すこと
- - -

## Ruboty で
## Discord-Bot を動かそう！！

---

## そもそも Discord とは

---

#### discord とは
- - -

* ゲーマー向けのボイスチャットを行うコミュニケーションツール    <!-- .element: class="fragment" -->
  * チャットツールでもある
* Slack と似ているが招待制でなかったり細かいところで方針が異なる    <!-- .element: class="fragment" -->
* 最近だと 学生LT が Slack から Discord に移行したことで有名    <!-- .element: class="fragment" -->
* Discord 上で Bot を動かそう！というのが目的    <!-- .element: class="fragment" -->

---

## Ruboty ってなに…？

---

#### Ruboty とは
- - -

* Ruby 製のチャットフレームワーク    <!-- .element: class="fragment" -->
* Ruby で拡張したり Bot をつくることができる    <!-- .element: class="fragment" -->
* 特徴として以下のように実装が分かれてる    <!-- .element: class="fragment" -->
  * 各種 SNS とハンドラを接続する部分（アダプタ）    <!-- .element: class="fragment" -->
  * 発言に対して処理を行う部分（ハンドラ）    <!-- .element: class="fragment" -->
* 既存のハンドラとアダプタを組み合わせるだけならコードを書かずに Bot をつくることが出来る    <!-- .element: class="fragment" -->

>>>

#### アダプタ
- - -

各種チャットサービスと Ruby を接続する部分

* [ruboty-discord](https://github.com/ykzts/ruboty-discord)
* [ruboty-slack](https://github.com/r7kamura/ruboty-slack)
* [ruboty-twitter](https://github.com/r7kamura/ruboty-twitter)
* [ruboty-line](https://github.com/osyo-manga/gem-ruboty-line)
* [ruboty-chatwork](https://github.com/mhag/ruboty-chatwork)

>>>

#### ハンドラ
- - -

* [ruboty-youtube](https://github.com/kaihar4-archive/ruboty-youtube)
  * Youtube で検索
* [ruboty-github](https://github.com/r7kamura/ruboty-github)
  * github-issues を立てたり
* [ruboty-vimhelp](https://github.com/osyo-manga/gem-ruboty-vimhelp)
  * Vim の :help したり
* [ruboty-tenki](https://github.com/osyo-manga/gem-ruboty-tenki)
  * 今日のお天気を返したり
* etc...

---

## と、いうことで Ruboty で
## Discord-Bot を動かしてみよう！！

---

#### 用意するもの
- - -

* Discord のアカウント    <!-- .element: class="fragment" -->
* Discord の Bot アカウント    <!-- .element: class="fragment" -->
  * Bot が動かせる Discord のサーバ    <!-- .element: class="fragment" -->
* Ruby    <!-- .element: class="fragment" -->
  * bundler
* お好きなエディタ    <!-- .element: class="fragment" -->

---

## デモ

---

## Ruboty をインストールして動かしてみる

>>>

#### Gemfile ファイルを用意する

```ruby
# Gemfile
source "https://rubygems.org"

# Ruboty 本体
gem "ruboty"
```

>>>

#### Ruboty をインストール

```shell
# Gemfile ファイルと同じディレクトリで実行
$ bundle install
# CLI 上で Ruboty を動かす！
# 起動後に ruboty help や ruboty ping で発言に対して動作する
$ bundle exec ruboty
```

---

## Ruboty にハンドラを追加してみる

>>>

#### Gemfile にハンドラを追加する

```ruby
source "https://rubygems.org"

# Ruboty 本体
gem "ruboty"

# ハンドラを追加
gem "ruboty-tanzaku", github: "osyo-manga/gem-ruboty-tanzaku"
gem "ruboty-vimhelp"
```

>>>

#### Ruboty を動かす

```shell
# Gemfile を書き換えたらもう1回 install
$ bundle install
# Ruboty を起動
# ruboty tanzaku hoge
# や
# ruboty :help i
# するとわかりがある
$ bundle exec ruboty
```

---

## Ruboty に自分でハンドラを定義してみる

>>>

#### Ruby ファイルを用意

```ruby
# app.rb
require 'rubygems'
require 'bundler'
Bundler.require

class Ruboty::Handlers::MyBot < Ruboty::Handlers::Base
	pn(
		/pong/,
		name: :pong,
		description: "pong"
	)
	def pong message
		message.reply("ping")
	end
end
```

>>>

#### app.rb を読み込んで Ruboty を動かす

```shell
# --load {file} でそのファイルを読み込む
$ bundle exec ruboty --load app.rb
```

---

## Discord で動かす！

>>>

#### Gemfile にアダプタを追加する

```ruby
source "https://rubygems.org"

gem "ruboty"

gem "ruboty-tanzaku", github: "osyo-manga/gem-ruboty-tanzaku"
gem "ruboty-vimhelp"

# アダプタを追加
gem "ruboty-discord"
```

>>>

#### CLI 上で動かす

```
$ bundle install
# これで Discord と通信している状態になり
# Discord 上の Bot がアクティブになって動作する
# また Discord 上の Bot は発言のプレフィックスが
# ruboty ではなくて『その Bot の名前』になるので注意
$ bundle exec ruboty
```

---

## まとめ

---

#### まとめ
- - -

* こんな感じで簡単に Bot をつくることができる    <!-- .element: class="fragment" -->
* ハンドラだけ用意しておけばいいので、他の SNS で動かすことが容易    <!-- .element: class="fragment" -->
  * スマートスピーカで動くアダプタを用意すれば…
* Ruby は Rails だけじゃないんだよ！！！    <!-- .element: class="fragment" -->
* 学生LT の Discord には discord_bot開発部があるので興味がある人は来よう！！    <!-- .element: class="fragment" -->

---

#### 注意点
- - -

* Discord で動かすときは Bot の名前がプレフィックスになるので注意    <!-- .element: class="fragment" -->
  * ruboty hoge だと動かない
* 作った Bot は権限のあるサーバ（Discord のチャット部屋）でないと追加できない    <!-- .element: class="fragment" -->
  * Bot を試す場合は自分でチャット部屋を作っておく
* Discord の Bot はどこかで動かしておく必要があるよ！    <!-- .element: class="fragment" -->

---

## ご清聴
## ありがとうございました
