---
title: ACI docker compose
---

```
docker-compose -f .\docker-compose.yml -f .\docker-compose.override.yml build
docker-compose -f .\docker-compose.yml -f .\docker-compose.override.yml push
docker -c mycontext compose  -f .\docker-compose.yml -f .\docker-compose.override.yml up
```

```
docker -c mycontext ps

```
