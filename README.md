## 概要

* 筑波大enPiTでrailsアプリを作る人の用の開発環境を自動作成するVagrantファイルです。
* 産技大enPiTのレポジトリ [github:ychubachi/vagrant_enpit](https://github.com/ychubachi/vagrant_enpit) を元に作っています。
 * vm.boxに CentOS 6.5  を使っているのが異なるところです
  * cloudstack on idcf cloud へ同じ環境をデプロイすることを想定
 * forkしてないのは実は一から作り直したから…
 * 元レポジトリにあった extra_provision.sh はやらなくても良い。 

## 準備

* Vagrant
* VirtualBox
* Chef DK

## Vagrantのプラグイン
* VagrantにChef，Berkshelfのプラグインを入れる．

```bash
vagrant plugin install vagrant-omnibus
vagrant plugin install vagrant-berkshelf
vagrant plugin install vagrant-cloudstack
vagrant plugin install dotenv
```

## VirtualBox上に仮想マシンを作成する場合

### 起動

* レシピのインストール．

```bash
% berks install
```

* 起動する．

```bash
vagrant up
```

## cloudstack上に仮想マシンを作成する場合

### 準備
* .envファイルを用意する
```bash
% cp dot.env.sample .env
```
* .envファイルを開き、接続先について必要項目を埋める

* Vagrantfileを開き89行目をコメントアウトする
```
 #chef.add_recipe "gems"
```

### 起動

```bash
% berks install
% vagrant up --provider=cloudstack
```

* 途中で以下のメッセージが表示されて止まってしまった場合には下記の対応をしてください。
```bash
==> default: sudo を実行するには tty がなければいけません。すみません
```

```bash
% vagrant ssh
vagrant@guestos> sudo visudo
```
viエディタで設定ファイルが開くので
```bash
 Defaults: requiretty
 ```
となっているところを

```bash
 Defaults: !requiretty
```
に変更して保存してログアウト。そのあと以下を実行。

```bash
% vagrant provision
```
