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

### aws-code-build
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

phases:
  build:
    commands:
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
・・・
[Container] 2018/02/02 05:12:33 Running command echo Compiling the Python code...
Compiling the Python code...

[Container] 2018/02/02 05:12:33 Running command python helloworld.py
hello world!!!!

[Container] 2018/02/02 05:12:33 Phase complete: BUILD Success: true
[Container] 2018/02/02 05:12:33 Phase context status code: Message: 
[Container] 2018/02/02 05:12:33 Entering phase POST_BUILD
[Container] 2018/02/02 05:12:33 Running command echo Build completed on `date`
Build completed on Fri Feb 2 05:12:33 UTC 2018
・・・
```
```
