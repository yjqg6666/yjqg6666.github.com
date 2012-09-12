---
layout: default
title: debian-aptitude-使用一段时间后读取数据库变慢的解决方法
published: true
category: Linux
tags: [aptitude,变慢]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p>dpkg tip

					<div class="entry-meta">
						<span class="meta-prep meta-prep-author">Posted on</span> <a href="http://antti-juhani.kaijanaho.fi/newblog/archives/521" title="14:04" rel="bookmark" target="_blank" target="_blank"><span class="entry-date">2009-05-02</span></a> <span class="meta-sep">by</span> <span class="author vcard"><a class="url fn n" href="http://antti-juhani.kaijanaho.fi/newblog/archives/author/antti-juhani-kaijanaho" title="View all posts by Antti-Juhani Kaijanaho">Antti-Juhani Kaijanaho</a></span>					</div>

					<div class="entry-content">
						<p>If your dpkg runs seem to take a long time in the “reading database” step, try this:</p><p>如果dpkg运行到读数据库这一步需要很长时间，试下这个：</p>
<p>Step One: Clear the available file dpkg --clear-avail</p><p>第一步： 清除可用的文件 &nbsp;dpkg --clear-avail</p>
<p>Step Two: Forget old unavailable packages dpkg --forget-old-unavail</p><p>第二步： 忘掉旧的无法获取的包 dpkg --forget-old-unavail</p>
<p>Step Three: If you use grep-available or other tools that rely on a useful available file, update the available file using sync-available (in the dctrl-tools package).</p><p>第三步： 如果你使用grep-available或其它的依赖于有用的可获得的文件（列表）的工具, &nbsp;使用sync-available(存在于dctrl-tools包中)更新可获得的文件（列表）</p>
<p>The few times I’ve tried it (all situations where the “reading 
database” step seemed to take ages), it has always sped the process up 
dramatically.  There probably are situations where it won’t make much 
difference, but I haven’t run into them.</p><p>我试了很多次（每回都是在‘读数据库’这一步都要花很长的时间）， 现在处理速度快多了。 也可能不会有多少变化， 我还没有试过。</p><p><br></p><p>－－－－－－－－－－－－－－－－－－－－－http://antti-juhani.kaijanaho.fi/newblog/archives/521</p><p><br></p><p>实际上只需要要用root执行（因为涉及到要处理/var/lib/dpkg/里面的文件 普通用户没权限操作里面的文件）&nbsp;</p><p>#dpkg --clear-avail &amp;&amp; dpkg --forget-old-unavail</p></div></p></div>
