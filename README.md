---
title: README docker compose ACI
---

Docker ACI integration (Beta)を使って、.NET Core App + redis の docker compose をAzure Container Instance にup する。

ドキュメントは、この辺。[Deploying Docker containers on Azure(Beta)](https://docs.docker.com/engine/context/aci-integration/#prerequisites)

2.3.2.0 以降が必要。[Deploying Docker containers on Azure/Prerequisites](https://docs.docker.com/engine/context/aci-integration/#prerequisites)

6/25、[2.3.2.0](https://docs.docker.com/docker-for-windows/edge-release-notes/#docker-desktop-community-2320)で、**Beta release of the Docker ACI integration** 使えるようになった。

## 概要

最初に、azure にdocker cliで、azure login して、ACI コンテキストを作る。（予めリソースグループは作っておく）

```sh
docker login azure
docker context create aci mycontext
```

compose upする。自己署名証明書を上げずに、httpだけにしている。

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

クロスプラットフォーム(Mac, Windows, WSL2, Linux)で動くはず。

## TODO

- image の更新方法。down して、up すれば更新されるけど。コンテナグループの特定のコンテナだけ更新したい。
- このプログラムだと、redisがないと動かないので、compose の中でしか動かない。当たり前だけど面倒。
- Log Analytics、Application Insightsにログを送るサンプルを作る
- 自己署名証明書も上げた方がいいかのなと思うが、クロスプラットフォームで動くようにするのはどうするかを検討。
- .gitattributes で、lf にしたときの微妙な動きをどこかに書く
