# spring batchのイントロダクション
ミッションクリティカルな環境でたくさんの処理が動いています。それらの処理は自動化されています。
処理は月次ベースなどで動いていて、

# spring batchを使うシーン

# spring batchのアーキテクチャ
![](http://static.springsource.org/spring-batch/reference/html-single/images/spring-batch-layers.png)

spring batchは

* Application
* Core
* Infrastructure

の3つに分かれます。

# チャンク単位での処理
spring2はチャンク単位での処理になりました。
![](http://static.springsource.org/spring-batch/reference/html-single/images/simplified-chunk-oriented-processing.png)


