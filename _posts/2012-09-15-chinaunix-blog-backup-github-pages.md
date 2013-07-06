---
layout: default
title: chinaunix博客备份
published: true
category: linux
tags: [chinaunix,博客,备份,github]
---
<div id="detail" class="detail" style="line-height: 1.3;">
    <ul>
        <li>
            获取博客用户id<br />
            访问博客首页  查看首页的链接 形如：http://blog.chinaunix.net/uid/<博客用户id>.html <br />
        </li>
        <li>
            下载备份脚本(需php环境)<br />
            下载zip压缩文件： https://github.com/yjqg6666/myconfig/zipball/master  解压文件 <br />
            Linux平台： cd 解压文件的位置 && cd cu2github && php conv.php <用户id>    <br />
            博客就会下载到_posts目录下   <br />
        </li>
        <li>
            获取博客里的附件   <br />
            在上一步的当前目录下 执行 ./get_attachment 将附件下载到attachment目录下 目录结构将与chinaunix上的一样 因此勿需修改博客内容内的地址 <br />
        </li>
    </ul>
</div>
