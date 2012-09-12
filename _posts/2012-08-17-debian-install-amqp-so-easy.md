---
layout: default
title: debian-安装amqp-so-easy
published: true
category: php
tags: [debian,安装amqp]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p><font size="4">检出源码：</font><div><font size="4"><br></font></div><div><font size="4">#&nbsp;<font color="#0000f0">sudo su -</font> &nbsp;(或su -切换到root用户下)</font></div><div><font size="4">#&nbsp;<font color="#0000f0">mkdir amqp</font></font></div><div><font size="4"># <font color="#0000f0">git clone&nbsp;git://github.com/alanxz/rabbitmq-c.git . </font>&nbsp; (注意最后有一个点 代表当前目录 )</font></div><div><font size="4"># <font color="#0000f0">git submodule init</font></font></div><div><font size="4"># <font color="#0000f0">git submodule update</font> &nbsp; (上一步初始化git子模块 这一步获取git子模块里的代码 &nbsp;获取的是codegen的代码)</font></div><div><font size="4">#<font color="#0000f0"> autoreconf -i &nbsp; &nbsp; &nbsp; &nbsp; </font>&nbsp; (autoreconf命令来源于autoconf包 所以你需要安装到有他 autoconf, automake, libtool这些都是编译软件常需要的 一同装上 &nbsp;#aptitude install autoconf automake libtool )</font></div><div><font size="4">#<font color="#0000f0"> ./configure &amp;&amp; make &amp;&amp; make install</font> &nbsp;(编译 安装)</font></div><div><font size="4"><br></font></div><div><font size="4"><br></font></div><div><font size="4">安装php扩展：</font></div><div><font size="4"># <font color="#0000f0">aptitude install php-pear php5-dev -y &nbsp;</font> &nbsp; &nbsp;(安装php-pear是为了使用pecl命令安装php扩展，php5-dev是因为安装amqp扩展需要使用到phpize这个命令 这个命令来源于php5-dev包)</font></div><div><font size="4"><br></font></div><div><font size="4"># <font color="#0000f0">pecl install amqp &nbsp;</font>(安装amqp扩展)</font></div><div><font size="4"># <font color="#0000f0">echo "extension=amqp.so" &gt; /etc/php5/conf.d/amqp.ini &nbsp;</font> (启用扩展)</font></div><div><font size="4"># &nbsp;<font color="#0000f0">service apache2 restart </font>&nbsp; (重启apache2) &nbsp;</font><span style="font-size: medium; ">通过执行 php --info |grep 'amqp' 来查看是否安装成功</span></div><div><font size="4"><br></font></div><div><font size="4"><br></font></div><div><font size="4">安装rabbitmq-server 服务端</font></div><div><font size="4">#<font color="#0000f0"> wget&nbsp;</font></font><span style="font-size: large; "><font color="#0000f0">&nbsp;</font></span><font size="4"><font color="#0000f0">http://www.rabbitmq.com/releases/rabbitmq-server/v2.8.5/rabbitmq-server_2.8.5-1_all.deb</font> &nbsp; &nbsp;</font><span style="font-size: large; ">(</span><span style="font-size: large; ">http://www.rabbitmq.com/download.html 点击Rabbitmq Server下面的 Quick Download &nbsp;》》Debian/Ubuntu 下载最新版）</span></div><div><font size="4"># <font color="#0000f0">dpkg -i&nbsp;rabbitmq-server_2.8.5-1_all.deb</font>&nbsp; &nbsp;(安装)</font></div><div><font size="4"><br></font></div><div><br></div></p></div>