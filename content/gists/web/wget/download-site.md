---
title: "Download site by wget"
date: 2024-03-11T20:07:28+01:00
authors: ["pashamray"]
description: "download site"
tags: ["download", "wget", "site"]
---
for create a mirror site, you can use command:

```bash
wget --mirror --page-requisites --adjust-extension --convert-links --no-parent <URL>
```

```
  -m,  --mirror                    shortcut for -N -r -l inf --no-remove-listing
  -p,  --page-requisites           get all images, etc. needed to display HTML page
  -E,  --adjust-extension          save HTML/CSS documents with proper extensions
  -k,  --convert-links             make links in downloaded HTML or CSS point to local files
  -np, --no-parent                 don't ascend to the parent directory
```
