#　元記事

[gitで起きたエラーの解決法 - Qiita](https://qiita.com/w-tdon/items/24348728c9256e5bf945)



------------------------------



# Gitで「Please tell me who you are」警告が出た際の対処方



commitしようとしたら、

```
$ git commit -m "initial commit"

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got '[PC名]')
```

となってcommitできなかったので対処法



# TL;DR

- アドレス設定：`$git config --global user.email [ここに自分のアドレス]`


- 名前設定：`$git config --global user.name [ここに自分の名前]`



# 解決法

エラー文の通り、gitに登録しているアドレスとユーザーネーム

がわかっていなかったため。



gitに自分を分からせるためにターミナルで以下を実行

- アドレス設定：`$git config --global user.email [ここに自分のアドレス]`

- 名前設定：`$git config --global user.name [ここに自分の名前]`