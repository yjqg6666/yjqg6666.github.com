---
layout: default
title: Python-下异常的处理
published: true
category: python
tags: [python error except]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p><SPAN class=kn></SPAN><BR>
<DIV id=codeText class=codeText>
<P>&gt;&gt;&gt; while True:<BR>...&nbsp;&nbsp;&nbsp;&nbsp; try:<BR>...&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; x = int(raw_input("Please enter a number: "))<BR>...&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; break<BR>...&nbsp;&nbsp;&nbsp;&nbsp; except ValueError:<BR>...&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; print "Oops!&nbsp; That was no valid number.&nbsp; Try again..."<BR>...<BR></P>
<P>===========================example delimiter ==============</P>
<P>... except (RuntimeError, TypeError, NameError):<BR>...&nbsp;&nbsp;&nbsp;&nbsp; pass</P>
<P>===========================example delimiter ==============</P>
<P>import sys</P>
<P>try:<BR>&nbsp;&nbsp;&nbsp; f = open('myfile.txt')<BR>&nbsp;&nbsp;&nbsp; s = f.readline()<BR>&nbsp;&nbsp;&nbsp; i = int(s.strip())<BR>except IOError as (errno, strerror):<BR>&nbsp;&nbsp;&nbsp; print "I/O error({0}): {1}".format(errno, strerror)<BR>except ValueError:<BR>&nbsp;&nbsp;&nbsp; print "Could not convert data to an integer."<BR>except:<BR>&nbsp;&nbsp;&nbsp; print "Unexpected error:", sys.exc_info()[0]<BR>&nbsp;&nbsp;&nbsp; raise</P>
<P>===========================example delimiter ==============</P>
<P>for arg in sys.argv[1:]:<BR>&nbsp;&nbsp;&nbsp; try:<BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; f = open(arg, 'r')<BR>&nbsp;&nbsp;&nbsp; except IOError:<BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; print 'cannot open', arg<BR>&nbsp;&nbsp;&nbsp; else:<BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; print arg, 'has', len(f.readlines()), 'lines'<BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; f.close()<BR>===========================example delimiter ==============</P>
<P>&gt;&gt;&gt; try:<BR>...&nbsp;&nbsp;&nbsp; raise Exception('spam', 'eggs')<BR>... except Exception as inst:<BR>...&nbsp;&nbsp;&nbsp; print type(inst)&nbsp;&nbsp;&nbsp;&nbsp; # the exception instance<BR>...&nbsp;&nbsp;&nbsp; print inst.args&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # arguments stored in .args<BR>...&nbsp;&nbsp;&nbsp; print inst&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # __str__ allows args to printed directly<BR>...&nbsp;&nbsp;&nbsp; x, y = inst&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; # __getitem__ allows args to be unpacked directly<BR>...&nbsp;&nbsp;&nbsp; print 'x =', x<BR>...&nbsp;&nbsp;&nbsp; print 'y =', y<BR>...<BR>&lt;type 'exceptions.Exception'&gt;<BR>('spam', 'eggs')<BR>('spam', 'eggs')<BR>x = spam<BR>y = eggs<BR></P>
<P>===========================example delimiter ==============</P>
<P>&gt;&gt;&gt; try:<BR>...&nbsp;&nbsp;&nbsp; get_web(url)<BR>...&nbsp;except:<BR>...&nbsp;&nbsp;&nbsp; pass #任何错误都跳过&nbsp; </P></DIV></p></div>
