---
layout: default
title: php转换\\u(UNICODE)字符串为汉字
published: true
category: php
tags: [php,unicode,字符串,汉字]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p><div id="codeText" class="codeText"><ol style="margin:0 1px 0 0;padding:5px 0;" start="1" class="dp-css"><li>$test = '\u5e86\u91cd\u5e86'; //庆重庆<br></li><li>
$temp = explode('\u',$test); 拆分成数组<br></li><li>
$rslt = array();&nbsp; 保存结果的数组<br></li><li>
array_shift($temp); //去掉第一个不含数据的</li><li>
foreach($temp as $k =&gt; $v) { <br></li><li>
    $v = hexdec($v);&nbsp; //将16进制转换成十进制<br></li><li>
    $rslt[] = '&amp;#' . $v . ';'; //转换成html实体<br></li><li>
}</li><li>
$rslt = implode('',$rslt); //组合结果数组成字符串<br></li><li>
<br></li><li>
echo $rslt;</li><li><br></li></ol></div></p></div>
