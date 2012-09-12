---
layout: default
title: jquery-在ie6－8下无效果-在ie8下提示-object-doesn't-support-method-or-property
published: true
category: php
tags: [ie,support method]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p>报错的行是 : &nbsp;title=$(this).find('span a').html();<div>此行在非ie的浏览器上运行正常.<br><div>&nbsp;将title改为new_title问题解决</div></div><div><br></div><div>title为html语言中的 &nbsp;在ie运行的js中应避免使用属性和标签名作变量 &nbsp;</div></p></div>
