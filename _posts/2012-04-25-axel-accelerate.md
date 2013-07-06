---
layout: default
title: 修改连接数-加速axel下
published: true
category: linux
tags: [Linux,axel,下,加速,迅雷]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p>使用root用户(sudo也一样)修改配置文件 /etc/axelrc<div>在尾部添加如下三行</div><div><br></div><div>## Customized</div><div><div>alternate_output=1 &nbsp;#使用类似于wget的进度显示</div><div>num_connections=10 &nbsp;#设置连接数为10</div></div><div><br></div></p></div>
