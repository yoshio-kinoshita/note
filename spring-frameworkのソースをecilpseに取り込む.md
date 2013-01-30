# springのソースをeclipseに取り込む

# やること
* [github](https://github.com/SpringSource)からclone
* eclipse用のメタデータを以下のコマンドで生成
    import-into-eclipse.bat || import-into-eclipse.sh
* eclipseにインポート

proxy経由の場合は、gradlweのDEFAULT_JVM_OPTSに以下のvmオプションを書けばOK

    set DEFAULT_JVM_OPTS=-Dhttp.proxyHost=proxyHost -Dhttp.proxyPort=ProxyPort
    