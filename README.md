---
title: ACI docker compose
---

現状だと、2.3.2.0 以降が必要。[Deploying Docker containers on Azure/Prerequisites](https://docs.docker.com/engine/context/aci-integration/#prerequisites)

6/25の[2.3.2.0](https://docs.docker.com/docker-for-windows/edge-release-notes/#docker-desktop-community-2320)で、**Beta release of the Docker ACI integration** が落ちてきたので、普通に使えるようになった。

2.3.2.1 (46329) が落ちてきた。2020/6/30

## やり方

最初に、azure にdocker cliで、azure login して、ACI コンテキストを作る。

```sh
docker login azure
docker context create aci mycontext
```

compose upする

```sh
docker-compose -f ./docker-compose.yml -f ./docker-compose.override.yml build
docker-compose -f ./docker-compose.yml -f ./docker-compose.override.yml push
docker -c mycontext compose  -f ./docker-compose.yml -f ./docker-compose.override.yml up
```

動いているのを見る

```sh
docker -c mycontext ps
```

消す

```sh
docker -c mycontext compose down
```

## TODO

- image の更新方法。down して、up すれば更新されるけど。コンテナグループの特定のコンテナだけ更新したい。
- このプログラムだと、redisがないと動かないので、compose の中でしか動かない。当たり前だけど面倒。
- Log Analytics、Application Insightsにログを送るサンプルを作る
