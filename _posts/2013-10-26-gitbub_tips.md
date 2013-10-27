---
layout: default
title: 建立github blog 注意项
permalink: github_tips.html
description: 搭建blog时遇到的一些问题
tags: "github" "blog"
---

**建立blog时的注意项**

* 对于 http://username.github.io 这样的网址，一个账户只能够建立一个，以及新建的Repository的名字必须为username.github.io，并且在主分支上建立。不设置_config.yml文件的baseurl属性。

* 对于 https://github.com/username/project 类似的网址，需要使用Repository的gh-pages分支，以及明确的设置baseurl属性，路径为Repository的名称。也可以用cname之类的设置网
页地址。

* 所有文件建议使用utf8编码，及注意使用无BOM格式编码
