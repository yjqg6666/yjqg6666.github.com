---
layout: default
title: adb-devices-????????-no-permissions的问题
published: true
category: python
tags: [color,style]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p><font size="4"><span class="wpcpspCSS">＄adb devices&nbsp; <br></span></font><div id="codeText" class="codeText"><ol style="margin:0 1px 0 0;padding:5px 0;" start="1" class="dp-css"><li><span style="color:#000000;">???????? no permissions</span></li></ol></div>
＄lsusb<br><div id="codeText" class="codeText"><ol style="margin:0 1px 0 0;padding:5px 0;" start="1" class="dp-css"><li><span style="color:#000000;">Bus 001 Device 002: <span style="color:#FF0000;">ID</span> 0bb4:0c02 High Tech Computer Corp<span style="color:#0000CC;">.</span> Dream <span style="color:#0000CC;">/</span> ADP1 <span style="color:#0000CC;">/</span> G1 Phone <span style="color:#0000CC;">(</span>Debug<span style="color:#0000CC;">)</span></span></li></ol></div><br>是因为需要在/dev文件夹下生成文件 但当前用户在dev文件夹下生成文件的权限 切换成root 重启adb daemon&nbsp; <br><div id="codeText" class="codeText"><ol style="margin:0 1px 0 0;padding:5px 0;" start="1" class="dp-css"><li><span style="color:#000000;">$su -<br></span></li><li>
#cd <span style="color:#0000CC;">/</span>path<span style="color:#0000CC;">/</span>to<span style="color:#0000CC;">/</span>adb<br></li><li>
#adb kill-<span style="color:#0000FF;">server</span><br></li><li>
#adb <span style="color:#FF0000;">start</span><span style="color:#FF0000;">-</span><span style="color:#0000FF;">server</span><br></li><li>
#exit<br></li><li>
$adb devices</li></ol></div><br><br></p></div>
