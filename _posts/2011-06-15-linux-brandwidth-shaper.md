---
layout: default
title: linux-下对单个程序网络限速brandwidth-shaper
published: true
category: Linux
tags: [linux,限网速,单个程序,进程]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p>windows下对单个程序限速 可以使用netlimiter <br><br><br>Linux可选软件(任一):&nbsp; pyshaper&nbsp;&nbsp;&nbsp; shaperd&nbsp;&nbsp;&nbsp; wondershaper trickle<br><br>pyshaper squeeze库中没有 没用过 <br>最后三个库中都有<br><br>最简单的是trickle 其余的还没研究（先实现功能要紧）<br><br>trickle -u 10 -d 20 iceweasel 启动火狐浏览器 并限制上传速度为10 KB/s 下速度为20 KB/s 
（在没trickled运行的情况下 使用trickle要加上 -s 参数&nbsp; 不然会报错： trickle: Could not reach 
trickled, working independently: No such file or directory）<br>
<br>
测试情况：<br>
$trickle -s -d 40 -u 5 axel http://192.168.0.111/video.flv &nbsp; &nbsp;(.111是本机ip)<br>
输出:<br><div>[ &nbsp;0%] &nbsp;.......... .......... .......... .......... .......... &nbsp;[ &nbsp;38.7KB/s]</div><div>[ &nbsp;0%] &nbsp;.......... .......... .......... .......... .......... &nbsp;[ &nbsp;39.4KB/s]</div><div>[ &nbsp;0%] &nbsp;.......... .......... .......... .......... .......... &nbsp;[ &nbsp;39.5KB/s]</div><div>[ &nbsp;0%] &nbsp;.......... .......... .......... .......... .......... &nbsp;[ &nbsp;39.7KB/s]</div><div>[ &nbsp;0%] &nbsp;.......... .......... .......... .......... .......... &nbsp;[ &nbsp;39.3KB/s]</div>
（其余部分省略）<div>Downloaded 162.2 megabytes in 1:09:42 seconds. (39.70 KB/s)</div><div><br>
$axel http://192.168.0.111/video.flv<br>
输出:<br>
[&nbsp; 0%]&nbsp; .......... .......... .......... .......... ..........&nbsp; [ 596.4KB/s]<br>
[&nbsp; 0%]&nbsp; .......... .......... .......... .......... ..........&nbsp; [1187.5KB/s]<br>
[&nbsp; 0%]&nbsp; .......... .......... .......... .......... ..........&nbsp; [1579.0KB/s]<br>
[&nbsp; 0%]&nbsp; .......... .......... .......... .......... ..........&nbsp; [2160.9KB/s]<br>
[&nbsp; 0%]&nbsp; .......... .......... .......... .......... ..........&nbsp; [2546.5KB/s]<br>
[&nbsp; 0%]&nbsp; .......... .......... .......... .......... ..........&nbsp; [3123.1KB/s]<br>
[&nbsp; 0%]&nbsp; .......... .......... .......... .......... ..........&nbsp; [3506.5KB/s]<br>（其余部分省略）</div><div><div>Downloaded 162.2 megabytes in 5 seconds. (31446.71 KB/s)</div><div><br></div><br>wondershaper的使用说明参考&nbsp; /usr/share/doc/wondershaper/README.Debian.gz或/usr/share/doc/wondershaper/README.gz<br><br><br><br>另外在个别论坛有人推荐用 tc 或nc（系统都自带） 前面的都是运行在user－space的 tc是在kernel上&nbsp; nc还不晓得 &nbsp; 由于更复杂更没时间研究了&nbsp;&nbsp; BTW&nbsp;&nbsp; linux中的软件或命令 名字短的通常都是超级牛力&nbsp; 有时间看看man会受益菲浅<br><br>iptables 也可限速 目前我只知道可以对整个网速或对单个ip限速<br></div></p></div>
