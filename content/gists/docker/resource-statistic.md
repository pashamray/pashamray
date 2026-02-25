---
title: "get docker resource statistic"
date: 2022-06-22T08:00:38Z
authors: ["pashamray"]
description: "get docker resource statistic"
tags: ["docker"]
---
```shell
# Статистика исрользования ресурсов 
docker stats --format 'table {{.Name}}\\t{{.CPUPerc}}\\t{{.MemUsage}}\\t{{.MemPerc}}'
```