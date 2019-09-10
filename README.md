# 事前作業

## sshキーの準備
sshキー作成
> ssh-keygen -t rsa -b 2048 -f ./kabuthon/id_rsa
> ssh-keygen -t rsa -b 2048 -f ./rundeck/data/.ssh/id_rsa

- Rundeckで使うsshキーがopen-ssh形式の場合はrsa形式に変更しないとジョブが実行できない
> ssh-keygen -p -f ./rundeck/data/.ssh/id_rsa -t rsa -m PEM

## Rundeckからジョブの実行環境へ入れるようにする
> cat rundeck/id_rsa.pub >> kabuthon/authorized_keys

公開鍵をgithubに登録
https://github.com/settings/keys


## コンテナ起動
> docker-compose build
> docker-compose up


## Rundeckにログイン
1. 以下のページにアクセス    
   1. http://127.0.0.1:4440/
   2. 初期のログイン情報はユーザ名: admin, パスワード: admin
2. プロジェクトを作成
   1. 適当な名前でプロジェクトを作成
3. ジョブ実行ノードの追加    
   1. "http://127.0.0.1:4440/project/kabuthon/nodes/sources"にアクセス
   2. "Add a new Node Source" -> "File"を選択
   3. formatにresource.xmlを選択
   4. ファイルパスに"/home/rundeck/projects/kabuthon/etc/resources.xml"ウォン選択
   5. Saveをクリック
4. ジョブの追加
