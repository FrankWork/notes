参考资料：
https://www.mediawiki.org/wiki/Manual:Installing_MediaWiki

1 download mediawiki

$ wget https://releases.wikimedia.org/mediawiki/1.26/mediawiki-1.26.2.tar.gz
Alternatively, using cURL:
$ curl -O https://releases.wikimedia.org/mediawiki/1.26/mediawiki-1.26.2.tar.gz

2 untar

$ sudo cp mediawiki-*.tar.gz /usr/share/nginx/html/mediawiki-*.tar.gz
$ cd /usr/share/nginx/html/
$ sudo tar xvzf mediawiki-*.tar.gz
$ sudo mv xxx mediawiki

http://localhost/mediawiki
LocalSettings.php not found.
Please set up the wiki first.

http://localhost/mediawiki/mw-config/index.php
无法找到合适的数据库驱动！您需要为PHP安装数据库驱动。目前支持以下数据库类型：MySQL（或兼容程序）、PostgreSQL、Oracle、微软SQL服务器、SQLite。

如果您自己编译了PHP，请通过启用数据库客户端重新配置它，例如使用 ./configure --with-mysqli。如果您从 Debian 或 Ubuntu 安装包安装了PHP，那么您也需要安装，例如 php5-mysql 安装包。
警告：找不到APC、XCache或WinCache，无法启用对象缓存。
Object caching is not enabled.

找不到GD库或ImageMagick。缩略图功能将不可用。
发现Git版本控制软件：/usr/bin/git
使用服务器名“http://localhost”。
使用服务器URL“http://localhost/mediawiki”。
警告：因为尚未安装 intl PECL 扩展以处理 Unicode 正常化，故只能退而采用运行较慢的纯 PHP 实现的方法。
如果您运行着一个高流量的网站，请参阅 Unicode标准化一文。

环境检查已经完成。您不能安装MediaWiki。


Here’s the basic configuration used for the NGINX wiki.

server {
    server_name wiki.nginx.org;
    root /var/www/mediawiki;

    client_max_body_size 5m;
    client_body_timeout 60;

    location / {
        try_files $uri $uri/ @rewrite;
    }

    location @rewrite {
        rewrite ^/(.*)$ /index.php?title=$1&$args;
    }

    location ^~ /maintenance/ {
        return 403;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass unix:/tmp/phpfpm.sock;
    }

    location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
        try_files $uri /index.php;
        expires max;
        log_not_found off;
    }

    location = /_.gif {
        expires max;
        empty_gif;
    }

    location ^~ /cache/ {
        deny all;
    }

    location /dumps {
        root /var/www/mediawiki/local;
        autoindex on;
    }
}
Note
In order for this configuration to work, you will need to set “$wgUsePathInfo = TRUE;” in your LocalSettings.php file.

Installation continued[edit]
CREATE DATABASE wikidb;
GRANT ALL PRIVILEGES ON wikidb.* TO 'wikiuser'@'localhost' IDENTIFIED BY 'password';
If your database is not running on the same server as your web server, you need to give the appropriate web server hostname -- mediawiki.example.com in my example -- as follows:

GRANT ALL PRIVILEGES ON wikidb.* TO 'wikiuser'@'mediawiki.example.com' IDENTIFIED BY 'password';
Warning Warning: MySQL on UNIX/Linux logs all queries sent to it to a file, which will include the password you used for the user account. If this concerns you, delete your .mysql_history file after running these queries. This file may be found in your home directory (~/.mysql_history).




二．使用入门

1.       修改默认logo

mediawiki站点默认logo图片路径名：$WIKI_HOME/skins/common/images/wiki.png，可以通过以下两种方式修改默认logo:

(1)用图片编辑工作打开wiki.png图片，进行修改后覆盖即可；或者自己新建一个135 x 135像素，图片格式为.png的同名图片覆盖即可，建议使用透明背景，否则将严重影响视觉效果。

(2)将logo文件放在目录$WIKI_HOME/skins/common/images下，再在根目录下打开LocalSettings.php文件，找到$wgLogo= “$wgStylePath/common/images/wiki.png”，修改为$wglogo=”$wgStylePath/common/images/logo文件名”

注：可以使用默认logo图片同目录下的mediawiki.png替代。

2.       去除底部powered by图标

在配置文件LocalSettings.php中加入如下行即可，

unset($wgFooterIcons['poweredby']);

3.       修改皮肤

MediaWiki系统的默认皮肤是Vector，使用管理员账户登录后，可以通过”设置” -> “显示” –> “皮肤”预览所有皮肤效果，不过此处修改保存的话，只有在管理员账户登陆时才有效。

如要修改系统默认皮肤，要在根目录下打开配置文件LocalSettings.php，找到$wgDefaultSkin = 'vector';一行，如希望使用Modern皮肤，则改为$wgDefaultSkin='modern';

如想增加新皮肤，可下载皮肤插件保存到skins目录下，然后通过上述方法使用新皮肤。

4.       新建页面

如果搜索一个不存在的页面，会得到一个链接去创建新页面；也可以用wiki的URL创建新页，如想新建一个名为HelloWorld的页面，则可在地址栏输入：http://localhost/mediawiki/index.php/HelloWorld,在出现的页面中点击“创建”，输入内容后点击“保存页面”即可，如下图所示。


5.       页面格式化

可以通过使用wiki标记来格式化文本，下文描述了部分wiki标记，更多详情可查阅http://www.mediawiki.org/wiki/Help:Formatting

字符格式化

如，文本内容用两对单引号括起来(''italic'')可实现斜体效果，用三对单引号括起来('''bold''')可实现粗体效果，用strike标签括起来(<strike>strike</strike>)实现删除线效果；使用标签nowiki括起来则会忽略上述标记。

章节格式化

(1)标题

MediaWiki页面中的标题使用等号标记，用几对等号括起来则表示是几级标题。

== Level 2 ==

=== Level 3 ===

==== Level 4 ====

===== Level 5 =====

====== Level 6 ======

注: #1. 不建议用一对等号，它表示页面自身。#2. 页面中有4级及更多标题时，会自动生成目录。

(2)水平线

如果想在页面内容之间插入分割线，可在要分割的地方使用”----”，如下所示：

水平线之前

----

水平线之后

(3)无序列表

文本前加”*”号可以实现无序列表效果，”*”号的个数表示列表对应的级别，如

*1

**11

**12

*2

**21

**22

(4)有序列表

文本前加”#”号可以实现有序列表效果，”#”号的个数表示列表对应的级别，如

#1

##11

##12

#2

##21

##22

分段

MediaWiki不识别换行。要另起一段，需要使用一空行；在段落中可通过HTML标签<br/>强制换行。

HTML标签

在MediaWiki中允许使用部分HTML标签。如使用<u>标签实现下划线效果，<s>标签实现删除线效果等。

6.       链接

下文仅简要描述内部链接和外部链接的用法，更多信息可查阅http://www.mediawiki.org/wiki/Help:Links

内部链接

内部链接，即链接到wiki中其他页面的链接。将目标页面名使用两对方括号括起来表示一个内部链接(如[[HelloWorld]])。保存后，如链接指向的页面已存在，链接会显示为蓝色，否则显示为红色。

如果想将链接显示为文字信息，需使用格式[[页面名|文字]]，如[[HelloWorld|到HelloWorld页面]]。

外部链接

外部链接，即链接到其他网站的链接。输入网站地址并以空格结束，就可以生成一个外部链接。保存后，链接后会有一个箭头，表示指向外部。

如果想将链接显示为文字信息，需使用格式[外部网址文字]，如[http://www.baidu.com 百度]。

7.       分类

在页面中加入[[Category:分类名]]，会在页面底部生成分类链接，点击链接后可看到该分类下的所有页面。

8.       上传文件设定

配置文件LocalSettings中，$wgEnableUploads就是控制上传的参数，true允许，false不允许。

MediaWiki中允许上传的文件类型是有限制的，默认支持'png','gif', 'jpg', 'jpeg'这几种文件类型，对应的配置可参阅DefaultSettings.php中$wgFileExtensions的值；而不允许的文件类型在参数$wgFileBlacklist中设定。

登录后，可以通过导航栏或特殊页面中的上传文件链接上传文件。可使用[[File:文件名]]在页面中引用文件，如果引入的是图片文件，还可以指定图片宽度([[File:Example.jpg|200px]])，加入图片说明([[File:Example.jpg|图片1]])

9.       编辑器

MediaWiki自带的编辑器比较简单，用于页面编辑不太方便。从1.18版开始，MediaWiki中集成了一款增强型编辑器WikiEditor，在LocalSettings.php中加入如下行可启用WikiEditor，

$wgDefaultUserOptions['usebetatoolbar'] =1;

从1.21版本开始，MediaWiki默认集成了GeSHi(Generic Syntax Highlighter)插件，这是一款支持语法高亮显示的插件，借助<syntaxhighlight>标签可在页面中显示格式化的源码，还可以在此标签中使用参数”line”以显示代码行号，如下面的例子所示：

<syntaxhighlight lang="php"line>

<?php

   echo "Hello, World!";

?>

</syntaxhighlight>

10.   修改导航栏

通过wiki地址index.php/MediaWiki:Sidebar

如，http://localhost/mediawiki/index.php/MediaWiki:Sidebar，或者在搜索栏中输入“mediawiki:sidebar”，进入页面后点击编辑即可。

导航栏格式如下：

*导航栏名称一

**链接一地址|链接一名称

**链接二地址|链接二名称

 

*导航栏名称二

**链接一地址|链接一名称

**链接二地址|链接二名称

11.   查看MediaWiki版本

可通过选择"特殊页面" -> "数据与工具" -> "版本"，或者搜索"Special:Version"打开版本页面，在这个页面可以看到MediaWiki版本、PHP版本、Apache版本和所安装的扩展的版本等信息。

12.   用户组

MediaWiki中有3个用户组：机器人/管理员/行政员，每个用户组的具体权限可通过”特殊页面” -> “用户组权限”查看，通过首页中”创建用户”注册的用户默认不属于任何用户组；从属于行政员用户组的用户，可通过”特殊页面” -> “用户权限管理”给其他用户分配用户组。

13.   页面缓存

在配置文件DefaultSettings.php中，找到参数$wgCacheEpoch，将参数值置为当前时间，可以取消全部已经缓存的页面(包括客户端和服务器端)。
