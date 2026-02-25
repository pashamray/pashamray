---
title: "generate ssh keys"
date: 2023-03-13T20:34:28+01:00
authors: ["pashamray"]
description: "генерация и корипование ssh ключей"
tags: ["ssh", "keys"]
---
Генерируем ключ
```shell
ssh-keygen -t ed25519 -b 4096 -C "name@example.com" -f ~/.ssh/my_key
```

вводим пароль для ключа
```shell
Generating public/private ed25519 key pair.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

наш ключ готов
```shell
Your identification has been saved in ~/.ssh/my_key
Your public key has been saved in ~/.ssh/my_key.pub
The key fingerprint is:
SHA256:YZNwKF/ExLQxXW5j+nnQo1v1CBcEGd65I5MDvK/pUYo name@example.com
The key's randomart image is:
+--[ED25519 256]--+
|      .BB. .++.  |
|    . .o+*.o.o . |
|     o .* o * +  |
|      .. o * + o |
|        S o O * .|
|         . = X =.|
|        E o = + .|
|           + +   |
|         .+ .    |
+----[SHA256]-----+
```

копируем наш ключ на сервер где `server_ip` ай-пи сервера куда копируем ключ
```shell
ssh-copy-id -i ~/.ssh/my_key.pub pashamray@server_ip
```

конфигурируем `.ssh/config`
```config
Host my_site
     HostName pashamray.site
     User pashamray
     IdentityFile ~/.ssh/my_key
     AddKeysToAgent yes
```

теперь можем подключаться
```shell
ssh my_site
```

или так, если скопировали ключи и для `root`
```shell
ssh root@my_site
```
