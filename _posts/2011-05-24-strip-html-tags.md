---
layout: default
title: 用unhtml命令快速去html标签
published: true
category: Linux
tags: [html source,linux,html去标签]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p>此方法需安装unhtml包 直接将源文件作参数运行就可以去标签&nbsp; 除css样式去不掉外 其它标签都能去掉 整体还不错<br>example 1:<br><br>wget -O - "$(xsel -b)" | iconv -f GBK -t UTF-8 | unhtml | less<br><br>example 2:<br><br>wget -O - "http://www.google.com/ncr" | unhtml&nbsp; &gt;googleSourceWithoutTag<br></p></div>
