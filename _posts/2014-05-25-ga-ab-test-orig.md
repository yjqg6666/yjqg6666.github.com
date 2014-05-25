---
layout: default
title: Linux下生成二维码[AB测试原文]
published: true
category: Linux
tags: [debian,二维码,生成图片]
---

<!-- Google Analytics Content Experiment code -->
<script>function utmx_section(){}function utmx(){}(function(){var k='63912626-0',d=document,l=d.location,c=d.cookie; if(l.search.indexOf('utm_expid='+k)>0)return; function f(n){if(c){var i=c.indexOf(n+'=');if(i>-1){var j=c.  indexOf(';',i);return escape(c.substring(i+n.length+1,j<0?c.  length:j))}}}var x=f('__utmx'),xx=f('__utmxx'),h=l.hash;d.write( '<sc'+'ript src="'+'http'+(l.protocol=='https:'?'s://ssl': '://www')+'.google-analytics.com/ga_exp.js?'+'utmxkey='+k+ '&utmx='+(x?x:'')+'&utmxx='+(xx?xx:'')+'&utmxtime='+new Date().  valueOf()+(h?'&utmxhash='+escape(h.substr(1)):'')+ '" type="text/javascript" charset="utf-8"><\/sc'+'ript>')})(); </script><script>utmx('url','A/B');</script>
<!-- End of Google Analytics Content Experiment code -->

<div id="detail" class="detail" style="line-height: 1.3;">
	1. 安装命令行工具： 
	<pre>
		bash#>>> apt-get install qrencode
	</pre>
	2. 生成图片
	<pre>
		bash$>>> qrencode -o /tmp/qrcode.png "string or url" 
	</pre>
	3. 如果需要经常生成二维码， 通过二维码在不同设置间复制内容时可以定义一个别名 (下面的别名会将剪贴板的内容生成二维码)
	<pre>
		bash$>>> alias qrmsg='qrencode -t png -o /tmp/qrcode.png `xsel -b` && xdg-open /tmp/qrcode.png' 
	</pre>
	4. 另外qrencode还支持生成字符串版的二维码， -t ascii即可 更多选项man qrencode
	5. 图形界面操作生成二维码， 安装qtqr运行即可
</div>