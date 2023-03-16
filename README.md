# Github Action: genova auto deploy

# 利用の方法
1. 対象のリポジトリにgithub action用のRepository Secret Keyとして `GENOVA_GITHUB_SECRET_KEY` を作成して下さい。
2. `.github/workflow/` 配下に下記内容のyamlファイルを配置して下さい。
```yaml
on:
  push:
    branches:
      - develop
    paths:
      - '/log_forwarder' # 変更を検出する特定のディレクトリを指定
jobs:
  genova_auto_deploy:
    runs-on: ubuntu-18.04
    steps:
      - name: genova metadata
        id: genova-metadata
        uses: metaps/action-genova@main
        with:
          app_domain: ***
          genova_github_secret_key: "${{ secrets.GENOVA_GITHUB_SECRET_KEY }}"
```


### Inputs

| input          | required | default                  | description                                         |
|----------------|----------|--------------------------|---------------------------|  
| `app_domain` |✔       |                   | 対象のアプリで稼働中のgenovaのドメインを指定します           |
| `genova_github_secret_key` |✔       |                   | Repository Secret Keyを指定します           |