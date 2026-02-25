+++

title = "generate php docs"
date = 2023-03-04T21:07:28+01:00
authors = ["pashamray"]
description = "generate php docs"
tags = ["php", "docs", "phpdoc", "PlantUML"]
draft = true

+++

https://phpdoc.org/

```shell
docker run --rm -v "$(pwd):/data" "phpdoc/phpdoc:3" --target=docs/project --directory=project/app --setting "graphs.enabled=true"
```

```shell
phpDocumentor 3.4.2-v3.6.0+3172563

Parsing files

    1/5823 [>---------------------------]   0%
  583/5823 [==>-------------------------]  10%
 1165/5823 [=====>----------------------]  20%
 1747/5823 [========>-------------------]  30%
 2330/5823 [===========>----------------]  40%
 2912/5823 [==============>-------------]  50%
 3494/5823 [================>-----------]  60%
 4077/5823 [===================>--------]  70%
 4659/5823 [======================>-----]  80%
 5241/5823 [=========================>--]  90%
 5823/5823 [============================] 100%
Applying transformations (can take a while)
```
