# sonar入れてみた。
jenkinsと連動させてたくてsonar入れてみた。

# 環境
環境は以下のとおり

+ VirtualBox + Ubuntu
+ [Sonar](http://www.sonarsource.org/)

# sonarって？
詳しくは[ここ](http://www.sonarsource.org/features/)を見てください。
ざっくり説明すると、以下のことをやってくれます。

+ コーディングルールチェック
+ 単体テストとカバレッジ測定
+ ソース分析(重複や複雑度、ライン数やクラスなどの計測)
+ 時系列でプロジェクト状態を表示

つまり、プロジェクトのソース状態をさまざまな視点からチェックしてくれます。チェック内容はカスタマイズできるので、プロジェクトごとにルールを変えて運用することになります。
また、インタフェースも良いと思います。

どんな感じかはサンプルプロジェクトの[nemo](http://nemo.sonarsource.org/)を見てみてください。

## sonarアーキテクチャ
sonarのhpから引用します。

![id](http://docs.codehaus.org/download/attachments/229736899/technical-architecture.png?version=3&modificationDate=1338554386797)

# sonarインストール方法
[ここ](http://docs.codehaus.org/display/SONAR/Installing+and+Configuring+Sonar+Runner)に詳しく書いてあります。
ざっくり言うとダウンロードして、スタートスクリプト実行。これだけ。

## 必要なもの
[ここ](http://docs.codehaus.org/display/SONAR/Requirements)参照。dbの文字コードはutr-8にしてください。

# 実行方法
僕はjenkins + sonarだったのでjenkins上でsonarプラグインを設定。インストールしたsonarへのURLを指定しました。ローカルで動かす場合は[ここ](http://docs.codehaus.org/display/SONAR/Analyzing+Source+Code)に詳しく書いてあります。
mavenとantでももちろん動かせますが、[sonnar runner](http://docs.codehaus.org/display/SONAR/Analyzing+with+Sonar+Runner)が推奨らしいです。

## sonar runnerで使う
[sonnar runnerのインストールページ](http://docs.codehaus.org/display/SONAR/Installing+and+Configuring+Sonar+Runner)を参考に入れました。
やることは

+ sonar runnerをダウンロード
+ $SONAR_RUNNER_HOME/conf/sonar-runner.propertiesを環境に合わせて編集。 sonarをデフォルトでかつローカルで動かす場合は、sonar-runner.propertiesはデフォルトでも大丈夫なはずです。
+ $SONAR_RUNNER_HOME/binにパスを通す。
+ sonar-runner -hで起動確認 

これで、sonar-runnerの設定が完了です。

### sonar runnerを起動。
任意のプロジェクトをsonar runnerで動かすためにはプロジェクトのrootにsonar-runner.propertiesを改めて置く必要があります。

###sonar-project.properties
    # required metadata
    sonar.projectKey=my:project
    sonar.projectName=My project
    sonar.projectVersion=1.0
     
    # optional description
    sonar.projectDescription=Fake description
     
    # path to source directories (required)
    sonar.sources=srcDir1,srcDir2
     
    # path to test source directories (optional)
    sonar.tests=testDir1,testDir2
     
    # path to project binaries (optional), for example directory of Java bytecode
    sonar.binaries=binDir
     
    # optional comma-separated list of paths to libraries. Only path to JAR file and path to directory of classes are supported.
    sonar.libraries=path/to/library/*.jar,path/to/classes/dir,path/to/specific/library/myLibrary.jar,parent/*/*.jar
     
    # The value of the property must be the key of the language.
    sonar.language=java
     
    # Additional parameters
    sonar.my.property=value
    
プロパティファイルを置いたらプロジェクトのrootに移動して

    sonar-runner
    
をたたくとsonar runnnerが起動し、sonar上でいろいろチェックが動きます。完了後、sonarを開くと該当プロジェクトが登録されているはずです。

# eclipseで使う
マニュアル読んでて見つけました。「*[Using Sonar in Eclipse](http://docs.codehaus.org/display/SONAR/Using+Sonar+in+Eclipse)*」。おおー。いいっすねー。
で何ができるのかというと。

+ sonarのチェック結果をソース上に表示できる。
+ チェック結果をProblemタブに表示できる。
+ ローカルモードならでsonarのチェックをeclipseから起動できる。

などです。
手順は上記リンクに書いてあります。事前準備として、sonar runnerなどでプロジェクトをsonarに登録する必要があります。

+ update site(http://dist.sonar-ide.codehaus.org/eclipse/)からプラグインインストール
+ Window => Preferences => Sonar => ServerでSonarサーバを指定。
+ プロジェクトを右クリック => configure => Associate with Sonar => 該当プロジェクトを選択
+ プロジェクトを右クリック => Sonar => mode => Localにすると、**Run Local Analysis**が有効になります。

# Continuous Integration
以下ののCIServerと組み合わせることで一段とsonarの力を発揮できます。

+ jenkis
+ Bamboo(sonarのプラグイン) 
+ Apache Continuum 1.2

jenkinsが一般的だと思います。