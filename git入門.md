# git入門
gitを始めて使うとき、何をしたら良いのか分からんと思うのでざっくりまとめます。

# gitって
分散型版管理システム(dvcs)です。版管理する対象は基本的に成果物すべて。
とりあえず、svnと考え方が違います。最初は戸惑うと思いますが、いろいろできます。便利です。

# gitインストール
debianをサンプルにします。
    sudo aptitude install git

windowsは[msysgit](http://code.google.com/p/msysgit/)をインストールすれば使えるはずです。

インストール完了後

    git --version
    
でgitのバージョンが確認できます。

# ユーザ名とメールアドレスを設定
ユーザ名とメールアドレスを設定しましょう。この名前がコミット時に使われます。
    git config --global user.name "name"
    git config --global user.email "email"

ほかにもエディタやdiffツールを設定することができます。

    git config --global core.editor vim
    git config --global merge.tool vimdiff

俺はエディタはvim。diffツールはvimdiffを使います。
設定内容は

    git config --list
    
で確認できます。
後、statusやlogに色づけするため

   git config --global color.ui true

で、とりあえずgitお任せですが、色づけできて見やすくなります。

# gitの構成
gitには以下の３つがあります。

* リポジトリ
* インデックス(ステージング)
* ワーキングツリー

![ALT](http://git-scm.com/figures/18333fig0106-tn.png)

# ファイルのライフサイクル
ファイルのライフサイクルです。

![ALT](http://git-scm.com/figures/18333fig0201-tn.png)

# よく使うコマンド
コマンドはいっぱいありますが、よく使うコマンドをピックアップします。

* git init(リポジトリ初期化)
* git add(ステージングに変更を登録)
* git commit(リポジトリにコミット)
* git clone(既存リポジトリのクローン)
* git status(変更ファイル一覧)
* git rm(追跡対象ファイルの削除)
* git mv(追跡対象ファイルのリネーム)
* git push(リモートリポジトリに送信)
* git fetch(リモートリポジトリから変更を取得)
* git merge(ブランチをマージ)
* git pull(リモートリポジトリから変更を取得して現在のブランチにマージ.fetch + merge)
* git diff(変更内容確認)
* git log(コミットログ)
* git branch(ブランチ作成)
* git checkout(リポジトリからソース取得)
* git reset(ステージングに登録した変更を取消)
* git revert(コミットを取り消す)
* git remote(リモートリポジトリの表示)
* git rebase(他のブランチにコミットされた変更を再現する。)

# ヘルプを見る。

一気に覚えられないのでヘルプ見ながら徐々に覚えるのが吉。

    git help <verb>
    git <verb> --help

# リポジトリの初期化
リポジトリにしたいディレクトリを作成し以下のコマンドを実行

    $ mkdir testgit
    $ cd testgit
    $ git init

これでリポジトリができます。

# インデックスに登録
変更した内容をインデックスに登録します。

    $ echo test > test.txt
    $ git add test.txt
    
間違えて登録した場合は以下のコマンドで取り消せます。

    git reset test.txt

何もコミットしていない場合は以下のコマンドで取り消します。

    git rm --cached test.txt

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
    
## コミットを変更する。
git addし忘れたファイルがあった場合やコミットメッセージを変更する場合に使います。

    git commit --amend
    
たとえば、コミット漏れの場合です。

    git commit -m 'first commit'
    git add forget.txt
    git commit --amend

これで最初のコミットにforget.txtも含まれます。

# リモートリポジトリのクローン

    git clone git://github.com/schacon/ticgit.git

# リモートリポジトリの表示

   git remote -v


# リモートリポジトリにpush

    git push 
	
# 変更履歴を見る

    git log

# 現状態

    git status
 
## 変更を取り消す
間違ってエディットした場合の取消方法はgit status内に記述されています。

    git checkout -- <filepath>

# 変更点を確認する
インデックスにとワークツリーの比較

    git diff
    
最新コミットとワークツリーの比較

    git diff HEAD
    
# コミットを取り消す
コミットを取り消しますが、取り消したログは残ります。

    git log
    git revert commit番号
    
# リモートからフェッチ
リモートリポジトリからデータを取得します。

    git fetch <remote-name>

ただし、これはローカルリポジトリにデータを取得するだけでワークツリーには入りません。
ワークツリーに入れる場合はmergeする必要があります。

    git merge <branch>
    
これだと面倒なので、fetch と マージを一回でやるコマンドpullです。
 
    git pull <remote-name>

これでfetch & mergeしてくれます。

# ファイルの無視

.gitigonoreを記述する。

# rebase
mergeとrebaseの違いにつまづくと思います。
rebaseについては[ここ](http://git-scm.com/book/ja/Git-%E3%81%AE%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E6%A9%9F%E8%83%BD-%E3%83%AA%E3%83%99%E3%83%BC%E3%82%B9)を読んでください。

ちょっと分かりづらいのでgit logで見てみましょう。

## mergeした場合
マージした場合、 git log コマンドには、以下のように出力されます。

    Merge branch 'master' into branch1

## rebaseした場合
リベースした場合、git logコマンドには以下のように出力されます。

    rebase対象をコミットします。

## merge vs rebase
git logを見比べると、何が違うか。mergeした場合はマージしたログが出ますが、rebaseの場合は出ません。
rebaseのほうがブランチ構成がシンプルになります。

## first-foward
ファーストフォワードというキーワードが出てくるのですが、詳しい解説がないので追記します。
ファーストフォワードというのはコミット1と2があるとき、コミット2にはコミット1がすべて含まれていることを言います。

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
