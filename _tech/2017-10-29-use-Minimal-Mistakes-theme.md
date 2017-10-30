---
title: 使用Minimal Mistakes主题
layout: single
toc: true
---

为了测试主题的可用性，在本地安装Ruby，见[安装jekyll](zhatrix.com/tech/2017-10-28-jekyll-install-and-use/)

## 一 问题

这次由于不想直接替换掉之前的主题，以及想使用多个Collection存放文件导致在安装主题的时候一直不成功，浪费了很多时间，把过程中遇到的问题记录如下：

1.  看文档不够仔细
2.  目标不够明确，在安装的过程中经常变换注意力
3.  英语太差，理解不了具体的意思，在看到真是的案例后才明白

##  二 创建流程

由于创建博客时，对各个内容不了解，创建的步骤的较为复杂，这里一步步讲。

先看整个目录结构，知道整体架构后，修改部分内容调整为自己喜欢的样式。

对于新手来说，主要修改的地方，是``_config.yml`和 `_data/navigation.yml`,若是添加非默认的文章列表，不仅在config里添加新的内容，也需要在`_pages`添加与Collection对应的页面。

```
├── CNAME
├── Gemfile
├── Gemfile.lock
├── LICENSE.txt
├── README.md
├── Rakefile
├── _config.yml
├── _data
│   ├── navigation.yml
│   └── ui-text.yml
├── _drafts
│   └── crack_wifi.md
├── _includes
│   ├── analytics-providers
│   │   ├── custom.html
│   │   ├── google-universal.html
│   │   └── google.html
│   ├── analytics.html
│   ├── archive-single.html
│   ├── author-profile-custom-links.html
│   ├── author-profile.html
│   ├── base_path
│   ├── breadcrumbs.html
│   ├── browser-upgrade.html
│   ├── category-list.html
│   ├── comment.html
│   ├── comments-providers
│   │   ├── custom.html
│   │   ├── discourse.html
│   │   ├── disqus.html
│   │   ├── facebook.html
│   │   ├── google-plus.html
│   │   ├── scripts.html
│   │   ├── staticman.html
│   │   └── staticman_v2.html
│   ├── comments.html
│   ├── feature_row
│   ├── figure
│   ├── footer
│   │   └── custom.html
│   ├── footer.html
│   ├── gallery
│   ├── group-by-array
│   ├── head
│   │   └── custom.html
│   ├── head.html
│   ├── masthead.html
│   ├── nav_list
│   ├── page__hero.html
│   ├── page__hero_video.html
│   ├── page__taxonomy.html
│   ├── paginator.html
│   ├── post_pagination.html
│   ├── read-time.html
│   ├── scripts.html
│   ├── seo.html
│   ├── sidebar.html
│   ├── social-share.html
│   ├── tag-list.html
│   ├── toc
│   ├── toc.html
│   └── video
├── _layouts
│   ├── archive-taxonomy.html
│   ├── archive.html
│   ├── compress.html
│   ├── default.html
│   ├── home.html
│   ├── single.html
│   └── splash.html
├── _pages
│   ├── 404.md
│   ├── archive-layout-with-content.md
│   ├── category-archive.html
│   ├── collection-archive.html
│   ├── contact.md
│   ├── home.md
│   ├── lorem-ipsum.md
│   ├── page-a.md
│   ├── page-archive.html
│   ├── page-b.md
│   ├── portfolio-archive.html
│   ├── recipes-archive.html
│   ├── sample-page.md
│   ├── sitemap.md
│   ├── splash-page.md
│   ├── tag-archive.html
│   ├── tech-archive.html
│   ├── terms.md
│   └── year-archive.html
├── _posts
│   └── 2014-06-15-lovely-sentence.md
├── _sass
│   ├── minimal-mistakes
│   │   ├── _animations.scss
│   │   ├── _archive.scss
│   │   ├── _base.scss
│   │   ├── _buttons.scss
│   │   ├── _footer.scss
│   │   ├── _forms.scss
│   │   ├── _masthead.scss
│   │   ├── _mixins.scss
│   │   ├── _navigation.scss
│   │   ├── _notices.scss
│   │   ├── _page.scss
│   │   ├── _print.scss
│   │   ├── _reset.scss
│   │   ├── _sidebar.scss
│   │   ├── _syntax.scss
│   │   ├── _tables.scss
│   │   ├── _utilities.scss
│   │   ├── _variables.scss
│   │   ├── skins
│   │   │   ├── _air.scss
│   │   │   ├── _contrast.scss
│   │   │   ├── _dark.scss
│   │   │   ├── _default.scss
│   │   │   ├── _dirt.scss
│   │   │   ├── _mint.scss
│   │   │   └── _sunrise.scss
│   │   └── vendor
│   │       ├── breakpoint
│   │       │   ├── _breakpoint.scss
│   │       │   ├── _context.scss
│   │       │   ├── _helpers.scss
│   │       │   ├── _legacy-settings.scss
│   │       │   ├── _no-query.scss
│   │       │   ├── _parsers.scss
│   │       │   ├── _respond-to.scss
│   │       │   ├── _settings.scss
│   │       │   └── parsers
│   │       │       ├── _double.scss
│   │       │       ├── _query.scss
│   │       │       ├── _resolution.scss
│   │       │       ├── _single.scss
│   │       │       ├── _triple.scss
│   │       │       ├── double
│   │       │       │   ├── _default-pair.scss
│   │       │       │   ├── _default.scss
│   │       │       │   └── _double-string.scss
│   │       │       ├── resolution
│   │       │       │   └── _resolution.scss
│   │       │       ├── single
│   │       │       │   └── _default.scss
│   │       │       └── triple
│   │       │           └── _default.scss
│   │       ├── font-awesome
│   │       │   ├── _animated.scss
│   │       │   ├── _bordered-pulled.scss
│   │       │   ├── _core.scss
│   │       │   ├── _fixed-width.scss
│   │       │   ├── _font-awesome.scss
│   │       │   ├── _icons.scss
│   │       │   ├── _larger.scss
│   │       │   ├── _list.scss
│   │       │   ├── _mixins.scss
│   │       │   ├── _path.scss
│   │       │   ├── _rotated-flipped.scss
│   │       │   ├── _screen-reader.scss
│   │       │   ├── _stacked.scss
│   │       │   └── _variables.scss
│   │       ├── magnific-popup
│   │       │   ├── _magnific-popup.scss
│   │       │   └── _settings.scss
│   │       └── susy
│   │           ├── _su.scss
│   │           ├── _susy-prefix.scss
│   │           ├── _susy.scss
│   │           ├── plugins
│   │           │   ├── _svg-grid.scss
│   │           │   └── svg-grid
│   │           │       ├── _prefix.scss
│   │           │       ├── _svg-api.scss
│   │           │       ├── _svg-grid-math.scss
│   │           │       ├── _svg-settings.scss
│   │           │       ├── _svg-unprefix.scss
│   │           │       └── _svg-utilities.scss
│   │           └── susy
│   │               ├── _api.scss
│   │               ├── _normalize.scss
│   │               ├── _parse.scss
│   │               ├── _settings.scss
│   │               ├── _su-math.scss
│   │               ├── _su-validate.scss
│   │               ├── _syntax-helpers.scss
│   │               ├── _unprefix.scss
│   │               └── _utilities.scss
│   └── minimal-mistakes.scss
├── _site
│   ├── CNAME
│   ├── _pages
│   │   └── 404
│   │       └── index.html
│   ├── archive-layout-with-content
│   │   └── index.html
│   ├── assets
│   │   ├── css
│   │   │   └── main.css
│   │   ├── fonts
│   │   │   ├── FontAwesome.otf
│   │   │   ├── fontawesome-webfont.eot
│   │   │   ├── fontawesome-webfont.svg
│   │   │   ├── fontawesome-webfont.ttf
│   │   │   ├── fontawesome-webfont.woff
│   │   │   └── fontawesome-webfont.woff2
│   │   └── js
│   │       └── main.min.js
│   ├── banner.js
│   ├── categories
│   │   └── index.html
│   ├── collection-archive
│   │   └── index.html
│   ├── contact
│   │   └── index.html
│   ├── feed.xml
│   ├── index.html
│   ├── lorem-ipsum
│   │   └── index.html
│   ├── lovely-sentence
│   │   └── index.html
│   ├── minimal-mistakes-jekyll.gemspec
│   ├── page-a
│   │   └── index.html
│   ├── page-archive
│   │   └── index.html
│   ├── page-b
│   │   └── index.html
│   ├── portfolio
│   │   └── index.html
│   ├── recipes
│   │   └── index.html
│   ├── robots.txt
│   ├── sample-page
│   │   └── index.html
│   ├── sitemap
│   │   └── index.html
│   ├── sitemap.xml
│   ├── splash-page
│   │   └── index.html
│   ├── start
│   │   ├── favicon.png
│   │   ├── icon.png
│   │   ├── start.html
│   │   └── style.css
│   ├── staticman.yml
│   ├── tags
│   │   └── index.html
│   ├── tech
│   │   ├── 2013-10-26-gitbub-tips
│   │   │   └── index.html
│   │   ├── 2013-11-12-vim-tips
│   │   │   └── index.html
│   │   ├── 2014-06-10-vim-tutorial
│   │   │   └── index.html
│   │   ├── 2014-12-20-vba-password-crack
│   │   │   └── index.html
│   │   ├── 2015-01-23-nexus4-no-audio-bug-fix
│   │   │   └── index.html
│   │   ├── 2017-01-13-VBA-string-replace-and-modify-code
│   │   │   └── index.html
│   │   ├── 2017-10-28-homebrew-tips
│   │   │   └── index.html
│   │   ├── 2017-10-28-jekyll-install-and-use
│   │   │   └── index.html
│   │   └── 2017-10-29-use-Minimal-Mistakes-theme
│   │       └── index.html
│   ├── tech-archive
│   │   └── index.html
│   ├── terms
│   │   └── index.html
│   └── year-archive
│       └── index.html
├── _tech
│   ├── 2013-10-26-gitbub-tips.md
│   ├── 2013-11-12-vim-tips.md
│   ├── 2014-06-10-vim-tutorial.md
│   ├── 2014-12-20-vba-password-crack.md
│   ├── 2015-01-23-nexus4-no-audio-bug-fix.md
│   ├── 2017-01-13-VBA-string-replace-and-modify-code.md
│   ├── 2017-10-28-homebrew-tips.md
│   ├── 2017-10-28-jekyll-install-and-use.md
│   └── 2017-10-29-use-Minimal-Mistakes-theme.md
├── assets
│   ├── css
│   │   └── main.scss
│   ├── fonts
│   │   ├── FontAwesome.otf
│   │   ├── fontawesome-webfont.eot
│   │   ├── fontawesome-webfont.svg
│   │   ├── fontawesome-webfont.ttf
│   │   ├── fontawesome-webfont.woff
│   │   └── fontawesome-webfont.woff2
│   └── js
│       ├── _main.js
│       ├── main.min.js
│       ├── plugins
│       │   ├── jquery.fitvids.js
│       │   ├── jquery.greedy-navigation.js
│       │   ├── jquery.magnific-popup.js
│       │   └── jquery.smooth-scroll.min.js
│       └── vendor
│           └── jquery
│               └── jquery-3.2.1.min.js
├── banner.js
├── index.html
├── logo.png
├── minimal-mistakes-jekyll.gemspec
├── package.json
├── start
│   ├── favicon.png
│   ├── icon.png
│   ├── start.html
│   └── style.css
└── staticman.yml
```

### 2.1 确定导航

修改`_data/navigation.yml`，看里面的内容：

```
# example navigation
# main links
main:
  - title: "About"
    url: /about/
  - title: "Sample Posts"
    url: /year-archive/
  - title: "Sample Collections"
    url: /collection-archive/
```

可以自定义上侧导航栏，需要注意的是，url地址可以为固定地址，内部文件通过`permalink: `声明地址，通过pages对应的Collection文件夹生成的文章列表。

若是一个以前不存在的列表，需要在`_pages`新增一个页面，与url地址一致，展示所有该文件夹内的文件列表。

#### 新增文件夹

首先在`config.yml`建立一个collection

```
collections:
  tech:
    output: true
    permalink: /:collection/:path/
```

新增一个类型

```yml
# Defaults
defaults:
  # _tech
  - scope:
      path: ""
      type: tech
    values:
      layout: single
      author_profile: true
```



####问题

列表按照时间升序排列

```
{% capture written_year %}'None'{% endcapture %}
{% for post in site.tech reversed %}
  {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
  {% if year != written_year %}
    <h2 id="{{ year | slugify }}" class="archive__subtitle">{{ year }}</h2>
    {% capture written_year %}{{ year }}{% endcapture %}
  {% endif %}
  {% include archive-single.html %}
{% endfor %}
```

在site.tech后添加`reversed`倒序一下即可

还可以[自定义左侧边栏](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#custom-sidebar-navigation-menu)




需要注意的是，url对应的均为固定的链接，

若是普通的 Archive，Home，联系

### 2.2 更新的博客信息  

修改`config.yml`记录，调整用户信息和网站信息

站点信息

```
# Site Settings
locale                   : "en"
title                    : "学而时习"
title_separator          : "-"
name                     : "zHaTriX"
description              : "知识改变行动 行动塑造身体 身体即是模型 具身认知改变"
url                      : "http://zhatrix.com" 
```

作者信息，便于别人快速认识

```
# Site Author
author:
  name             : "张振玉"
  avatar           : # path of avatar image, e.g. "/assets/images/bio-photo.jpg"
  bio              : "6年通信工程师，2年互联网数据分析师，2年物流SAAS产品经理。"
  location         : "杭州,浙江"
  email            : "i@zhatrix.com"
  uri              : "zhatrix.com"
```





参考链接：

[mimimal - mistakes 官方博客] (https://mmistakes.github.io/minimal-mistakes/docs/navigation/)

# Changelog

20171030 张振玉：修改

20171029 张振玉：创建