# Docker 入門講座 実践編


## Nginx
<span style="font-size: 200%"> **Nginxのコンテナを起動** </span>

`$ docker run nginx`



<span style="font-size: 200%"> **これだけ！！！！！！！** </span>

- DockerしかインストールしていないのにこれだけでWebサーバが立つ

- `-v`オプションで設定ファイルやHTMLファイルやHTMLファイルをマウントすればそれだけで思い通りに動かせる

- 外部に公開するなら`-p 80:80`とすれば80番ポートで公開される

  左がホストOS、右がDocker