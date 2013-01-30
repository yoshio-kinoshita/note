# jemterをコマンドラインで起動する。
jmeterをコマンドラインで実行しようとするときのオプションをちょいちょい忘れるのでメモ。

     sh apache-jmeter-2.8/bin/jmeter.sh -n -t hogehoge.jmx -l log.jtl

ログファイルに結果が出力されるので、Guiモードで起動してサンプラーで読み込めば結果が確認できる。

# お勧めサンプラー
jmeter2.8から追加された以下のサンプラーがお勧め

## Response Time Graph
各処理のレスポンスタイムをグラフィカルに表示できます。
![response time graph](http://jmeter.apache.org/images/screenshots/changes/2.8/09_resp_time_graph.png)

## Aggregate Graph
処理の平均や中間値,90%ラインなどをグラフィカルに表示できます。
![Aggregate Graph](http://jmeter.apache.org/images/screenshots/changes/2.8/07_aggregate_graph_legend_left_right.png)

これと既存のサンプラーいくつか使えば、ばっちり計測できるはずです。
