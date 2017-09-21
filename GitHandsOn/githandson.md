# Git Handson

- jupyter notebookをgitで管理する例を通して簡単な使い方を学びます。

## Install

### Git

https://git-scm.com/downloads

から自分のOS用のものをダウンロードしてインストール

### jupyter

*** Condaでjupyter installする方法 誰か書いて ***

### pandas

*** Condaでjupyter installする方法 誰か書いて ***


## 最初の設定(最低限やらないといけないこと)

nameとemail addressの設定はやっておく

    git config --global user.email "you@example.com"
    git config --global user.name "Your Name"


## エイリアスなどやっとくと便利な設定

あとあとのことを考えるとエイリアスは設定しておいたほうが便利

    git config --global alias.co checkout
    git config --global alias.ci commit
    git config --global alias.st status
    git config --global alias.br branch

このあたりを参考に

http://blog.karky7.com/2012/12/git.html

## リポジトリの作成

initialize

    mkdir msm11
    cd msm11
    git init

## ファイルの登録

## 状態確認

## コミットを行う

## さらに色々追加

## さらにコミット

## 履歴確認

## リバート（必要か？）

## ブランチ

## タグ

## マージ

## コンフリクトの解消

## git init --bare

## redmineとの連携の話

## GUIのツール紹介（今回は使わない）