---
layout: default
title: 关闭IPV6的端口监听（apache2,exim4,git-daemon）
published: true
category: Linux
tags: [apache,exim4,git-daemon,关闭ipv6端口监听]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p>在root下使用netstat -tlnp查看开放的端口及使用的daemon <br><br><br>apache2:<br>&nbsp;#vim /etc/apache2/ports.conf<br>Listen 80&nbsp;&nbsp;&nbsp; ========&gt;&nbsp; Listen 0.0.0.0:80<br><br><br>exim4:<br>#vim /etc/exim4/update-exim4.conf.conf<br>dc_local_interfaces='127.0.0.1 ; ::1'&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ==========&gt; dc_local_interfaces='127.0.0.1'<br><br>git-daemon:<br>#vim /etc/sv/git-daemon/run<br>&nbsp;"$(git --exec-path)"/git-daemon --verbose --reuseaddr&nbsp; \&nbsp;&nbsp; ==========&gt; "$(git --exec-path)"/git-daemon --verbose --reuseaddr --listen=0.0.0.0 \&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <br><br></p></div>
