---
layout: default
title: 取消百度影音关联无扩展名文件
published: true
category: Windows
tags: [windows,百度影音,扩展名,关联]
---
<div id="detail" class="detail" style="line-height: 1.3;">
	首先强烈鄙视这种流氓行为! 除了不专业外还流氓， 满以为用百度可以搜索出来怎么解决， 结果无果还是G威武
	症状如这几个链接所说的一样：
	<ol>
		<li><a target="_blank" href="http://tieba.baidu.com/p/2048474665">http://tieba.baidu.com/p/2048474665</a></li>
		<li><a target="_blank" href="http://pcbbs.baidu.com/thread-127993-1-1.html">http://pcbbs.baidu.com/thread-127993-1-1.html</a></li>
		<li><a target="_blank" href="http://zhidao.baidu.com/question/1709635.html">http://zhidao.baidu.com/question/1709635.html</a></li>
		<li><a target="_blank" href="http://zhidao.baidu.com/question/544339833.html">http://zhidao.baidu.com/question/544339833.html</a></li>
	</ol>
	参考链接: <a target="_blank" href="http://superuser.com/questions/13653/how-to-set-the-default-program-for-opening-files-without-an-extension-in-windows">http://superuser.com/questions/13653/how-to-set-the-default-program-for-opening-files-without-an-extension-in-windows</a> 
	从中可以了解到无扩展名的文件对应的注册表关系是： [[HKEY_CLASSES_ROOT\.]]  但是没有找到相关项。  发现baiduplayer的关联是通过BaiduPlay.扩展名 项来关联的 删除相关项即可删除关联  因此只需删除[[HKEY_CLASSES_ROOT\BaiduPlay.]] 这个项即可 其实现在已经生效了 只是你看不到效果 重启系统或在任务管理器中结束explorer.exe进程 文件－新建任务 输入explorer.exe 确定即>
</div>