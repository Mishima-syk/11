# Git Hands-on

- jupyter notebookをgitで管理する例を通して簡単な使い方を学びます。

## Install

### Git

https://git-scm.com/downloads

から自分のOS用のものをダウンロードしてインストール

### jupyter

普通に入れられる、または伝統的なインストールのお作法が好きな方はそっちで入れてください。
macだとbrewで入れたりするといいでしょう。

#### anaconda

そうでない人達は
[データサイエンティストを目指す人のpython環境構築 2016](https://qiita.com/y__sama/items/5b62d31cb7e6ed50f02c)を参考に
インストールしてください

python3を入れたほうが良いでしょう。


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

コミットにバージョンなどのタグをつけることが出来ます。一人で使うときにはあまり使わないと思います。

    git tag # タグ一覧が見れます
    git tag v1.0 # タグをセット

# 複数箇所で使う（Gitの分散管理に関して知る）

一人で一通り使えるようになったら、複数箇所で使うことを考えます。例えば自分のノートパソコンとサーバーで使うといった用途です。

Gitで管理されているディレクトリは簡単に複製を作ることが出来ます。

    cd ~
    mkdir deb
    cd deb
    git clone ~/msm11

と打つだけで先程まで行っていたjupyterタスクの複製が作られます。

もちろんホスト間でもcloneは可能で

    git clone host:~/msm11
    git clone https://host/msm11

のようなこともできます。会社で使う場合は大抵sshをつかったクローンが多くなると思います。

分散管理に関してはこのあたりを読むと良いでしょう。

https://git-scm.com/book/ja/v1/Git-%E3%81%A7%E3%81%AE%E5%88%86%E6%95%A3%E4%BD%9C%E6%A5%AD-%E5%88%86%E6%95%A3%E4%BD%9C%E6%A5%AD%E3%81%AE%E6%B5%81%E3%82%8C

## git init --bare

ただし、複数箇所で使う場合はどこか一箇所で管理したいとか、そこでは開発する必要はなくてバックアップ先として
使いたいというニーズのほうが多いと思います。
そういったプロジェクトの管理専用のGitディレクトリを作成したい場合は、bareオプションをつけてinitします

    mkdir ~/anotherrepo
    cd ~/anotherrepo
    git init --bare

このオプションで作られたディレクトリでは作業が出来ず。pushしたりcloneするだけのディレクトリになります。

## 作ったリポジトリをoriginに指定して、pushする

ここから cloneすればどこが親だかわかっているのでgit pushでcloneもとにコミットがプッシュされます。

既に手元にあるGitレポジトリを新たに作ったbareのリポジトリにpushするにはどうしたらいいでしょうか？

    git remote add origin ~/anotherrepo (absdirのほうがよい)
    git push -u origin master

## 任意のコミットをチェックアウトする

ログを見てチェックアウトしたいバージョンを調べます。

    git log

    commit 38aaefb7c6d2d228569876dd6648a256a2fa7fdc
    Author: Kazufumi Ohkawa <kerolinq@gmail.com>
    Date:   Fri Sep 22 10:07:01 2017 +0200
    
        Add IRIS-tSNE
    
    commit 72495d9d7c44e4ffc21917ded456e591c23d36d0
    Author: Kazufumi Ohkawa <kerolinq@gmail.com>
    Date:   Fri Sep 22 06:04:03 2017 +0200
    
        Revert "Add kPCA"
        
        This reverts commit fd668aea2c08bf734e968c6d980539dc8f0273f5.
    
    commit fd668aea2c08bf734e968c6d980539dc8f0273f5
    Author: Kazufumi Ohkawa <kerolinq@gmail.com>
    Date:   Fri Sep 22 05:58:55 2017 +0200
    
        Add kPCA
    
    commit e931e56747f4105e84151e1e8d2e988c42889cfa
    Author: Kazufumi Ohkawa <kerolinq@gmail.com>
    Date:   Fri Sep 22 05:08:08 2017 +0200
    
        Change Figure

commit番号を指定してcheckoutします。全部指定しなくても一意に決まればOKです

    git co fd668aea2c08bf7

## コンフリクトの解消

複数箇所で作業するとコンフリクトという現象が発生します。
今回はそこまでやらないので、コンフリクトしたら以下を参照して解決してください☆

http://qiita.com/hkengo/items/f47b9f50ac2dca407d12

## GitHubへ

このように、普段の仕事ではチームのコードを一箇所にまとめて管理するサーバーを立てることが多いと思います。
もしチームの垣根を超えて、大きなコミュニティーで一つの巨大なリポジトリマネジメントが出来たらどうなるでしょう？
そしてgit init --bareというようなルーティーンもウェブ上から簡単に行えるようになっていたり、チケットや、バグ報告も
ウェブの掲示板的な仕組みと連動していたら？

それがGitHubです。

## redmineとの連携の話

redmineのサーバーと同じホストにGitディレクトリを作ると、redmineと連携させることが出来ます。

- redmine上でコードの差分管理ができる
- [チケットとブランチを対応させる](https://git-scm.com/book/ja/v1/Git-%E3%81%AE%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E6%A9%9F%E8%83%BD-%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E3%81%A8%E3%83%9E%E3%83%BC%E3%82%B8%E3%81%AE%E5%9F%BA%E6%9C%AC)ことで効率的な開発が行える

## jupyterのテンプレートを用意したい。

テンプレートファイルを用意したらgit cloneでクローンして
使い捨てればよいと思います。

## GUIのツール紹介（今回は使わない）

- gitk(これはgit入れると使えるようになっているはず)
- [sourcetree](https://ja.atlassian.com/software/sourcetree)
- [github desktop](https://desktop.github.com/)