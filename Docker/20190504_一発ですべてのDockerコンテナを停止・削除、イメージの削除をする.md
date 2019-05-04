#　元記事

 [一発ですべてのDockerコンテナを停止・削除、イメージの削除をする](https://qiita.com/shisama/items/48e2eaf1dc356568b0d7)



------------------------------



# 一発ですべてのDockerコンテナを停止・削除、イメージの削除をする

起動しているすべてのDockerコンテナの停止や削除をするときに使っているコマンドが便利なので紹介したいと思います。
紹介するコマンドは[Docker For Mac](https://www.docker.com/docker-mac)で実行し確認しました。



# TL;DR
- 全コンテナ停止: `docker stop $(docker ps -q)`

- 全コンテナ削除: `docker rm $(docker ps -q -a)`

- 全イメージ削除: `docker rmi $(docker images -q)`

  

# すべてのコンテナを停止する

```
docker stop $(docker ps -q)
```

`docker stop`に関しては説明不要かと思います。
`$(docker ps -q)`の部分に関してですが、
`docker ps`の`-q`フラグを付けることでコンテナのIDのみを取得します。

例えば、以下のように起動しているコンテナがある場合

```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
e2d41562fb71        ubuntu              "/bin/bash"         39 hours ago        Up 13 seconds                           affectionate_bassi
d886772499bd        ubuntu              "/bin/bash"         45 hours ago        Up 12 seconds                           gallant_curran
96b81bf5c03d        alpine              "/bin/sh"           47 hours ago        Up 11 seconds                           cocky_chebyshev
```

`docker ps -q`を実行すると以下のようにコンテナIDのみ表示されます。

```
e2d41562fb71
d886772499bd
96b81bf5c03d
```

このコンテナIDのみ取得する方法を利用しています。

```
docker stop $(docker ps -q)
```
は以下を実行しているのと同じです。
```
docker stop e2d41562fb71 d886772499bd 96b81bf5c03d
```



# すべてのコンテナを削除する

要領は前項と同じです。

```
docker rm $(docker ps -q -a)
```

`docker ps`では起動しているコンテナのみ表示します。
停止しているコンテナも含めすべてのコンテナを表示するには`-a`フラグを用います。

ただし停止しているコンテナのみを削除するので、全てのコンテナを削除するには前項で紹介した方法を用いてコンテナをすべて停止する必要があります。



# すべてのイメージを削除する

```
docker rmi $(docker images -q)
```
`docker images`でも`ps`コマンドと同じように`-q`フラグを用いることでイメージIDのみ取得することができます。

通常はコンテナが停止していないとDockerのイメージを削除することができませんが、`-f`フラグを用いることでコンテナが削除されていなくてもイメージを削除することができます。

```
docker rmi $(docker images -q) -f
```

ただしコンテナが起動している場合はイメージを削除できませんのでコンテナを停止する必要があります。

```
docker stop $(docker ps -q) && docker rmi $(docker images -q) -f
```



# 最後に

筆者は`.bash_profile`に以下を記述しaliasに登録しています。

```
alias docker-purge='docker stop $(docker ps -q) && docker rmi $(docker images -q) -f'
```

一つ一つコンテナの停止・削除、イメージの削除を行っていたときより非常に捗るようになりました。
本記事が皆様の一助になると幸いです。