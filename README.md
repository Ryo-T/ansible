# ansible
僕の考えた最強のansible

■環境
```
$ python --version
Python 2.7.5

$ cat /etc/redhat-release
CentOS Linux release 7.5.1804 (Core)
```

■インストール
```
$ sudo yum -y install epel-release
$ sudo yum -y install ansible
```

確認
```
$ ansible --version
ansible 2.5.3
  config file = /etc/ansible/ansible.cfg
```

■コマンド例
# 構文チェック
```
$ ansible-playbook -i hosts simple-playbook.yml --syntax-check
```
# dry-run
```
$ ansible-playbook -i production -vv site.yml -T 15 -D --tags=hosts --check
```
# 実行
```
$ ansible-playbook -i production -vv site.yml -T 15 -D --tags=hosts
```

■オプション説明
?-i INVENTORY, --inventory-file=INVENTORY 
	?インベントリファイルを指定する(デフォルトは /etc/ansible/hosts)

?-D, --diff 
	?file や template の差分(diff)を表示する。--check と一緒に使うと便利

?-T TIMEOUT, --timeout=TIMEOUT 
	?SSH のタイムアウトを指定する(デフォルトは10秒)

?-C, --check 
	?インストールなどの変更は行わないが、条件の確認などは実行する

?-t TAGS, --tags=TAGS
	?指定の tag が付けられた task のみを実行する

?-U SUDO_USER, --sudo-user=SUDO_USER 
	?sudo での実行ユーザーを指定する(デフォルトは root)

?-v, --verbose
	?冗長モード (-vvv でより冗長な出力になる)

?--private-key=PRIVATE_KEY_FILE 
	?SSH の秘密鍵ファイルを指定する

?-f FORKS, --forks=FORKS 
	?並列実行する数(デフォルトは5)




■ディレクトリ説明

・hosts
	通称inventoryファイル
	ホストやグループを定義するファイル

・vars(group_vars)
	変数を定義する場所

・role
	サーバーの役割ごとにフォルダ分けして下記のファイルをまとめる場所
	機能ごとに作るか(zabbix,redmine)、サーバーごと(web,admin)に作るか悩みどころ

・taks
	各roleに必要な構成要素を用意する場所
	main.ymlから各要素をincludeするときれい

・handlers
	基本的にサービスの再起動などの操作を行うコマンドを配下のmain.ymlに記載する
	taskのnotifyでhandlersに通知を行う

・template
	設定ファイルを置く場所
	j2形式で置いておく


■ディレクトリ構造
作成中
