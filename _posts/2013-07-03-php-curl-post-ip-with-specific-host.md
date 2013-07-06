---
layout: default
title: PHP-curl提交到未做dns解析的域名ip
published: true
category: PHP
tags: [测试,curl,php,ip, host]
---
<div id="detail" class="detail" style="line-height: 1.3;">
	<pre>
		php>> $ch = curl_init();
		php>> curl_setopt($ch, CURLOPT_POST, true);
		php>> curl_setopt($ch, CURLOPT_POSTFIELDS, array('a'=>'b','c'));
		php>> curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
		php>> curl_setopt($ch, CURLOPT_HTTPHEADER, array('Host: 5t.zhubajie.cn'));
		php>> curl_setopt($ch, CURLOPT_URL, 'http://127.0.0.1/t.php');
		php>> $rsa = curl_exec($ch);
		php>> if ($rsa === false) echo 'error:' . curl_error($ch) . ',code:' . curl_errno($ch);
		php>> curl_close($ch);
	</pre>
或者
	<pre>
		php>> $ch = curl_init('http://127.0.0.1/t.php');
		php>> curl_setopt_array($ch, array(
			CURLOPT_POSTFIELDS=> array('a'=>'b','c'),
			CURLOPT_RETURNTRANSFER=> true,
			CURLOPT_HTTPHEADER=> array('Host: 5t.zhubajie.cn')
		));
		php>> $rsa = curl_exec($ch);
		php>> if ($rsa === false) echo 'error:' . curl_error($ch) . ',code:' . curl_errno($ch);
		php>> curl_close($ch);
	</pre>
</div>