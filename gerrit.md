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
 
# jenkinsと連携する。
おそらくgerrit単体で使うよりjenkinsと連携させるパターンのほうが多いと思うので、連携についても解説します。

## jenkinsでgerrit toggleを設定する。
jenkinsのプラグインインで[Gerrit Trigger](https://wiki.jenkins-ci.org/display/JENKINS/Gerrit+Trigger)を設定します。

Gerritサーバー情報を入力し、テスト接続で接続を確認します。

* ホスト名：localhost
* フ ロントエンドURL:http://localhost:8080/
* SSHポート:29418
* ユーザ名：gerritを使うユーザ名
* sshキーファイル：先ほど生成したid_rsa
* sshキーファイルパスワード：sshキーファイルパスワード

jenkinsをリスタートし、gerrit toggle => control => start, stopが動くことを確認。


# gerrit構成
![alt](gerrit.png)

# ワークフロー
![alt](workflow-0.png)

# ~/.ssh/config
    Host tr
      Hostname git.example.com
      Port 29418
      User john.doe

# .git/config
    [remote "for-a-exp"]
      url = tr:kernel/common
      receivepack = git receive-pack --reviewer=a@a.com --cc=b@o.com
      push = HEAD:refs/for/experimental

# プロジェクト作成
管理画面から作成する。

# 権限設定
gerritが裏でこそこそ動き回るときのグループはNon-Interactive Usersのため、Non-Interactive Usersに権限設定します。
## READ権限
READ権限をrefs/*でNon-Interactive Usersに付与

## Label Code-Review権限
Label Code-Review権限をrefs/heads/*でNon-Interactive Usersに付与
## Label Code-Review権限
Label Code-Review権限をrefs/heads/*でNon-Interactive Usersに付与

## Label Verified
Label Verified権限をrefs/heads/*でNon-Interactive Usersに付与

後はメンバーの権限設定でご自由にレビュー権限などを付与してください。

# jenkisでgerrit toggleｐプラグイン設定
gerrit toggleプラグインを使うと、pushされた時点でgerritからjenkinsに連携され、指定された処理が動きます。
今回は warとsonarを実行しています。sonarチェックが完了すると、verifiedに１がセットされます。失敗した場合は -1です。
レビュー対象はverifiedが１のリソースです。

## ちょっとハマったこと。
$GERRIT_REFSPECをブランチに設定しています。この値はgerritから連携されるため、プロジェクトを手動で動かそうとしても動きません。

