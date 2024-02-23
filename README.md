# 新しいプロジェクトの作成環境
## AWS Cloud9にて、以下の設定で環境を作成した
- Environment type : EC2 instance
- Instance type : t2.micro
- Platform : Amazon Linux 2023
- Cost-saving setting : After 30 minutes
- 接続 : AWS Systems Manager(SSM)

## 新しいSpring Bootのアプリケーションを開始するために以下のコマンドを実行した
```
$ mkdir blog && cd blog
$ curl https://start.spring.io/starter.zip -d language=kotlin -d type=gradle-project-kotlin -d dependencies=web,mustache,jpa,h2,devtools -d packageName=com.example.blog -d name=Blog -o blog.zip
```

## githubとの連携を行った
github のverは2.40.1でした
1. ```ssh-keygen -t rsa```で公開鍵・秘密鍵の作成
2. GitHub上でSettings>SSH and GPG keysに行ってSSH公開鍵をGitHubに設定[^1]
3. vi ~/.ssh/configでサーバー側SSH設定と疎通確認を実施
   ```
   Host github
    HostName github.com
    IdentityFile ~/.ssh/id_rsa
    User git
   ```
5. SSH設定ファイルの権限を設定後、GItHubとの接続ができているか確認
   ```
   chmod 600 ~/.ssh/config
   ssh -T github
   ```
8. Gitコマンドの初期設定を実施
    ```
    $ git config --global user.name "GitHubのユーザ名"
    $ git config --global user.email "GitHubの登録アドレス"
    $ git config --global core.editor 'vim -c "set fenc=utf-8"'
    $ git config --global color.diff auto
    $ git config --global color.status auto
    $ git config --global color.branch auto
    ```
9. GitHubにリポジトリを作成
10. Cloud9上でblogプロジェクトに移動後、Gitの初期設定を実施
    ```
    cd /blog
    git init
    ```
12. 変更を保存
    ```
    git add .
    git commit -m "コメント"
    ```
14. リモートリポジトリを設定
    ```
    git remote add origin git@github.com:ユーザ名/リポジトリ名.git
    ```
16. リモートリポジトリへ反映
    ```
    git push origin master
    ```
[^1]:SSH公開鍵は、Cloud9のターミナル上で ```cat ~/.ssh/id_rsa.pub```を実行し、表示された内容をすべてkeyにコピペした
