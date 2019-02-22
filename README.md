# ansible sample for Nano Pi

Nano Piを簡単にセットアップするためのansibleスクリプトです。　　
ansibleの勉強として作りました。
小一時間で、以下のすべてのイントールと設定を実行できます。

- apt updateとupgrade
- ロケールとタイムゾーンの設定
- nfsやusbディスクのマウント
- folder2ramによるSDカードのtmpfs化
- netdataをインストール
- node.jsをインストール
- node-redのインストール

## Getting Started

以下の環境で試しています。
- MacOS Mojave 10.14.3
- ansible 2.7.1
- python version = 3.7.1
- nanopi-neo2_sd_friendlycore-xenial_4.14_arm64_20181011.img
- Nano Pi Neo / Neo2

Nano Piにssh接続できれば、すぐに実行できます。  
IPアドレスorホスト名、ssh用のID、パスワードを用意してください。

### Prerequisites

homebrew導入済みのmacへのansibleのインストールは以下の通りです。

```
$ brew install ansible
```
windows他の環境は試していません。検索してください。

### Installing

ansible.cfgにssh用のIDを書き込みます。
```
remote_user = pi
```

hostsに接続するNano PiのIPアドレスorホスト名を記入します。
```
[app10]
#app10.local
192.168.22.43
```

ansible-galaxyよりnetdata、node-redのロールをインストールします。
```
$ ansible-galaxy install mrlesmithjr.netdata
$ ansible-galaxy install trombik.node_red
```

以下のコマンドで実行します。
sshのパスワードを聞かれますので入力してください。
```
$ ansible-playbook site.yml

user-MBP:nanopi_ansible user$ ansible-playbook site.yml
SSH password:

PLAY [app10] *******************************************************************

TASK [Gathering Facts] *********************************************************
ok: [192.168.22.43]

TASK [apt : install aptitude] **************************************************
ok: [192.168.22.43]

TASK [apt : update all packages] ***********************************************
ok: [192.168.22.43]

TASK [apt : upgrade all packages] **********************************************
ok: [192.168.22.43]

TASK [apt : install apt packages] **********************************************

・・・
```

- node-redは以下のアドレスで開きます。
http://「Nano PiのIPアドレスorホスト名.local」:1880/

- netdataは以下のアドレスで開きます。
http://「Nano PiのIPアドレスorホスト名.local」:19999/