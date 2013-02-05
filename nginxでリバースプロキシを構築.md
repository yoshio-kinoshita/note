# nginxでリバースプロキシを構築
jenkinsやらsonarやらgerritやらをたてていますが、urlにポート番号が入っちゃっています。
これだと覚えるの大変なので、nginxでリバースプロキシたててポート番号を排除します。

# nginx
[nginx](http://nginx.com/)を参考にしました。

# ダウンロード
downloadページからnginxの最新をダウンロード.pgp比較して本物を確認

# nginxについて
![alt](http://www.aosabook.org/images/nginx/architecture.png)



