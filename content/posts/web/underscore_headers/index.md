---
title: "underscore headers"
date: 2023-03-04T21:07:28+01:00
authors: ["pashamray"]
description: "underscore headers"
tags: ["nginx", "apache", "headers"]
---
Веб сервера, такие как NGINX и Apache отбрасывают заголовки которые содержат в своем имени `_` (подчеркивание).

В документаций NGINX написано следующее:

> Missing (disappearing) HTTP Headers
> 
> If you do not explicitly set `underscores_in_headers on;`, NGINX will silently drop HTTP headers with underscores (which are perfectly valid according to the HTTP standard). This is done in order to prevent ambiguities when mapping headers to CGI variables as both dashes and underscores are mapped
> to underscores during that process.

В документаций Apache написано следующее:

> Passing broken headers to CGI scripts
> 
> Starting with version 2.4, Apache is more strict about how HTTP headers are converted to environment variables in `mod_cgi` and other modules: Previously any invalid characters in header names were simply translated to underscores. This allowed for some potential cross-site-scripting attacks via ?
> header injection (see [Unusual Web Bugs](http://events.ccc.de/congress/2007/Fahrplan/events/2212.en.html), slide 19/20).
> 
> If you have to support a client which sends broken headers and which can't be fixed, a simple workaround involving `mod_setenvif` and `mod_headers` allows you to still accept these headers:
> 
> ```config
> #
> # The following works around a client sending a broken Accept_Encoding
> # header.
> #
> SetEnvIfNoCase ^Accept.Encoding$ ^(.*)$ fix_accept_encoding=$1
> RequestHeader set Accept-Encoding %{fix_accept_encoding}e env=fix_accept_encoding
> ```



##### ссылки

https://www.nginx.com/resources/wiki/start/topics/tutorials/config_pitfalls/#missing-disappearing-http-headers

https://httpd.apache.org/docs/trunk/env.html#examples
