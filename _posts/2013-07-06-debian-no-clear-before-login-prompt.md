---
layout: default
title: debian在登录提示前不清屏
published: true
category: linux
tags: [linux,prompt,boot]
---
<div id="detail" class="detail" style="line-height: 1.3;">
	Reference link:
		http://forums.debian.net/viewtopic.php?f=17&t=104118<br />
	Search "/sbin/getty --noclear" ->
		http://www.raspberrypi.org/phpBB3/viewtopic.php?f=26&t=26052
		http://comments.gmane.org/gmane.linux.debian.user/433332
	and check manual page:
		<quote>
			Usage:
			 getty [options] line baud_rate,... [termtype]
			 getty [options] baud_rate,... line [termtype]

			Options:
			 -8, --8bits                assume 8-bit tty
			 -a, --autologin <user>     login the specified user automatically
			 -c, --noreset              do not reset control mode
			 -f, --issue-file <file>    display issue file
			 -h, --flow-control         enable hardware flow control
			 -H, --host <hostname>      specify login host
			 -i, --noissue              do not display issue file
			 -I, --init-string <string> set init string
			 -l, --login-program <file> specify login program
			 -L, --local-line           force local line
			 -m, --extract-baud         extract baud rate during connect
			 -n, --skip-login           do not prompt for login
			 -o, --login-options <opts> options that are passed to login
			 -p, --loginpause           wait for any key before the login
			 -R, --hangup               do virtually hangup on the tty
			 -s, --keep-baud            try to keep baud rate after break
			 -t, --timeout <number>     login process timeout
			 -U, --detect-case          detect uppercase terminal
			 -w, --wait-cr              wait carriage-return
				 --noclear              do not clear the screen before prompt
				 --nonewline            do not print a newline before issue
				 --no-hostname          no hostname at all will be shown
				 --long-hostname        show full qualified hostname
				 --version              output version information and exit
				 --help                 display this help and exit
		</quote>

		autologin can also achieved in this way.
		修改/etc/inittab文件中的第54行： 
		<pre>
			1:2345:respawn:/sbin/getty 38400 tty1
		</pre>
		改为：
		<pre>
			1:2345:respawn:/sbin/getty --noclear 38400 tty1
		</pre>
</div>