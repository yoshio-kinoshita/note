# gitで日本語ファイル名が文字化けする
UTF-8環境で日本語ファイル名が文字化けする場合は以下のオプションを設定すればOKです。

     git config --global core.quotepath false

これで

     git status

などでも文字化けせずにファイル名を見ることができます。
