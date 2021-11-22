# Hinemos

## 説明
- 下記イメージ利用のためのdockercompose.yml及びdockerfileです。
  - [akatoan/hinemos-6.2-manager](https://hub.docker.com/r/akatoan/hinemos-6.2-manager)
  - [akatoan/hinemos-6.2-agent](https://hub.docker.com/r/akatoan/hinemos-6.2-agent)
  - [akatoan/hinemos-6.2-agent-win](https://hub.docker.com/r/akatoan/hinemos-6.2-agent-win)

## 使い方

### dockercompose.yml
1. dockercompose.ymlファイルをダウンロード
1. powershellの起動
1. work directoryの設定  
  `cd <dockercompose.yml格納ディレクトリ>`
1. docker-compose upの実行  
  `docker-compose -d`
  
### dockerfile
1. dockerfileのダウンロード
1. powershellの起動
1. docker buildの実行  
   `docker build -t <イメージ名>:<タグ> <dockerfileのパス>`

## 注意事項
- dockerfileを使ったbuildについて
  - dockerfileの中でローカルファイルのCOPYを実施しています  
    COPY対象ファイルは当リポジトリから予め取得し、各dockerfileと同ディレクトリに配置してください
    
## IPアドレスの変更について
- dockercompose.ymlの中でIPアドレスを設定しています  
  変更する場合は値を書き換えてください
- Hinemos ManagerのIPアドレスを変更する場合は、追加で下記の作業が必要です
  - Hinemos-6.2-Agent
    - Hinemos-6.2-Agentのdockerfile内のIPアドレス指定の変更  
      `HINEMOS_MANAGER=10.244.0.2`
    - dockerfileによるイメージのリビルド
  - Hinemos-6.2-Agent-Win
    - Hinemos-6.2-Agent-Winの設定ファイルAgent.properties内のIPアドレス指定の変更  
      `managerAddress=http://10.244.0.2:8081/HinemosWS/`
    - dockerfileによるイメージのリビルド
