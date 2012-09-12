---
layout: default
title: vim-自动去BOM
published: true
category: vim
tags: [vim,去BOM]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p>－－－from &nbsp;&nbsp;http://vim.1045645.n5.nabble.com/utf8-BOM-td1171699.html<div><br></div><div>Q： &nbsp; &nbsp;I use utf8, and I would like to know how to save a file with BOM&nbsp;</div>1. always added
<br>2. always removed
<br>3. unchanged
<br>and what is the default behaviour of vim?
<br>thank in advance.&nbsp;<br><div><br></div><div><br></div><div>A： &nbsp;The default behaviour for existing files is to leave it unchanged. The&nbsp;</div>default for new files depends on the global setting of 'bomb' (which is 
<br>off by default, but I use
<br><br>&nbsp; &nbsp; &nbsp; &nbsp; setglobal bomb
<br><br>in my vimrc to make it on by default).
<br><br>To always add it, even on existing files:
<br><br>&nbsp; &nbsp; &nbsp; &nbsp; au BufReadPost setlocal bomb
<br><br>To always remove it, even on existing files:
<br><br>&nbsp; <font class="Apple-style-span" color="#F00000"><span class="Apple-style-span" style="font-size: x-large;">&nbsp; &nbsp; &nbsp; au BufReadPost setlocal nobomb
</span></font><br><br>The above autocommands allow you to change the setting manually for one 
<br>file and it will be saved that way -- unless you read that file again, 
<br>of course.
<br><br>Note that setting 'bomb' or 'nobomb' also sets 'modified'.
<br><br>To normally leave it unchanged you don't need to do anything, then you 
<br>can use ":setlocal bomb" or ":setlocal nobomb" to change it for the 
<br>current file. (Use ":setlocal" in that case, not ":set", to avoid 
<br>changing the default for new files).
<br><br>The 'bomb' setting has no effect when a file is saved in any 
<br>'fileencoding' other than utf-8, ucs-2, ucs-4, utf-16, utf-32 (and the 
<br>le and be variants of the latter four).
<br><br>see
<br>&nbsp; &nbsp; &nbsp; &nbsp; :help 'bomb'
<br>&nbsp; &nbsp; &nbsp; &nbsp; :help :setglobal
<br>&nbsp; &nbsp; &nbsp; &nbsp; :help :setlocal
<br>&nbsp; &nbsp; &nbsp; &nbsp; :help Unicode
<br>&nbsp; &nbsp; &nbsp; &nbsp; <a href="http://vim.wikia.org/wiki/Working_with_Unicode" target="_top" rel="nofollow" link="external" target="_blank">http://vim.wikia.org/wiki/Working_with_Unicode</a><br><br><br>Best regards,
<br>Tony.
<br>-- 
<br>Expense Accounts, n.:
<br>&nbsp; &nbsp; &nbsp; &nbsp; Corporate food stamps.&nbsp;<br><div><br></div><div>Just for the record, utf8 and hence its BOM is endian neutral.</div><div><br></div><div><br></div><div><br></div><div>With UTF-8, a BOM does not specify endianness but it does specify that 
<br>the file is in UTF-8 rather than UTF-16 or UTF-32. For instance, Windows 
<br>XP WordPad, which cannot _write_ Unicode files except in UTF-16le (with 
<br>BOM), can _read_ UTF-8 files if they have a BOM.
<br><br>Therefore, IMHO the appellation "BOM" (Byte Order Mark) is a misnomer; I 
<br>would have preferred "Unicode encoding marker" or some such. It can take 
<br>the following hex values:
<br><br>EF BB BF &nbsp; &nbsp; &nbsp; &nbsp;UTF-8
<br>FE FF &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; UTF-16be
<br>FF FE &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; UTF-16le
<br>00 00 FE FF &nbsp; &nbsp; UTF-32be
<br>FF FE 00 00 &nbsp; &nbsp; UTF-32le
<br><br>As can be seen, uniqueness assumes that UTF-16le files don't begin with 
<br>a NULL.
<br><br>Best regards,
<br>Tony.&nbsp;</div><div>&nbsp;</div><div><br></div><div><br></div><div>在vimrc中添加两行 &nbsp;</div><div>setglobal nobomb&nbsp;</div><div><span class="Apple-style-span" style="font-size: medium;">au BufReadPost setlocal nobomb &nbsp;&nbsp;</span><span class="Apple-style-span" style="font-size: medium; ">#vim打开的时候（读完buffer ）去bom</span></div><div><span class="Apple-style-span" style="font-size: medium; "><br></span></div><div><span class="Apple-style-span" style="font-size: medium;">只修改当前文件&nbsp;</span></div><div><span class="Apple-style-span" style="font-size: medium;">:setlocal nobomb &nbsp;</span></div><div><span class="Apple-style-span" style="font-size: medium;">或者</span></div><div><span class="Apple-style-span" style="font-size: medium;">:set nobomb</span></div></p></div>
