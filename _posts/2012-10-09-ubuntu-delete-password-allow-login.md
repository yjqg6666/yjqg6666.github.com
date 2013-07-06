---
layout: default
title: Ubuntu清空密码并允许空密码登录 
published: true
category: linux
tags: [ubunt,清空密码,空密码登录]
---
<div id="detail" class="detail" style="line-height: 1.3;">

<quote>
[转载](http://ubuntuforums.org/showthread.php?t=819198 "先转载有时间的时候翻译")
</quote>
# 清空密码 #
<code>
$sudo su - //切换到root
</code>
<code>
#passwd --delete <要清空密码的用户名> //清空密码
</code>
# 允许空密码登录 #
<code>
#sed -i 's/nullok_secure/nullok/' /etc/pam.d/common-auth //允许空密码登录
</code>
<code>
#sed -i 's/#PasswordRequired=false/PasswordRequired=false/' /etc/gdm/gdm.conf  //图形界面允许空密码登录 
</code>
</div>
