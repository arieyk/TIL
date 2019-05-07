# Docker超入門 Part01 - Dockerを使った開発環境構築 メモ

プラスウイングTVさんのDocker超入門動画を実際に試してみた。

その過程を文章化したもの。



## なにはともあれ元動画

[Docker超入門 Part01 - Dockerを使った開発環境構築 - YouTube](https://www.youtube.com/watch?v=7mwoTs0LoYA&list=PLp_EUEO9JJP24hkHvRbS9hTLsjSMzbJrM)



## やること

Dockerで開発環境(Ruby on Rails)を作ってみよう。



## Dockerって？

- 仮想マシンの技術(vmwareやVirtualBox)と構成管理ツール(ChefやAnsible)をあわせてようなソフト



## 作ってみる

1. フォルダをどこかしらに作る

   ```
   mkdir rails
   ```

2. VSCodeで作成したフォルダを開く

3. 必要なファイルを作成する

   - Dockerfile

     ```dockerfile
     FROM ruby:2.6.3-stretch
     ```

   - docker-compose.yaml

     ```yaml
     version: '3'
     services:
       app:
         build: .
         volumes:
          - ".:/app"
         ports:
          - "3000:3000"
         tty: true
          
     ```

4. アプリを起動する

   ```
   docker-compose up
   ```

5. アプリにアクセスする

   別窓で

   `docker exec -it rails_app_1 /bin/bash`

6. Railsの設定1

   ```
   cd app
   gem install rails
   rails new .
   rails s -b 0.0.0.0
   ```

   →失敗する。RailsにはNode.jsが必要なため

7. Railsの設定2

   ```
   apt-get update
   apt-get install node.js
   rails s -b 0.0.0.0
   ```

   →なぜかここでエラー(Could not find rake-12.3.1 in any of the sources)

   ```
   rm -rf .bundle/
   bundle install
   rails s -b 0.0.0.0
   ```
   
   →これ[^1]でOK
   

   
8. アクセスしてみる

   https://localhost:3000/
   
   →Docker Toolboxの人は、localhostではなくVirtualBoxの指定IPにする。
   
   http://xxx.xxx.xx.xxx:3000/



## 参考

[^1]:[docker - rails can't find rake gem - Stack Overflow](https://stackoverflow.com/questions/49598686/rails-cant-find-rake-gem)