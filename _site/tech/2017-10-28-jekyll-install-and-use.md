# jekyll的安装使用

## 一、搭建环境

为了升级更快捷，搭建更方便，便于处理，需要依赖的软件包括：

>   rvm    #Ruby Version Manager,Ruby版本管理器，包括Ruby的版本管理和Gem库管理(gemset)。

###1.1 安装rvm

```
$ curl -L get.rvm.io | bash -s stable
$ source ~/.profile
```

验证是否安装正常

```
rvm  -v
```

###1.2 安装ruby

列出ruby可安装版本

```
rvm list known  
```

安装一个ruby版本

```
rvm install 2.4
```

查看已安装列表

```
rvm list
```

卸载ruby版本

```
rvm remove 2.4
```

切换 ruby版本

```
rvm use  2.4  #切换的版本均是已安装的版本
```



安装时可能出现的错误

```
Searching for binary rubies, this might take some time.
No binary rubies available for: osx/10.12/x86_64/ruby-2.4.1.
Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
Checking requirements for osx.
Installing requirements for osx.
Updating system - please wait
Installing required packages: autoconf, automake, libtool, pkg-config, coreutils, libyaml, libksba - please wait
There were package installation errors, make sure to read the log.

Try `brew tap --repair` and make sure `brew doctor` looks reasonable.

Check Homebrew requirements https://github.com/Homebrew/homebrew/wiki/Installation
Error running 'requirements_osx_brew_libs_install autoconf automake libtool pkg-config coreutils libyaml libksba',
please read /Users/zenyu/.rvm/log/1509172777_ruby-2.4.1/package_install_autoconf_automake_libtool_pkg-config_coreutils_libyaml_libksba.log
Requirements installation failed with status: 1.
```

运行`brew tap —repair` 后，再次安装ruby

```
brew tap --repair
```



参考链接 http://debugly.cn/script/2017/06/20/update-ruby-use-rvm.html

###1.3 更换源

查看已有的源

```
gem source -l
```

更换源

```
gem update --system
gem uninstall rubygems-update
gem sources -remove  http://ruby-china.org/ #移除旧源
gem sources -add  http://ruby-china.org/    # 添加新源
```



## 二、安装jekyll和建立blog

如果Ruby版本小于2.1的话，会报错，如下：

```
sudo gem install jekyll
Password:
YAML safe loading is not available. Please upgrade psych to a version that supports safe loading (>= 2.0).
ERROR:  SSL verification error at depth 1: unable to get local issuer certificate (20)
ERROR:  You must add /O=Digital Signature Trust Co./CN=DST Root CA X3 to your local trusted store
ERROR:  Error installing jekyll:
	public_suffix requires Ruby version >= 2.1.
```

如果不适用rvm安装的话，也会报错：

```
gem install jekyll
YAML safe loading is not available. Please upgrade psych to a version that supports safe loading (>= 2.0).
ERROR:  SSL verification error at depth 1: unable to get local issuer certificate (20)
ERROR:  You must add /O=Digital Signature Trust Co./CN=DST Root CA X3 to your local trusted store
ERROR:  While executing gem ... (Gem::FilePermissionError)
    You don't have write permissions for the /Library/Ruby/Gems/2.0.0 directory.
```

### 2.1 安装 jekyll

```
gem install jekyll
Fetching: public_suffix-3.0.0.gem (100%)
Successfully installed public_suffix-3.0.0
Fetching: addressable-2.5.2.gem (100%)
Successfully installed addressable-2.5.2
Fetching: colorator-1.1.0.gem (100%)
Successfully installed colorator-1.1.0
Fetching: rb-fsevent-0.10.2.gem (100%)
Successfully installed rb-fsevent-0.10.2
Fetching: ffi-1.9.18.gem (100%)
Building native extensions.  This could take a while...
Successfully installed ffi-1.9.18
Fetching: rb-inotify-0.9.10.gem (100%)
Successfully installed rb-inotify-0.9.10
Fetching: sass-listen-4.0.0.gem (100%)
Successfully installed sass-listen-4.0.0
Fetching: sass-3.5.3.gem (100%)
Successfully installed sass-3.5.3
Fetching: jekyll-sass-converter-1.5.0.gem (100%)
Successfully installed jekyll-sass-converter-1.5.0
Fetching: listen-3.0.8.gem (100%)
Successfully installed listen-3.0.8
Fetching: jekyll-watch-1.5.0.gem (100%)
Successfully installed jekyll-watch-1.5.0
Fetching: kramdown-1.15.0.gem (100%)
Successfully installed kramdown-1.15.0
Fetching: liquid-4.0.0.gem (100%)
Successfully installed liquid-4.0.0
Fetching: mercenary-0.3.6.gem (100%)
Successfully installed mercenary-0.3.6
Fetching: forwardable-extended-2.6.0.gem (100%)
Successfully installed forwardable-extended-2.6.0
Fetching: pathutil-0.16.0.gem (100%)
Successfully installed pathutil-0.16.0
Fetching: rouge-2.2.1.gem (100%)
Successfully installed rouge-2.2.1
Fetching: safe_yaml-1.0.4.gem (100%)
Successfully installed safe_yaml-1.0.4
Fetching: jekyll-3.6.2.gem (100%)
Successfully installed jekyll-3.6.2
Parsing documentation for public_suffix-3.0.0
Installing ri documentation for public_suffix-3.0.0
Parsing documentation for addressable-2.5.2
Installing ri documentation for addressable-2.5.2
Parsing documentation for colorator-1.1.0
Installing ri documentation for colorator-1.1.0
Parsing documentation for rb-fsevent-0.10.2
Installing ri documentation for rb-fsevent-0.10.2
Parsing documentation for ffi-1.9.18
Installing ri documentation for ffi-1.9.18
Parsing documentation for rb-inotify-0.9.10
Installing ri documentation for rb-inotify-0.9.10
Parsing documentation for sass-listen-4.0.0
Installing ri documentation for sass-listen-4.0.0
Parsing documentation for sass-3.5.3
Installing ri documentation for sass-3.5.3
Parsing documentation for jekyll-sass-converter-1.5.0
Installing ri documentation for jekyll-sass-converter-1.5.0
Parsing documentation for listen-3.0.8
Installing ri documentation for listen-3.0.8
Parsing documentation for jekyll-watch-1.5.0
Installing ri documentation for jekyll-watch-1.5.0
Parsing documentation for kramdown-1.15.0
Installing ri documentation for kramdown-1.15.0
Parsing documentation for liquid-4.0.0
Installing ri documentation for liquid-4.0.0
Parsing documentation for mercenary-0.3.6
Installing ri documentation for mercenary-0.3.6
Parsing documentation for forwardable-extended-2.6.0
Installing ri documentation for forwardable-extended-2.6.0
Parsing documentation for pathutil-0.16.0
Installing ri documentation for pathutil-0.16.0
Parsing documentation for rouge-2.2.1
Installing ri documentation for rouge-2.2.1
Parsing documentation for safe_yaml-1.0.4
Installing ri documentation for safe_yaml-1.0.4
Parsing documentation for jekyll-3.6.2
Installing ri documentation for jekyll-3.6.2
Done installing documentation for public_suffix, addressable, colorator, rb-fsevent, ffi, rb-inotify, sass-listen, sass, jekyll-sass-converter, listen, jekyll-watch, kramdown, liquid, mercenary, forwardable-extended, pathutil, rouge, safe_yaml, jekyll after 30 seconds
19 gems installed
```

检查安装是否成功

```
➜  ~ jekyll -v
jekyll 3.6.2
```

### 新建站点

```
jekyll new  blog-name
```

可能出现的错误

```
➜  Workspace jekyll new test2
Could not load Bundler. Bundle install skipped.
New jekyll site installed in /Users/zenyu/Workspace/test2.
```

可以在站点目录下，运行如下命令，修复问题：

```
$ gem install bundler
$ bundle install
$ bundle exec jekyll serve
```



```
## 博客生成，默认生成再_site目录下，当然也可以在配置文件中自定义
jekyll build
## 开启jekyll本地预览
jekyll server
```

