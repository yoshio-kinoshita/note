# VirtualBoxにUbuntu入れてjenkins使ってみた。
jenkinsをどうしても試してみたくて。けど、windowsだといろいろハマりそうだったので、今回は以下の環境で構築してみました。

+ [VirtualBox](https://www.virtualbox.org/)
+ [Ubuntu12.10](http://www.ubuntulinux.jp/)
+ [Jenkins](http://jenkins-ci.org/)
+ [git](http://git-scm.com/)
+ [maven3](http://maven.apache.org/)
+ [gerrit](http://code.google.com/p/gerrit/)
+ [sonar](http://www.sonarsource.org/)

# やったこと。
VirtualBoxをインストールして、Ubuntu12.10のイメージを使って起動。メモリ割り当ては2Gにしました。 Ubutuの設定で30分ぐらい？
aptitude入れて、jenkis,git,maven3をインストール。
gerrit,sonnarはサイトからダウンロードしたものを使いました。

# jenkins起動
jenkinsをインストールすると、すでに起動しています。

    http://localhost:8080/
    
再起動するときやとめるときは
    /etc/init.d/jenkis start | restart | stop

# 試したプラグイン
**jenkinsの管理**からいろいろプラグインをインストールできます。
今回、以下のプラグインを試してみました。

+ Findbugs
+ checkstyle
+ cpd
+ pmd
+ Sonar
+ maven
+ Gerrit Trigger

# 感想
jenkins + gerrit + sonarでプロジェクトをまわせば、かなり安定した開発ができると感じました。
成果物の内容がグラフ化されるので、自分達のソースを客観的に判断できると思います。まぁ、どう使うかは結局自分たち次第ですが。。。
なお、sonarやgerritの設定は書いたら改めて共有します。


