# aws-CodeXXX-dev
- aws CodeCommit
- aws CodeBuild
- aws CodePipline

を利用してみる。

### aws-code-commit
- codecommitにリポジトリを作成
- SSHで接続するので
  - IAMユーザにsshの公開鍵を保存
  - .ssh/configに以下を追加
```
Host git-codecommit.*.amazonaws.com
  User <SSH-KEY-ID>
  IdentityFile ~/.ssh/<SECRET-KEY>
```

### パラメータストア
- パラメータストアにデータを格納
```
❯❯❯ aws ssm put-parameter --name "welcome" --type "String" --value "helloWorld"
{
    "Version": 1
}
```
- 格納したデータを確認
```
❯❯❯ aws ssm get-parameters --name welcome                                                    ✘ 2
{
    "Parameters": [
        {
            "Name": "welcome",
            "Type": "String",
            "Value": "helloWorld",
            "Version": 1
        }
    ],
    "InvalidParameters": []
}
```

## aws-code-build
- 実行環境
  - aws/codebuild/python:3.6.5 (コンテナイメージ)

- gitの構成
```
aws-code-build-test
├── buildspec.yml
└── helloworld.py

0 directories, 2 files
```

- 配置した `buildspec.yml` 
```
version: 0.2


env:
  parameter-store:
    hello: "welcome"

phases:
  build:
    commands:
      - echo ${hello}
      - echo Build started on `date`
      - echo Compiling the Python code...
      - python helloworld.py
  post_build:
    commands:
      - echo Build completed on `date`
artifacts:
  files:
    - helloworld.py
```

- ビルドログ
```
[Container] 2018/06/22 02:56:05 Running command echo ${hello}
helloWorld

[Container] 2018/06/22 02:56:05 Running command echo Build started on `date`
Build started on Fri Jun 22 02:56:05 UTC 2018

[Container] 2018/06/22 02:56:05 Running command echo Compiling the Python code...
Compiling the Python code...

[Container] 2018/06/22 02:56:05 Running command python helloworld.py
hello world!!!!
```
