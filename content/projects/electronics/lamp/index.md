+++

title = "lamp" 
date = 2023-12-18T19:28:28+01:00 
authors = ["pashamray"] 
description = "USB to UART module" 
tags = ["electronics", "CP2102", "USB", "UART", "USB to UART"] 
draft = true

+++

```bash
git clone https://github.com/openshwprojects/OpenBK7231T_App
```

ubuntu x64 install i386 support

```shell
sudo apt-get install libc6-i386
```

```
cd OpenBK7231T_App
make
cd ..
```

```
git clone https://github.com/OpenBekenIOT/hid_download_py
```

вставить переходник в USB и выполнить комманду
```
$ sudo dmesg | grep tty
[582007.392154] usb 1-3: cp210x converter now attached to ttyUSB0
```

```
sudo python uartprogram ../OpenBK7231T_App/output/dev_20231218_145713/OpenBK7231T_dev_20231218_145713.bin -d /dev/ttyUSB0 -w
```
