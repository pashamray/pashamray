+++
title = "docker get container ip by name or by id"
date = 2022-06-22T08:12:38Z
authors = ["pashamray"]
description = "get container ip by name or by id"
tags = ["docker", "gist"]
draft=false
+++

```shell
# Узнать IP адрес контейнера
docker inspect --format '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' CONTAINER_ID_OR_NAME
```
