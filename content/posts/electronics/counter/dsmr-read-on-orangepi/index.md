+++
title = "dsmr-parser issue dependences on OrangePI"
date = 2025-09-15T20:11:00+01:00
authors = ["pashamray"]
description = "dsmr-parser issue dependences on OrangePI"
tags = ["OrangePI", "dsmr", "dsmr-parser", "dependences", "python", "pip"]
draft=false
+++

## Library

https://github.com/ndokter/dsmr_parser

A library for parsing Dutch Smart Meter Requirements (DSMR) telegram data. It also includes client implementation to directly read and parse smart meter data.

## Repository

I wrote reader base on examples 

```shell
git clone https://github.com/pashamray/dsmr-read.git
```

## Troble on OrangePI

```shell
pip install -r requirements.txt
```

And I had error, console output:

```shell
Collecting dsmr-parser==1.4.3 (from -r requirements.txt (line 1))
  Using cached dsmr_parser-1.4.3-py3-none-any.whl.metadata (539 bytes)
Collecting rich==14.1.0 (from -r requirements.txt (line 2))
  Using cached rich-14.1.0-py3-none-any.whl.metadata (18 kB)
Collecting pyserial<4,>=3 (from dsmr-parser==1.4.3->-r requirements.txt (line 1))
  Using cached pyserial-3.5-py2.py3-none-any.whl.metadata (1.6 kB)
Collecting pyserial-asyncio-fast>=0.11 (from dsmr-parser==1.4.3->-r requirements.txt (line 1))
  Using cached pyserial_asyncio_fast-0.16-py3-none-any.whl.metadata (2.5 kB)
Collecting pytz (from dsmr-parser==1.4.3->-r requirements.txt (line 1))
  Using cached pytz-2025.2-py2.py3-none-any.whl.metadata (22 kB)
Collecting Tailer==0.4.1 (from dsmr-parser==1.4.3->-r requirements.txt (line 1))
  Using cached tailer-0.4.1.tar.gz (7.5 kB)
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Collecting dlms_cosem==21.3.2 (from dsmr-parser==1.4.3->-r requirements.txt (line 1))
  Using cached dlms_cosem-21.3.2-py3-none-any.whl.metadata (10 kB)
Collecting markdown-it-py>=2.2.0 (from rich==14.1.0->-r requirements.txt (line 2))
  Using cached markdown_it_py-4.0.0-py3-none-any.whl.metadata (7.3 kB)
Collecting pygments<3.0.0,>=2.13.0 (from rich==14.1.0->-r requirements.txt (line 2))
  Using cached pygments-2.19.2-py3-none-any.whl.metadata (2.5 kB)
Collecting attrs>=20.3.0 (from dlms_cosem==21.3.2->dsmr-parser==1.4.3->-r requirements.txt (line 1))
  Using cached attrs-25.3.0-py3-none-any.whl.metadata (10 kB)
Collecting cryptography>=35.0.0 (from dlms_cosem==21.3.2->dsmr-parser==1.4.3->-r requirements.txt (line 1))
  Using cached cryptography-45.0.7.tar.gz (744 kB)
  Installing build dependencies ... error
  error: subprocess-exited-with-error

  × pip subprocess to install build dependencies did not run successfully.
  │ exit code: 1
  ╰─> [29 lines of output]
      Collecting maturin<2,>=1.8.6
        Using cached maturin-1.9.4.tar.gz (213 kB)
        Installing build dependencies: started
        Installing build dependencies: finished with status 'done'
        Getting requirements to build wheel: started
        Getting requirements to build wheel: finished with status 'done'
        Installing backend dependencies: started
        Installing backend dependencies: finished with status 'done'
        Preparing metadata (pyproject.toml): started
        Preparing metadata (pyproject.toml): finished with status 'error'
        error: subprocess-exited-with-error

        × Preparing metadata (pyproject.toml) did not run successfully.
        │ exit code: 1
        ╰─> [4 lines of output]
            Python reports SOABI: cpython-312-riscv64-linux-gnu
            Computed rustc target triple: riscv64-unknown-linux-gnu
            Target triple not supported by rustup: riscv64-unknown-linux-gnu
            Rust not found, installing into a temporary directory
            [end of output]

        note: This error originates from a subprocess, and is likely not a problem with pip.
      error: metadata-generation-failed

      × Encountered error while generating package metadata.
      ╰─> See above for output.

      note: This is an issue with the package mentioned above, not pip.
      hint: See above for details.
      [end of output]

  note: This error originates from a subprocess, and is likely not a problem with pip.
error: subprocess-exited-with-error

× pip subprocess to install build dependencies did not run successfully.
│ exit code: 1
╰─> See above for output.

note: This error originates from a subprocess, and is likely not a problem with pip.
```

## Fix

install build dependences for packages

```shell
sudo apt install rustc cargo build-essential libssl-dev pkg-config python3-dev libffi-dev
```

and try install requirements

```shell
pip install -r requirements.txt
```

console output

```shell
...
  Using cached cryptography-45.0.7.tar.gz (744 kB)
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Collecting asn1crypto>=1.4.0 (from dlms_cosem==21.3.2->dsmr-parser==1.4.3->-r requirements.txt (line 1))
  Downloading asn1crypto-1.5.1-py2.py3-none-any.whl.metadata (13 kB)
Collecting python-dateutil>=2.8.1 (from dlms_cosem==21.3.2->dsmr-parser==1.4.3->-r requirements.txt (line 1))
  Downloading python_dateutil-2.9.0.post0-py2.py3-none-any.whl.metadata (8.4 kB)
Collecting typing-extensions>=3.10 (from dlms_cosem==21.3.2->dsmr-parser==1.4.3->-r requirements.txt (line 1))
  Using cached typing_extensions-4.15.0-py3-none-any.whl.metadata (3.3 kB)
Collecting mdurl~=0.1 (from markdown-it-py>=2.2.0->rich==14.1.0->-r requirements.txt (line 2))
  Downloading mdurl-0.1.2-py3-none-any.whl.metadata (1.6 kB)
Collecting cffi>=1.14 (from cryptography>=35.0.0->dlms_cosem==21.3.2->dsmr-parser==1.4.3->-r requirements.txt (line 1))
  Using cached cffi-2.0.0-cp312-cp312-linux_riscv64.whl
Collecting six>=1.5 (from python-dateutil>=2.8.1->dlms_cosem==21.3.2->dsmr-parser==1.4.3->-r requirements.txt (line 1))
  Downloading six-1.17.0-py2.py3-none-any.whl.metadata (1.7 kB)
Collecting pycparser (from cffi>=1.14->cryptography>=35.0.0->dlms_cosem==21.3.2->dsmr-parser==1.4.3->-r requirements.txt (line 1))
  Using cached pycparser-2.23-py3-none-any.whl.metadata (993 bytes)
Downloading dsmr_parser-1.4.3-py3-none-any.whl (24 kB)
Downloading rich-14.1.0-py3-none-any.whl (243 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 243.4/243.4 kB 4.5 MB/s eta 0:00:00
Downloading dlms_cosem-21.3.2-py3-none-any.whl (128 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 128.8/128.8 kB 4.4 MB/s eta 0:00:00
Downloading markdown_it_py-4.0.0-py3-none-any.whl (87 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 87.3/87.3 kB 3.3 MB/s eta 0:00:00
Downloading pygments-2.19.2-py3-none-any.whl (1.2 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.2/1.2 MB 5.9 MB/s eta 0:00:00
Downloading pyserial-3.5-py2.py3-none-any.whl (90 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 90.6/90.6 kB 3.5 MB/s eta 0:00:00
Downloading pyserial_asyncio_fast-0.16-py3-none-any.whl (9.7 kB)
Downloading pytz-2025.2-py2.py3-none-any.whl (509 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 509.2/509.2 kB 5.6 MB/s eta 0:00:00
Downloading asn1crypto-1.5.1-py2.py3-none-any.whl (105 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 105.0/105.0 kB 3.8 MB/s eta 0:00:00
Downloading attrs-25.3.0-py3-none-any.whl (63 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 63.8/63.8 kB 2.6 MB/s eta 0:00:00
Downloading mdurl-0.1.2-py3-none-any.whl (10.0 kB)
Downloading python_dateutil-2.9.0.post0-py2.py3-none-any.whl (229 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 229.9/229.9 kB 4.6 MB/s eta 0:00:00
Using cached typing_extensions-4.15.0-py3-none-any.whl (44 kB)
Downloading six-1.17.0-py2.py3-none-any.whl (11 kB)
Using cached pycparser-2.23-py3-none-any.whl (118 kB)
Building wheels for collected packages: Tailer, cryptography
  Building wheel for Tailer (pyproject.toml) ... done
  Created wheel for Tailer: filename=tailer-0.4.1-py3-none-any.whl size=5482 sha256=f378f2cd2f22439991bc7e4b13397e4960614e5c8e16c11ebf3d0ae055f6acc7
  Stored in directory: /home/orangepi/.cache/pip/wheels/56/10/b3/9b55070a23f7689a4cde0d997e34884ee5d66a0255aa0d6a3f
  Building wheel for cryptography (pyproject.toml) ... done
  Created wheel for cryptography: filename=cryptography-45.0.7-cp312-abi3-linux_riscv64.whl size=4793837 sha256=155579580a3c01ebf61f1c8d7ac54cf636c6464dc90115af129ea42c1e75f7f8
  Stored in directory: /home/orangepi/.cache/pip/wheels/d9/16/48/4d74a7b28728ea12bbc1a20756b30c343c3985c0099943146f
Successfully built Tailer cryptography
Installing collected packages: Tailer, pytz, pyserial, asn1crypto, typing-extensions, six, pyserial-asyncio-fast, pygments, pycparser, mdurl, attrs, python-dateutil, markdown-it-py, cffi, rich, cryptography, dlms_cosem, dsmr-parser
Successfully installed Tailer-0.4.1 asn1crypto-1.5.1 attrs-25.3.0 cffi-2.0.0 cryptography-45.0.7 dlms_cosem-21.3.2 dsmr-parser-1.4.3 markdown-it-py-4.0.0 mdurl-0.1.2 pycparser-2.23 pygments-2.19.2 pyserial-3.5 pyserial-asyncio-fast-0.16 python-dateutil-2.9.0.post0 pytz-2025.2 rich-14.1.0 six-1.17.0 typing-extensions-4.15.0
```

Enjoy !
