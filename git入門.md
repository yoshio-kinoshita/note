# git入門
gitを始めて使うとき、何をしたら良いのか分からんと思うのでざっくりまとめます。

# gitって
分散型版管理システム(dvcs)です。版管理する対象は基本的に成果物すべて。
とりあえず、svnより複雑ですが、いろいろできます。便利です。

# gitインストール
debianをサンプルにします。
    sudo aptitude install git

windowsは[msysgit](http://code.google.com/p/msysgit/)をインストールすれば使えるはずです。

# ユーザ名とメールアドレスを設定
ユーザ名とメールアドレスを設定しましょう。この名前がコミット時に使われます。
    git config --global user.name "name"
    git config --global user.email "email"


# gitの構成
gitには以下の３つがあります。
* リポジトリ
* インデックス(ステージング)
* ワーキングツリー

## リポジトリとインデックスとワーキングツリー
リポジトリとワーキングツリーはまぁ、大丈夫だと思いますがインデックスってのがGit独自ですね。
インデックスというのはワーキングツリーとリポジトリの間にある層です。これがあることによって、コミット内容をきれいに練り上げることができます。

![ALT](http://git-scm.com/figures/18333fig0106-tn.png)

# よく使うコマンド
コマンドはいっぱいありますが、よく使うコマンドをピックアップ

* git init(リポジトリ初期化)
* git add(ステージングに変更を登録)
* git commit(リポジトリにコミット)
* git push(リモートリポジトリに送信)
* git fetch(リモートリポジトリから変更を取得)
* git merge(ブランチをマージ)
* git status(変更ファイル一覧)
* git diff(変更内容確認)
* git log(コミットログ)
* git branch(ブランチ作成)
* git checkout(ブランチ取得)
* git reset(ステージングに登録した変更を取消)
* git revert
* git rebase

# ヘルプを見る。
ヘルプに大体のことは書いてあります。
    git help <verb>
    git <verb> --help

# リポジトリの初期化
リポジトリにしたいディレクトリを作成し以下のコマンドを実行
    git init

# インデックスに登録
変更した内容をインデックスに登録します。
    git add <filepattern>
    
間違えて登録した場合は以下のコマンドで取り消せます。
    git reset <filepattern>
 
# コミット
コミットは以下の内容でできます。
    git commit -m "コメント"

Gitのルールでコミットコメントは細かく書くということになっています。書き方のサンプルをあげます。

    1行目：対応内容の1概要
    2行目：空
    3行目以降：コミット内容を説明する。
    
コメントをちゃんと書くと１コミット２分ぐらいはかかります。またコミットの単位は論理的に意味のある単位にしたほうがよいらしいです。

また、以下のコマンドで対話形式でコミットメッセージを書くことができます。
    git commit -i 

# 既存リポジトリのクローン
    git clone ssh://ユーザ名@172.21.52.47/リポジトリ名

# リモートリポジトリにpush
    git push origin HEAD:refs/for/master
    

以下のブランチにコミットするとレビューなしで取り込まれます。
使っちゃだめです。
    git push origin HEAD:refs/heads/master
	
# 変更履歴を見る
    git log

# 現状態
    git status
    
# 変更点を確認する
インデックスにとワークツリーの比較
    git diff
最新コミットとワークツリーの比較    
    git diff HEAD
    
# コミットを取り消す
コミットを取り消しますが、取り消したログは残ります。
    git log
    git revert commit番号

# ファイルの無視
.gitigonoreを記述する。

# rebase
[ここ](http://www.backlog.jp/git-guide/stepup/stepup1_4.html)のrebaseに詳しく書いてある。


# コミットをなかったことにする。
ログを含めすべてなかったことにします。
    git reset HEAD^

# コミットをやり直す
    git commit --amend

# ワークツリーの変更を取り消す
    git checkout <paths>
    
# bareリポジトリ
ワーキングツリーがないリポジトリ。中央リポジトリとして使う。
    git init --bare
    
# 用語
## patch(パッチ)
git diffの出力結果の形式。

### パッチサンプル
    yoshiokinoshita@yoshiokinoshita-ubuntu:~/gitusers$ git diff
    diff --git a/index.html b/index.html
    index 1d70c8a..73bf963 100644
    --- a/index.html
    +++ b/index.html
    @@ -3,6 +3,7 @@
     </head>
     <body>
     <h1>hogehoge</h1>
    -<p>test</p>
    +<p>test before</p>
    +<p>test2</p>
     </body>
     </html>
    
## hunk(ハンク)
git diffの出力結果のうち、@@マーカーの後のインデントされたファイルの内容

### ハンクサンプル
     </head>
     <body>
     <h1>hogehoge</h1>
    -<p>test</p>
    +<p>test before</p>
    +<p>test2</p>
     </body>
     </html>

## HEAD(ヘッド)
現在最新のコミットのことをHEADと呼ぶ。

## origin
リポジトリをクローンしたときには、リモートリポジトリに対して自動的に origin という名前がつけられます。

## origin/master
(remote)/(branch)で、リモートリポジトリのmasterブランチを指す。

## Fast-forward と Non Fast-forward
[ここ](http://www.backlog.jp/git-guide/stepup/stepup1_4.html)に丁寧な解説あり。

# cloneサンプル
    git clone ssh://ykinos@172.21.52.47:29418/testproject
# pushサンプル
    git push origin HEAD:refs/for/master

# gerritプロジェクト作成
    ssh -p 29418 ykinos@172.21.52.47 gerrit create-project --empty-commit --name testproject

# gerritでno common ancestry

# gerrit接続チェック
    ssh -p 29418 172.16.5.95

# 鍵生成

# git ssh で ssh Bad file number



