---
layout: default
title: python-自定义函数多返回值的处理
published: true
category: python
tags: [python,多个返回值]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p><div id="codeText" class="codeText"><ol style="margin:0 1px 0 0;padding:5px 0;" start="1" class="dp-css"><li><span style="color:#000000;"><span style="color:#0000FF;">def</span> getElement<span style="color:#0000CC;">(</span><span style="color:#0000CC;">)</span><span style="color:#0000CC;">:</span><br></span></li><li>
&nbsp;&nbsp;&nbsp;&nbsp;a <span style="color:#0000CC;">=</span> <span style="color:#FF00FF;">"first"</span><br></li><li>
&nbsp;&nbsp;&nbsp;&nbsp;b <span style="color:#0000CC;">=</span> <span style="color:#FF00FF;">"second"</span><br></li><li>
&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#0000FF;">return</span> a<span style="color:#0000CC;">,</span> b</li><li><br></li><li>
firstElement<span style="color:#0000CC;">,</span> secElement <span style="color:#0000CC;">=</span> getElement<span style="color:#0000CC;">(</span><span style="color:#0000CC;">)</span><br></li><li>
<br></li><li>
<span style="color:#0000FF;">print</span><span style="color:#0000CC;">(</span>firstElement<span style="color:#0000CC;">)</span>  #first<br></li><li>
<span style="color:#0000FF;">print</span><span style="color:#0000CC;">(</span>secElement<span style="color:#0000CC;">)</span> #second</li></ol></div></p></div>
