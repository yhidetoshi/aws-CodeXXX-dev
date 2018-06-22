# aws-CodeXXX-dev
- aws CodeCommit
- aws CodeBuild
- aws CodePipline

を利用してみる。


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


