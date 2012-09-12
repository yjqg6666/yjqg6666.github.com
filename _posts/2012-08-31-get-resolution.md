---
layout: default
title: 获取当前显示的分辨率
published: true
category: Linux
tags: [linux,分辨率,查询]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p><div>It refers to the clarity of an image on screen. Screen resolution suggests the number of dots or pixels on the entire computer screen. For example, when you say a 640 x 480 screen resolution then all you means is individual 640 dots on each 480 lines i.e. 307K pixels.</div><div><br></div><div>Use xdpyinfo command to find out current screen resolution:</div><div><br></div><div>$<font color="#008080" size="4"> xdpyinfo &nbsp;| grep 'dimensions:'</font></div><div><br></div><div>dimensions: 800x600 pixels (283x212 millimeters)</div><div><br></div><div>You can also use xrandr command:</div><div><br></div><div>$<font color="#008080" size="4"> xrandr | grep '*'</font></div><div><br></div><div>*0 1024 x 768 ( 283mm x 212mm ) *61</div></p></div>
