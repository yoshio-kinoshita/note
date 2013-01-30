# gerrit triggerを使う
[gerrit trigger](https://wiki.jenkins-ci.org/display/JENKINS/Gerrit+Trigger)のページに書いてありますが、日本語で書きます。

# セットアップ
* gerritと連携するユーザのssh keyをセットアップ
* gerritのページ -> Groups -> Non-Interfative Users -> 連携ユーザをセット
* 権限設定

## 権限設定
gerritが裏でこそこそ動き回るときのグループはNon-Interactive Usersのため、Non-Interactive Usersに権限設定します。
### READ権限
READ権限をrefs/*でNon-Interactive Usersに付与

## Label Code-Review権限
Label Code-Review権限をrefs/heads/*でNon-Interactive Usersに付与
### Label Code-Review権限
Label Code-Review権限をrefs/heads/*でNon-Interactive Usersに付与

### Label Verified
Label Verified権限をrefs/heads/*でNon-Interactive Usersに付与

# トリガー設定
gerritのイベントをトリガーにしてビルドすることができます。
以下に、トリガーの説明をそのまま貼り付けます。

* Patch set created 新しいチェンジかパッチセットがアップロードされた時にトリガー (デフォルト)
* Draft published ドラフトのチェンジかパッチセットが発表された時にトリガー (デフォルト、ただしドラフト機能を利用可能なGerritのバージョンの場合)
* Change merged チェンジがマージ/提出された時にトリガー
* Comment added レビューコメントが追加された時にトリガー（評価カテゴリーと評価値でフィルタリング）
* Reference updated ブランチやタグが更新された時にトリガー

Patch set createdを選んでおけばよいでしょう。
次に動的トリガーを設定します。

プロジェクトとブランチのパターンを設定します。
パターンはplainにして、gerritに登録したプロジェクト名とブランチ名を設定するのが無難でしょう。

# その他の設定
RefSpecに$GERRIT_REFSPEC。'Branches to build'に$GERRIT_BRANCHを設定してください。

後はgerritに変更をpushすれば動くはずです。