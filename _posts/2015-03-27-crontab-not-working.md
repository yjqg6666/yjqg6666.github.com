---
layout: default
title: crontab无效
published: true
category: Linux
tags: [crontab,定时,linux]
---
<div id="detail" class="detail" style="line-height: 1.3;">
	<div>
		$crontab -l  <br />
		0 18 * * * shutdown -h now <br />
		添加后无效 到点不执行 改成每2分钟执行一次也不执行 翻了man格式正确 <br />
		网上搜了下都是说cron(d)服务要必须开启 也确认了是运行中的 <br />
		$service cron status <br />
		cron is running <br />
		仍然没有自动执行  复制出来执行是没有问题的 确认不是typo  <br />
		<strong>网上搜到的结果中注意到都是写的全路径</strong> 我是直接写的命令 不含路径 <br />
		换成全路径执行正常了 <br />
		新加一条 <br />
		$crontab -l  <br />
		* * * * * echo $PATH >> /tmp/testlog <br />
		仍无输出 连echo也不行  <br />
		$whereis echo  <br />
		/bin/echo
		$crontab -l  <br />
		* * * * * /bin/echo $PATH > /tmp/testlog  <br />
		有内容输出到文件<br />
		$cat /tmp/testlog <br />
		/usr/bin:/bin <br />
		在路径中echo居然没有执行  具体的原因还不清楚  难道不是通过shell调用的
		没有使用$PATH <br />
		<strong>总结:</strong>
		在使用crontab调用脚本或命令的时候一定要使用<strong>绝对路径</strong>
	</div>
</div>