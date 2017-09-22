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

## 図の見た目を気にして綺麗に並べる

[少し変更を施して](ipynbs/msm11_3.ipynb)コミットします。

一応変更があるか確認

    git status (git st)

ではコミットします。

    git ci -am "Change plot" (or git commit -am "Add LDA-PCA")

## kPCA

[IRISのKernel PCAを追加したら](ipynbs/msm11_4.ipynb)コミットします。

一応変更があるか確認

    git status (git st)

ではコミットします。

    git ci -am "Add kPCA" (or git commit -m "Add kPCA")

## revert

**コミットはしたもののkPCAはいまいちだったのでやっぱりなかったことにしたい**

消したいコミットIDを確認します

    git log

ではrevertします

    git revert fd668aea2c08 (idをコピペ)

確認

    git log

実際になかったことになっていることを確認します。
プロットが2つ並んでいるコミットまで戻っているはず

## ブランチ

そもそもコミットするかどうかわからない実験的な試みの場合、いつでも元に戻せるような
環境で試したいことがあります。それがブランチという枝分かれさせる昨日です。

枝分かれさせておいて破棄したい場合はそのまま削除、本体に取り込める場合にはマージして
とりこむということが出来ます。

tSNEで試してみましょう。ブランチを作成するコマンドはbranchですのでtsneというブランチを
作ってみましょう


    git branch tsne

git branchでどのブランチがあるのか確認できます。

    git branch
    * master
      tsne

masterが今のブランチなのでcheckoutすることでブランチを移ることが出来ます

    git co tsne
    Switched to branch 'tsne'
    
    git branch
      master
    * tsne

アスタリスクがついているのが現在のブランチです。ここでファイルに色々な変更を加えても
マスターは影響を受けません。

なお、ブランチをつくりつつそのブランチに移動するショートカットもあって

    git co -b tsne

とチェックアウト時に-bオプションを付ければOKです

では[tSNE](ipynbs/msm11_5.ipynb)を試してコミットしましょう。

    git ci -am "Add IRIS-tSNE"

ログを確認

    git log

## マージ

先程のtsneブランチの作業は上手くいったので、masterブランチに反映させたいところです。
この取り込み工程をマージするといいます

masterブランチに移ってtsneブランチをマージします

    git co master
    git branch # masterに移っていることを確認
    git log # tsneブランチで作ったコミットがないことを確認
    git merge tsne
    git log # tsneでのコミットがあることを確認

ブランチさせてマージさせることでmasterを常に綺麗に保つことが出来ます。汚れを溜め込まないのが
メンテナンス性を向上させるコツですね。

さていらなくなったtsneブランチはどうしたら良いでしょう？

サクッと消します。

    git branch -d tsne
    git branch # ブランチ確認

今回はブランチを一つ作りましたが、複数作ることが多いですし、例えばブランチである作業中だった時に
急ぎのべつの割り込みタスクが入ってきた場合、別途ブランチを作って先にそっちをやってからやりかけだった
元のブランチで作業するというようなことはよくあります。

うまくやるコツはマスターではなるべく作業せずにブランチを使ってマスターをできるだけクリーンに保つことです。

## タグ

## コンフリクトの解消

## git init --bare

## redmineとの連携の話

## GUIのツール紹介（今回は使わない）