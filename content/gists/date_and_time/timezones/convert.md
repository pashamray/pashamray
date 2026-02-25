---
title: "конвертирование таймзон"
date: 2023-03-09T21:13:28+01:00
authors: ["pashamray"]
description: "underscore headers"
tags: ["nginx", "apache", "headers"]
---
###### переход на летнее время
```sql
SELECT CONVERT_TZ('2023-03-25 23:00:00', '+00:00', 'Europe/Kyiv'); # 2023-03-26 01:00:00
SELECT CONVERT_TZ('2023-03-26 00:00:00', '+00:00', 'Europe/Kyiv'); # 2023-03-26 02:00:00
SELECT CONVERT_TZ('2023-03-26 01:00:00', '+00:00', 'Europe/Kyiv'); # 2023-03-26 04:00:00
SELECT CONVERT_TZ('2023-03-26 02:00:00', '+00:00', 'Europe/Kyiv'); # 2023-03-26 05:00:00
SELECT CONVERT_TZ('2023-03-26 03:00:00', '+00:00', 'Europe/Kyiv'); # 2023-03-26 06:00:00
SELECT CONVERT_TZ('2023-03-26 04:00:00', '+00:00', 'Europe/Kyiv'); # 2023-03-26 07:00:00
```

###### переход на зимнее время
```sql
SELECT CONVERT_TZ('2023-10-28 23:00:00', '+00:00', 'Europe/Kyiv'); # 2023-10-29 02:00:00
SELECT CONVERT_TZ('2023-10-29 00:00:00', '+00:00', 'Europe/Kyiv'); # 2023-10-29 03:00:00
SELECT CONVERT_TZ('2023-10-29 01:00:00', '+00:00', 'Europe/Kyiv'); # 2023-10-29 03:00:00
SELECT CONVERT_TZ('2023-10-29 02:00:00', '+00:00', 'Europe/Kyiv'); # 2023-10-29 04:00:00
SELECT CONVERT_TZ('2023-10-29 03:00:00', '+00:00', 'Europe/Kyiv'); # 2023-10-29 05:00:00
SELECT CONVERT_TZ('2023-10-29 04:00:00', '+00:00', 'Europe/Kyiv'); # 2023-10-29 06:00:00
```