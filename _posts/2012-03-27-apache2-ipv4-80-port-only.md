---
layout: default
title: apache2-只监听ipv4的80端口
published: true
category: Linux
tags: [apache2,ipv4,80端口]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p>修改/etc/apache2/port.conf&nbsp; 的listen指令<br>Listen 80改为&nbsp; Listen 0.0.0.0:80<br><br><br>&lt;quote&gt;<br><p>When Apache starts, it binds to some port and address on
    the local machine and waits for incoming requests. By default,
    it listens to all addresses on the machine.  However, it may need to
    be told to listen on specific ports, or only on selected 
    addresses, or a combination of both. This is often combined with the 
    Virtual Host feature, which determines how Apache responds to 
    different IP addresses, hostnames and ports.</p>

    <p>The <a href="http://httpd.apache.org/docs/2.2/mod/mpm_common.html#listen" target="_blank">Listen</a>
    directive tells the server to accept
    incoming requests only on the specified ports or
    address-and-port combinations. If only a port number is
    specified in the <a href="http://httpd.apache.org/docs/2.2/mod/mpm_common.html#listen" target="_blank">Listen</a>
    directive, the server
    listens to the given port on all interfaces. If an IP address
    is given as well as a port, the server will listen on the given
    port and interface. Multiple <a href="http://httpd.apache.org/docs/2.2/mod/mpm_common.html#listen" target="_blank">Listen</a> directives may be used to
    specify a number of addresses and ports to listen on. The
    server will respond to requests from any of the listed
    addresses and ports.</p>

    <p>For example, to make the server accept connections on both
    port 80 and port 8000, on all interfaces, use:</p>

    <div class="example"><p>
      Listen 80<br>
      Listen 8000
    </p></div>

    <p>To make the server accept connections on port 80 for one interface,
       and port 8000 on another, use</p>

    <div class="example"><p>
      Listen 192.0.2.1:80<br>
      Listen 192.0.2.5:8000
    </p></div>

    <p>IPv6 addresses must be enclosed in square brackets, as in the
    following example:</p>

    <div class="example"><p>
      Listen [2001:db8::a00:20ff:fea7:ccea]:80 <br></p><p><br></p><a name="ipv6" id="ipv6">Special IPv6 Considerations</a><p><br></p><p>A growing number of platforms implement IPv6, and
    <a class="glossarylink" href="http://httpd.apache.org/docs/2.2/glossary.html#apr" title="see glossary">APR</a> supports IPv6 on most of these platforms,
    allowing Apache to allocate IPv6 sockets, and to handle requests sent 
    over IPv6.</p>

    <p>One complicating factor for Apache administrators is whether or
    not an IPv6 socket can handle both IPv4 connections and IPv6 
    connections.  Handling IPv4 connections with an IPv6 socket uses 
    IPv4-mapped IPv6 addresses, which are allowed by default on most 
    platforms, but are disallowed by default on FreeBSD, NetBSD, and 
    OpenBSD, in order to match the system-wide policy on those
    platforms. On systems where it is disallowed by default, a 
    special <a href="http://httpd.apache.org/docs/2.2/programs/configure.html" target="_blank">configure</a> parameter can change this behavior
    for Apache.</p>

    <p>On the other hand, on some platforms, such as Linux and Tru64, the 
    <strong>only</strong> way to handle both IPv6 and IPv4 is to use 
    mapped addresses. If you want Apache to handle IPv4 and IPv6 connections 
    with a minimum of sockets, which requires using IPv4-mapped IPv6 
    addresses, specify the --enable-v4-mapped <a href="http://httpd.apache.org/docs/2.2/programs/configure.html" target="_blank">configure</a> option.</p>

    <p>--enable-v4-mapped is the default on all platforms except 
    FreeBSD, NetBSD, and OpenBSD, so this is probably how your Apache was 
    built.</p>

    <p>I<font color="#F00000">f you want Apache to handle IPv4 connections only, regardless of 
    what your platform and APR will support, specify an IPv4 address on all 
    <a href="http://httpd.apache.org/docs/2.2/mod/mpm_common.html#listen" target="_blank">Listen</a> directives, as in the
    following examples:</font></p>

    <div class="example"><p>
      <font color="#F00000">Listen 0.0.0.0:80</font><br>
      Listen 192.0.2.1:80
    </p></div>

    <p><font color="#008080">If your platform supports it and you want Apache to handle IPv4 and 
    IPv6 connections on separate sockets (i.e., to disable IPv4-mapped 
    addresses), specify the --disable-v4-mapped <a href="http://httpd.apache.org/docs/2.2/programs/configure.html" target="_blank">configure</a> option. --disable-v4-mapped is the
    default on FreeBSD, NetBSD, and OpenBSD.</font></p></div><br>&lt;/quote&gt;<br></p></div>
