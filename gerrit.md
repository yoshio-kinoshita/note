# gerritインストールからもろもろ設定まで
[gerrit](http://code.google.com/p/gerrit/)のサイト。すべてここに乗っている情報ですが、インストールから設定までをざっくりまとめます。

# gerritとは
「げりっと」と読みます。コードレビューシステムです。 ci(俺はjenkins)と組み合わせることで単体テストやコード分析を通過したソースだけをコードレビュー対象にできます。

# 早速インストール
インストール方法についてざっくり。公式マニュアルにしたがってセットアップします。

## 前提条件
* jdk ver1.6以上が必要です。

## ユーザ生成
gerrit2という名前のユーザを追加

     $ sudo adduser gerrit2
     $ sudo su gerrit2

## gerritダウンロード
* [gerrit](http://code.google.com/p/gerrit/downloads/list)をからwarをダウンロード

## gerritサイト初期化
gerrit_testsiteという名前で作ります。

    java -jar gerrit.war init --batch -d ~/gerrit_testsite

いろいろ聞かれます。後から変更することも可能ですので、すべてデフォルトで設定しましょう。
設定が終わるとgerritが起動します。

    http://localhost:8080
    
でつながります。

#クライアント設定
クライアント側でssh keysの設定が必要です。

## SSHキー生成コマンド

    ssh-keygen -t rsa
    
## sshキー登録
gerritサイトからsshキーを登録します。

    http://localhost:8080
    
をブラウザで開き、sigin inします。デフォルトはopenid認証になるので、ログインしてください。
ログイン後、settings ＝＞ ssh public keys ＝＞ Add keyを開き、生成したid_key.pubを貼り付けてください_。

## 接続確認
接続できるか確認しましょう。クライアントから以下のコマンドを入力
    
    ssh user@localhost -p 29418 

ウェルカムメッセージが表示されれば、OKです。

    Welcome to Gerrit Code Review

# gerritプロジェクト生成
クライアントからプロジェクトを生成できます。

    ssh -p 29418 user@localhost gerrit create-project --empty-commit --name demo-project

# 既存プロジェクトを使う
既存プロジェクトの場合はプロジェクト生成後し、既存プロジェクトのルートへ移動後

	$ git clone 既存プロジェクト
	$ cd 既存プロジェクト
    $ git push ssh://user@localhost:29418/demo-project *:*

# pushする
gerritの場合pushする先は
    /refs/for/master
になります。そこにpushすることで、該当pushがレビュー対象になります。

    $ date > testfile.txt
    $ git add testfile.txt
    $ git commit -m "test commit"
    $ git pus origin HEAD:ref/for/master

間違って/ref/heads/masterにpushしたらレビュー対象外となります。
 