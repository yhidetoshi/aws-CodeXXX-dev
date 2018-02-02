# aws-CodeXXX-dev
aws Code buildテスト用リポジトリ

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
