## 概要

* 筑波大enPiTでrailsアプリを作る人の用の開発環境を自動作成するVagrantファイルです。
* 産技大enPiTのレポジトリ [github:ychubachi/vagrant_enpit](https://github.com/ychubachi/vagrant_enpit) を元に作っています。
 * vm.boxに CentOS 6.5  を使っているのが異なるところです
  * cloudstack on idcf cloud へ同じ環境をデプロイすることを想定
 * forkしてないのは実は一から作り直したから…
 * 元レポジトリにあった extra_provision.sh はやらなくても良い。 

## 準備

- Vagrant
- VirtualBox
- Chef DK

## Vagrantのプラグイン
VagrantにChef，Berkshelfのプラグインを入れる．

```bash
vagrant plugin install vagrant-omnibus
vagrant plugin install vagrant-berkshelf
```

## 起動

レシピのインストール．

```bash
berks install
```

起動する．

```bash
vagrant up
```

* 途中hubのインストールで"goがないよ"というエラーで落ちたら以下のコマンドで
再度実行すると動くはず。

```bash
vagrant provision
```






