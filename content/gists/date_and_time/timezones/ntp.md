---
title: "Check end enable ntp"
date: "2023-11-28T18:12:00+01:00"
tags: ["ntp", "time", "synchronization", "datetime"]
---
# Check and enable ntp

#### check status synchronization

```shell
timedatectl status

               Local time: вт 2023-11-28 18:02:40 CET
           Universal time: вт 2023-11-28 17:02:40 UTC
                 RTC time: вт 2023-11-28 17:02:32
                Time zone: Europe/Kiev (CET, +0200)
System clock synchronized: no
              NTP service: inactive
          RTC in local TZ: no
```

`System clock synchronized: no`



#### check service synchronization

```shell
systemctl status systemd-timesyncd.service

○ systemd-timesyncd.service - Network Time Synchronization
     Loaded: loaded (/usr/lib/systemd/system/systemd-timesyncd.service; disabled; preset: enabled)
     Active: inactive (dead)
       Docs: man:systemd-timesyncd.service(8)
```

#### enable synchronization
```shell
timedatectl set-ntp true
```

#### check service synchronization again

```shell
systemctl status systemd-timesyncd.service

● systemd-timesyncd.service - Network Time Synchronization
     Loaded: loaded (/usr/lib/systemd/system/systemd-timesyncd.service; enabled; preset: enabled)
     Active: active (running) since Tue 2023-11-28 18:03:29 CET; 2min 45s ago
       Docs: man:systemd-timesyncd.service(8)
   Main PID: 4163449 (systemd-timesyn)
     Status: "Contacted time server 162.159.200.123:123 (0.manjaro.pool.ntp.org)."
      Tasks: 2 (limit: 38344)
     Memory: 1.6M
        CPU: 78ms
     CGroup: /system.slice/systemd-timesyncd.service
             └─4163449 /usr/lib/systemd/systemd-timesyncd
```
