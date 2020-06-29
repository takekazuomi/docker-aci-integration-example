---
title: ACI docker compose
---

```sh
docker-compose -f ./docker-compose.yml -f ./docker-compose.override.yml build
docker-compose -f ./docker-compose.yml -f ./docker-compose.override.yml push
docker -c mycontext compose  -f ./docker-compose.yml -f ./docker-compose.override.yml up
```

```sh
docker -c mycontext ps
```

## TODO

- image の更新方法。down して、up すれば更新されるけど。コンテナグループの特定のコンテナだけ更新したい。
- このプログラムだと、redisがないと動かないので、compose の中でしか動かない。当たり前だけど面倒。