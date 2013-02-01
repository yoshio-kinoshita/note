# jenkinsでthinBackupプラグインを試してみる
jenkinsでどのようにバックアップ取るのが楽かを調べてみました。

条件として

* スケジュールでバックアップ
* リストア簡単。
* バックアップ対象は設定だけ。リソースはいらない。

です。backupプラグインがあったのですが、それではスケジューリングできず。antだとリストア簡単とは言えなさそうでした。
で、色々調べてみたらthinBackupというプラグインを発見。良さそうなので試してみます。

# thinBackup
ページは[ここ](https://wiki.jenkins-ci.org/display/JENKINS/thinBackup)
インストールして、パラメタを設定していきます。

## Backup directory
jenkinsプロセスが読み書きできるディレクトリを指定します。

## Backup schedule for full backups
cron形式で記述します。月-金で12時バックアップにします。

    0 12 * * 1-5

## Backup schedule for differential backups
差分バックアップです。使わないので何も書きません。

## Max number of backup sets
バックアップを何世代前まで保持するかです。なんとなく5にしてみます。

## Files excluded from backup (regular expression)
バックアップ対象外。

# 手動でバックアップ
backupを押せば手動でバックアップ取れます。

# リストア
リストアボタンを押してリスト対象を選べばokです。

# 最後に
バックアップ、リストアが楽にできるので良いプラグインだと思います。
これで何かあっても設定は復活できます。


