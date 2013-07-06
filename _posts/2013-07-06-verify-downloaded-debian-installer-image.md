---
layout: default
title: 验证下载的debian镜像是否为官方镜像
published: true
category: PHP
tags: [测试,curl,php,ip, host]
---
<div id="detail" class="detail" style="line-height: 1.3;">
	1. 下载：下载ftp目录下面跟iso同级的*.sign 和 *SUMS文件 
	2. 验证(以sha512sums为例)签名: 
	<pre>
		bash$>>>  gpg --verify SHA512SUMS.sign SHA512SUMS
	</pre>
	输出为：
	<quote>
		gpg: Signature made Sun 16 Jun 2013 09:30:18 PM UTC using RSA key ID 6294BE9B
		gpg: Can't check signature: public key not found
	</quote>
	添加公钥
	<pre>
		bash$>>> gpg --keyserver keyring.debian.org --recv-keys 6294BE9B
	</pre>
	输出为：
	<quote>
		gpg: requesting key 6294BE9B from hkp server keyring.debian.org
		gpg: $HOME/.gnupg/trustdb.gpg: trustdb created
		gpg: key 6294BE9B: public key "Debian CD signing key <debian-cd@lists.debian.org>" imported
		gpg: no ultimately trusted keys found
		gpg: Total number processed: 1
		gpg:               imported: 1  (RSA: 1)
	</quote>
	<pre>
		bash$>>> gpg --armor --export 6294BE9B |apt-key add -
	</pre>
	输出为：<quote>OK</quote>
	<pre>
		bash$>>>  gpg --verify SHA512SUMS.sign SHA512SUMS
	</pre>
	输出为：
	<quote>
			gpg: Signature made Sun 16 Jun 2013 09:30:17 PM UTC using RSA key ID 6294BE9B
			gpg: Good signature from "Debian CD signing key <debian-cd@lists.debian.org>"
			gpg: WARNING: This key is not certified with a trusted signature!
			gpg:          There is no indication that the signature belongs to the owner.
			Primary key fingerprint: DF9B 9C49 EAA9 2984 3258  9D76 DA87 E80D 6294 BE9B
	</quote>
	核对fingerprint地址(通常为最后几个cd为倒数3或4，dvd为倒数1，2)： <a target="_blank" href="http://www.debian.org/CD/verify">http://www.debian.org/CD/verify</a>
	3. 验证镜像(md5sum,sha256sum,sha512sum参数相同)
	<pre>
	bash$>>> sha512sum -c SHA512SUMS debian-7.1.0-amd64-i386-netinst.iso
	</pre>
	输出为：
	<quote>
		debian-7.1.0-amd64-i386-netinst.iso: OK
		sha512sum:      94 main/binary-amd64/Release: No such file or directory
		.....
	</quote>
	只需要第一行输出为ok 即为“正版” 否则。。。 你懂的
</div>