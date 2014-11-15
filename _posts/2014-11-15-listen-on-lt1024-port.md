---
layout: default
title: 让普通用户可以在小于1024的端口下面监听
published: true
category: Linux
tags: [普通用户,1024,端口]
---
<div id="detail" class="detail" style="line-height: 1.3;">
	<div>
		<a href="https://stackoverflow.com/questions/413807/is-there-a-way-for-non-root-processes-to-bind-to-privileged-ports-1024-on-l">Reference#1</a>
		<a href="http://serverfault.com/questions/112795/how-can-i-run-a-server-on-linux-on-port-80-as-a-normal-user">Reference#2</a>
	</div>
	<div>
	<code>
		#setcap 'cap_net_bind_service=+ep' /path/to/program 
		注: 路径必须为真实文件 不能为链接
	</code>
		<quote>
			Okay, thanks to the people who pointed out the capabilities system and CAP_NET_BIND_SERVICE capability. If you have a recent kernel, it is indeed possible to use this to start a service as non-root but bind low ports. The short answer is that you do:

			setcap 'cap_net_bind_service=+ep' /path/to/program
			And then anytime program is executed thereafter it will have the CAP_NET_BIND_SERVICE capability. setcap is in the debian package libcap2-bin.

			Now for the caveats:

			You will need at least a 2.6.24 kernel
			This won't work if your file is a script. (ie, uses a #! line to launch an interpreter). In this case, as far I as understand, you'd have to apply the capability to the interpreter executable itself, which of course is a security nightmare, since any program using that interpreter will have the capability. I wasn't able to find any clean, easy way to work around this problem.
			Linux will disable LD_LIBRARY_PATH on any program that has elevated privileges like setcap or suid. So if your program uses its own .../lib/, you might have to look into another option like port forwarding.
		</quote>
	</div>
</div>