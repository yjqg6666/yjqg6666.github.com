---
layout: default
title: gnome-程序延时启动
published: true
category: Linux
tags: [延时启动,开机启动]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p>通过System-&gt;Preference-&gt;Startup Applications添加需要开机启动的程序 &nbsp;&nbsp;<div><br></div><div>我将icedove邮件管理端程序加成开机启动 &nbsp;但由于启动的时候网络连接（无线连接）还没有就绪 &nbsp; icedove会不断报错 无法连接到邮件服务器 &nbsp; 因此需要等无线连上以后才启动icedove &nbsp; 如果是系统管理员 &nbsp;可以添加到init.d中 其中有个优先级的数字 数字小的会最先启动 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 基于安全考虑 最好还是以普通用户启动 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;在用户目录下新建一个目录 &nbsp;</div><div>$mkdir ~/.bin</div><div>创建bash</div><div>$cat ~/.bin/delayed_icedove_start.bash</div><div>#!/bin/bash</div><div>sleep 15s</div><div>/usr/bin/icedove</div><div><br></div><div>$chmod +x &nbsp;~/.bin/delayed_icedove_start.bash</div><div><br></div><div>将~/.bin/delayed_icedove_start.bash添加到System-&gt;Preference-&gt;Startup Applications中</div><div><br></div><div><br></div><div>That's all, done.</div></p></div>
