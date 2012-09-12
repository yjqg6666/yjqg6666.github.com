---
layout: default
title: python-提取items列表中只含小写字母和数字的项
published: true
category: python
tags: [python,列表,小写,数字,字母]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p><div id="codeText" class="codeText"><ol style="margin: 0pt 1px 0pt 0pt; padding: 5px 0pt;" start="1" class="dp-css"><li><span style="color:#000000;"><span style="color:#0000FF;">import</span> string<br></span></li><li>
limitation <span style="color:#0000CC;">=</span> list<span style="color:#0000CC;">(</span>string<span style="color:#0000CC;">.</span>ascii_lowercase <span style="color:#0000CC;">+</span> string<span style="color:#0000CC;">.</span>digits<span style="color: rgb(0, 0, 204);">) <br></span></li><li><div id="codeText" class="codeText"><ol style="margin:0 1px 0 0;padding:5px 0;" start="1" class="dp-css"><li><span style="color:#000000;"><span style="color:#FF00FF;">""</span><span style="color:#FF00FF;">"<br></span></span></li><li>&nbsp;&nbsp;&nbsp;
whitespace -- a string containing all ASCII whitespace<br></li><li>
&nbsp;&nbsp;&nbsp;&nbsp;ascii_lowercase -- a string containing all ASCII lowercase letters<br></li><li>
&nbsp;&nbsp;&nbsp;&nbsp;ascii_uppercase -- a string containing all ASCII uppercase letters<br></li><li>
&nbsp;&nbsp;&nbsp;&nbsp;ascii_letters -- a string containing all ASCII letters<br></li><li>
&nbsp;&nbsp;&nbsp;&nbsp;digits -- a string containing all ASCII decimal digits<br></li><li>
&nbsp;&nbsp;&nbsp;&nbsp;hexdigits -- a string containing all ASCII hexadecimal digits<br></li><li>
&nbsp;&nbsp;&nbsp;&nbsp;octdigits -- a string containing all ASCII octal digits<br></li><li>
&nbsp;&nbsp;&nbsp;&nbsp;punctuation -- a string containing all ASCII punctuation characters<br></li><li>
&nbsp;&nbsp;&nbsp;&nbsp;printable -- a string containing all ASCII characters considered printable<br></li><li>
"<span style="color:#FF00FF;">""</span></li></ol></div></li><li><span style="color: rgb(0, 0, 204);">items = ["aa", "aB", "a3", "中文", "BB"]</span></li><li><span style=" color: rgb(0, 0, 204);">tempItems = []<br></span></li><li><span style="color: rgb(0, 0, 204);">for item in items:</span></li><li><span style="color: rgb(0, 0, 204);">&nbsp;&nbsp;&nbsp;&nbsp; if len(item) == len([ i for i in item if i in limitation ]):</span></li><li><span style="color: rgb(0, 0, 204);">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; tempItems.append(item)</span></li><li>extractedItems = tempItems[0:]<br><span style="color: rgb(0, 0, 204);"></span></li><li><span style="color: rgb(0, 0, 204);">print(extractedItems)</span></li><li><span style="color: rgb(0, 0, 204);">#['aa', 'a3']</span></li></ol></div></p></div>
