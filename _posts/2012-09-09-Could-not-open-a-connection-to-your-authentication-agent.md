---
layout: default
title: [转载]Could-not-open-a-connection-to-your-authentication-agent
published: true
category: Linux
tags: [ssh-keygen]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p>http://funkaoshi.com/blog/could-not-open-a-connection-to-your-authentication-agent<div class="vimiumReset vimiumHUD" style="right: 150px; opacity: 0; display: none; "></div><div><br></div><div><br></div><div><p><a href="http://en.wikipedia.org/wiki/Secure_Shell" target="_blank"><span class="caps">SSH</span></a>
 private-keys are usually stored encrypted on the computers they are 
stored on. A pass-phrase is used to decrypt them when they are to be 
used. Since most people use <a href="http://funkaoshi.com/blog/SSH" target="_blank"><span class="caps">SSH</span> public-private key-pairs to get around typing in passwords all the time</a>, the <a href="http://www.securityfocus.com/infocus/1812" target="_blank">ssh-agent</a>
 daemon exists to store decrypted private-keys you plan on using in a 
given session. The thing most people get tripped up on when using ssh-agent is that what the program outputs, some borne or csh shell commands, needs to be run. It may <em>look</em> like ssh-agent has set some variables for you, but it has in fact done no such thing. If you call ssh-add without processing ssh-agent’s
 output, it will complain it is unable to open a connection to your 
authentication agent. The most straightforward way to run ssh-agent on 
the command line is as follows: eval `ssh-agent`. After doing this, calls to ssh-add should succeed without error.</p><p><br></p><p>执行ssh-add ~/.ssh/rsa</p><p>&nbsp;报标题上的错误</p><p>先执行 &nbsp;eval `ssh-agent` &nbsp;（是～键上的那个`） 再执行 ssh-add ~/.ssh/rsa成功</p><p>ssh-add -l 就有新加的rsa了</p><p><span class="float_left"></span></p></div></p></div>
