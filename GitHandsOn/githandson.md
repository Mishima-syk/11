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

    jupyter notebook

[IRISのPCAをやったら](ipynbs/msm11_1.ipynb)コミットします。

余談ですが、GitHubにipynb形式のファイルを
アップロードするとフォーマットしてくれます（md/markdown形式も）

    git add msm11.ipynb
    git ci -m "Add IRIS-PCA" (or git commit -m "Add IRIS-PCA")

## 状態確認

status(st)で状態を確認できます。

    git st (git status)

コミット履歴は

    git log

## さらにLDAを追加してコミット

[IRISのLDAをやったら](ipynbs/msm11_2.ipynb)コミットします。

一応変更があるか確認

    git status (git st)

ではコミットします。

    git add msm11.ipynb
    git ci -m "Add LDA-PCA" (or git commit -m "Add LDA-PCA")

またはaオプションをつけるとGit管理下にあって変更のあるものは全てaddされるので
次のように一行でかけます（僕は普段こっち）。

    git ci -am "Add LDA-PCA" (or git commit -am "Add LDA-PCA")

## 履歴確認

   コミット履歴を見てみましょう

    git log

## リバート（必要か？）

## ブランチ

## タグ

## マージ

## コンフリクトの解消

## git init --bare

## redmineとの連携の話

## GUIのツール紹介（今回は使わない）