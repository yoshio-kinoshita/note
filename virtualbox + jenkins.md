# VirtualBoxにUbuntu入れてjenkins使ってみた。
jenkinsをどうしても試してみたくて。けど、windowsだといろいろハマりそうだったので、今回は以下の環境で構築してみました。

+ [VirtualBox](https://www.virtualbox.org/)
+ [Ubuntu12.10](http://www.ubuntulinux.jp/)
+ [Jenkins](http://jenkins-ci.org/)

jenkinsはaptitudeでインストールしました。

# 試したプラグイン
jenkinsにはいろいろなプラグインがあります。以下のプラグインを試してみました。

+ Findbugs
+ checkstyle
+ cpd
+ pmd
+ sonar
+ maven
+ gerrit

# 感想
jenkins + gerrit + sonarでプロジェクトをまわせば、かなり安定した開発ができると感じました。
成果物の内容がグラフ化されるので、自分達のソースを客観的に判断できると思います。まぁ、どう使うかは結局自分たち次第ですが。。。


