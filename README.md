# aws-code-build-test
aws Code buildテスト用リポジトリ

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
