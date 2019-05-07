# Docker超入門 Part02 - Dockerfileをちゃんと書く メモ

プラスウイングTVさんのDocker超入門動画を実際に試してみた。

その過程を文章化したもの。



## なにはともあれ元動画

[Docker超入門 Part02 - Dockerfileをちゃんと書く - YouTube](https://www.youtube.com/watch?v=Hm_EtjXBYOM&list=PLp_EUEO9JJP24hkHvRbS9hTLsjSMzbJrM&index=2)



## やること

前回やったDockerに入ってなにかしらインストールするは邪道。

今回はそれを訂正する。



## 前回の内容をDockerfileで行う

1. Dockerfileに追記

   - Dockerfile

     ```dockerfile
     FROM ruby:2.6.3-stretch
     
     RUN gem install rails
     
     RUN apt-get update && \
     	apt-get install -y node.js
     ```

     

2. 実行してみる

   ```
   docker-compose up --build
   ```

   buildオプションを付けると、Dockerのコンテナを破棄して新しく実行してくれる

   

3. アプリにアクセスする

   別窓で

   `docker exec -it rails_app_1 /bin/bash`

   

4. Railsの設定1

   ```
   bundle install
   rails s -b 0.0.0.0
   ```

   

5. アクセスしてみる

   https://localhost:3000/
