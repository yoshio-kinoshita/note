# プラグ可能性
servlet3.0からの新機能のJSP Container Pluggability.
jspをjarに含めることができるので、サブシステムをまるごとプラグイン化することができます。

# 使い方
WEB-INF/＊.jar/META-INF/resources配下にjspやhtlmを置くと、tomcatが自動的に読み込んでくれます。
jspをjarに入れるシーンってなさそうであったりするので、かなり便利。

一歩進めてSpringと連携する場合は、

    WEB-INF/＊.jar/META-INF/resource/WEB-INF/views/＊.jsp

とすることでViewResolverと連携することができます。
