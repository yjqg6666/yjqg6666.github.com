---
layout: default
title: 非官方xdebug配置文件
published: true
category: Linux
tags: [xdebug,配置,参数]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p>[xdebug]
<p>;;;;;;;;;;;;;;;;;;;<br>
; About this file ;<br>
;;;;;;;;;;;;;;;;;;;<br>
;<br>
; built by G. Giunta as a verbatim copy of info from xedbug website on 2007/11/08</p>
<p>; You must uncomment one (and only one) line from the following to load<br>
; the xdebug extension.<br>
zend_extension="/usr/lib/<a href="http://en.wikipedia.org/wiki/PHP" class="ml-smartlink" target="_blank">php4</a>/xdebug.so"<br>
;zend_extension_ts="/usr/lib/php4/xdebug.so"<br>
;zend_extension_ts="c:\php4\xdebug.dll"<br>
;zend_extension="c:\php4\xdebug.dll"</p><p>;;;;zend_extension 指令可以是以下之一：{</p><p>;;  zend_extension (non ZTS, non <a href="http://en.wikipedia.org/wiki/Debugging" class="ml-smartlink" target="_blank">debug</a> build)<span></span></p><p><span>;;  zend_extension_ts ( ZTS, non debug build)</span><br></p><p>;; zend_extension_debug (non ZTS, <a href="http://en.wikipedia.org/wiki/Debugging" class="ml-smartlink" target="_blank">debug</a> build)<br></p><span>;; zend_extension_debug_ts (ZTS, debug build)<br>;; ZTS &nbsp; MEANS &nbsp;&nbsp; ZEND Thread Safety<br><br>;;&nbsp;&nbsp; }</span><strong><span> </span></strong><strong><strong><span></span> </strong></strong><strong><strong></strong>

</strong>
<p>; When this setting is set to on, the tracing of function calls will be enabled<br>
; just before the script is run. This makes it possible to trace code in the<br>
; auto_prepend_file.<br>
xdebug.auto_trace=Off</p>
<p>; This setting, defaulting to On, controls whether Xdebug should write the<br>
; filename used in include(), include_once(), require() or require_once() to<br>
; the trace files.<br>
xdebug.collect_includes=On</p>
<p>; This setting, defaulting to 0, controls whether Xdebug should collect the<br>
; parameters passed to functions when a function call is recorded in either the<br>
; function trace or the <a href="http://en.wikipedia.org/wiki/Stack_trace" class="ml-smartlink" target="_blank">stack trace</a>.<br>
; The setting defaults to Off because for very large scripts it may use huge<br>
; amounts of memory and therefore make it impossible for the huge script to run.<br>
; You can most safely turn this setting on, but you can expect some problems in<br>
; scripts with a lot of function calls and/or huge data structures as parameters.<br>
; Xdebug 2 will not have this problem with increased memory usage, as it will<br>
; never store this information in memory. Instead it will only be written to disk.<br>
; This means that you need to have a look at the disk usage though.<br>
; This setting can have four different values. For each of the values a different<br>
; amount of information is shown. Below you will see what information each of the<br>
; values provides. See also the introduction of the feature Stack Traces for a<br>
; few screenshots.<br>
; Value Argument Information Shown<br>
; 0     None.<br>
; 1     Type and number of elements (f.e. string(6), array(8)).<br>
; 2     Type and number of elements, with a tool tip for the full information.<br>
; 3     Full variable contents (with the limits respected as set by<br>
;           xdebug.var_display_max_children, xdebug.var_display_max_data and<br>
;           xdebug.var_display_max_depth.<br>
; 4     Full variable contents and variable name.<br>
xdebug.collect_params=0</p>
<p>; This setting, defaulting to Off, controls whether Xdebug should write the<br>
; return value of function calls to the trace files.<br>
xdebug.collect_return=On</p>
<p>; This setting tells Xdebug to gather information about which variables are<br>
; used in a certain scope. This analysis can be quite slow as Xdebug has to<br>
; reverse engineer <a href="http://en.wikipedia.org/wiki/PHP" class="ml-smartlink" target="_blank">PHP</a>'s opcode arrays. This setting will not record which<br>
; values the different variables have, for that use xdebug.collect_params.<br>
; This setting needs to be enabled only if you wish to use<br>
; xdebug_get_declared_vars().<br>
xdebug.collect_vars=Off</p>
<p>; If this setting is On then stacktraces will be shown by default on an error<br>
; event. You can disable showing stacktraces from your code with xdebug_disable().<br>
; As this is one of the basic functions of Xdebug, it is advisable to leave this<br>
; setting set to 'On'.<br>
xdebug.default_enable=On</p>
<p>; These seven settings control which data from the superglobals is shown when an<br>
; error situation occurs. Each <a href="http://en.wikipedia.org/wiki/PHP" class="ml-smartlink" target="_blank">php</a>.ini setting can consist of a comma seperated<br>
; list of variables from this superglobal to dump, but make sure you do not add<br>
; spaces in this setting. In order to dump the REMOTE_ADDR and the REQUEST_METHOD<br>
; when an error occurs, add this setting: xdebug.dump.SERVER = REMOTE_ADDR,REQUEST_METHOD<br>
xdebug.dump.COOKIE=<br>
xdebug.dump.FILES=<br>
xdebug.dump.GET=<br>
xdebug.dump.POST=<br>
xdebug.dump.REQUEST=<br>
xdebug.dump.SERVER=<br>
xdebug.dump.SESSION=</p>
<p>; Controls whether the values of the superglobals as defined by the xdebug.dump.*<br>
; settings whould be shown or not.<br>
xdebug.dump_globals=On</p>
<p>; Controls whether the values of the superglobals should be dumped on all error<br>
; situations (set to Off) or only on the first (set to On).<br>
xdebug.dump_once=On</p>
<p>; If you want to dump undefined values from the superglobals you should set this<br>
; setting to On, otherwise leave it set to Off.<br>
xdebug.dump_undefined=Off</p>
<p>; Controls whether Xdebug should enforce 'extended_info' mode for the PHP parser;<br>
; this allows Xdebug to do file/line breakpoints with the remote <a href="http://en.wikipedia.org/wiki/Debugger" class="ml-smartlink" target="_blank">debugger</a>. When<br>
; tracing or profiling scripts you generally want to turn off this option as PHP's<br>
; generated oparrays will increase with about a third of the size slowing down<br>
; your scripts. This setting can not be set in your scripts with ini_set(), but<br>
; only in php.ini.<br>
xdebug.extended_info=1</p>
<p>; Introduced in Xdebug 2.1<br>
; This setting determines the format of the links that are made in the display<br>
; of stack traces where file names are used. This allows IDEs to set up a<br>
; link-protocol that makes it possible to go directly to a line and file by<br>
; clicking on the <a href="http://en.wikipedia.org/wiki/Filename" class="ml-smartlink" target="_blank">filenames</a> that Xdebug shows in stack traces. An example format<br>
; might look like: myide://%f@%l<br>
; The possible format specifiers are:<br>
; %f    the filename<br>
; %l    the line number<br>
xdebug.file_link_format=</p>
<p>; Controls which IDE Key Xdebug should pass on to the DBGp debugger handler.<br>
; The default is based on environment settings. First the environment setting<br>
; DBGP_IDEKEY is consulted, then USER and as last USERNAME. The default is set<br>
; to the first <a href="http://en.wikipedia.org/wiki/Environment_variable" class="ml-smartlink" target="_blank">environment variable</a> that is found. If none could be found the<br>
; setting has as default ''.<br>
xdebug.idekey=</p>
<p>; This is the base url for the links from the function traces and error message<br>
; to the manual pages of the function from the message. It is advisable to set<br>
; this setting to use the closest mirror.<br>
xdebug.manual_url=http://www.php.net</p>
<p>; Controls the protection mechanism for infinite recursion protection. The value<br>
; of this setting is the maximum level of nested functions that are allowed before<br>
; the script will be aborted.<br>
xdebug.max_nesting_level=100</p>
<p>; Introduced in Xdebug 2.1<br>
; By default Xdebug overloads var_dump() with its own improved version for displaying<br>
; variables when the html_errors php.ini setting is set to 1. In case you do not<br>
; want that, you can set this setting to 0, but check first if it's not smarter<br>
; to turn off html_errors.<br>
xdebug.overload_var_dump=On</p>
<p>; When this setting is set to 1, profiler files will not be overwritten when a<br>
; new request would map to the same file (depnding on the xdebug.profiler_output_name setting.<br>
; Instead the file will be appended to with the new profile.<br>
xdebug.profiler_append=0</p>
<p>; Enables Xdebug's profiler which creates files in the profile output directory.<br>
; Those files can be read by KCacheGrind to visualize your data. This setting<br>
; can not be set in your script with ini_set().<br>
xdebug.profiler_enable=0</p>
<p>; When this setting is set to 1, you can trigger the generation of profiler<br>
; files by using the XDEBUG_PROFILE GET/POST parameter. This will then write<br>
; the profiler data to defined directory.<br>
xdebug.profiler_enable_trigger=0</p>
<p>; The directory where the profiler output will be written to, make sure that the<br>
; user who the PHP will be running as has write permissions to that directory.<br>
; This setting can not be set in your script with ini_set().<br>
xdebug.profiler_output_dir=/tmp</p>
<p>; This setting determines the name of the file that is used to dump traces into.<br>
; The setting specifies the format with format specifiers, very similar to sprintf()<br>
; and strftime(). There are several format specifiers that can be used to format<br>
; the <a href="http://en.wikipedia.org/wiki/Filename" class="ml-smartlink" target="_blank">file name</a>.<br>
; See the xdebug.trace_output_name documentation for the supported specifiers.<br>
xdebug.profiler_output_name=cachegrind.out.%p</p>
<p>; Normally you need to use a specific HTTP GET/POST variable to start <a href="http://en.wikipedia.org/wiki/Debugging" class="ml-smartlink" target="_blank">remote debugging</a>.<br>
; When this setting is set to 'On' Xdebug will always attempt to start a remote<br>
; debugging session and try to connect to a client, even if the GET/POST/COOKIE<br>
; variable was not present.<br>
xdebug.remote_autostart=Off</p>
<p>; This switch controls whether Xdebug should try to contact a <a href="http://en.wikipedia.org/wiki/Debugging" class="ml-smartlink" target="_blank">debug</a> client which<br>
; is listening on the host and port as set with the settings xdebug.remote_host<br>
; and xdebug.remote_port. If a connection can not be established the script will<br>
; just continue as if this setting was Off.<br>
xdebug.remote_enable=Off</p>
<p>; Can be either 'php3' which selects the old PHP 3 style debugger output, '<a href="http://en.wikipedia.org/wiki/GNU_Debugger" class="ml-smartlink" target="_blank">gdb</a>'<br>
; which enables the GDB like debugger interface or 'dbgp' - the brand new debugger<br>
; protocol. The DBGp protocol is more widely supported by clients. See more<br>
; information in the introduction for <a href="http://en.wikipedia.org/wiki/Debugging" class="ml-smartlink" target="_blank">Remote Debugging</a>.<br>
xdebug.remote_handler=dbgp</p>
<p>; Selects the host where the debug client is running, you can either use a host<br>
; name or an IP address.<br>
xdebug.remote_host=localhost</p>
<p>; If set to a value, it is used as filename to a file to which all remote debugger<br>
; communications are logged. The file is always opened in append-mode, and will<br>
; therefore not be overwritten by default. There is no concurrency protection<br>
; available.<br>
xdebug.remote_log=</p>
<p>; Selects when a debug connection is initiated. This setting can have two different values:<br>
; req    Xdebug will try to connect to the debug client as soon as the script starts.<br>
; hit    Xdebug will only try to connect to the debug client as soon as an error condition occurs.<br>
xdebug.remote_mode=req</p>
<p>; The port to which Xdebug tries to connect on the remote host. Port 9000 is the<br>
; default for both the client and the bundled debugclient. As many clients use<br>
; this port number, it is best to leave this setting unchanged.<br>
xdebug.remote_port=9000</p>
<p>; When this setting is set to 1, Xdebug will show a <a href="http://en.wikipedia.org/wiki/Stack_trace" class="ml-smartlink" target="_blank">stack trace</a> whenever an<br>
; exception is raised - even if this exception is actually caught.<br>
xdebug.show_exception_trace=0</p>
<p>; When this setting is set to something != 0 Xdebug's generated stack dumps in<br>
; error situations will also show all variables in the top-most scope. Beware<br>
; that this might generate a lot of information, and is therefore turned off by default.<br>
xdebug.show_local_vars=0</p>
<p>; When this setting is set to something != 0 Xdebug's human-readable generated<br>
; trace files will show the difference in memory usage between function calls.<br>
; If Xdebug is configured to generate computer-readable trace files then they<br>
; will always show this information.<br>
xdebug.show_mem_delta=0</p>
<p>; The format of the trace file.<br>
; 0    shows a human readable indented trace file with: time index, memory usage,<br>
;      memory delta (if the setting xdebug.show_mem_delta is enabled), level,<br>
;      function name, function parameters (if the setting xdebug.collect_params<br>
;      is enabled, filename and line number.<br>
; 1    writes a computer readable format which has two different records. There<br>
;      are different records for entering a stack frame, and leaving a stack frame<br>
xdebug.trace_format=0</p>
<p>; When set to '1' the trace files will be appended to, instead of being overwritten<br>
; in subsequent requests.<br>
xdebug.trace_options=0</p>
<p>; The directory where the tracing files will be written to, make sure that the<br>
; user who the PHP will be running as has write permissions to that directory.<br>
xdebug.trace_output_dir=/tmp</p>
<p>; This setting determines the name of the file that is used to dump traces into.<br>
; The setting specifies the format with format specifiers, very similar to<br>
; sprintf() and strftime(). There are several format specifiers that can be used<br>
; to format the <a href="http://en.wikipedia.org/wiki/Filename" class="ml-smartlink" target="_blank">file name</a>. The '.xt' extension is always added automatically.<br>
;The possible format specifiers are:<br>
; %c  <a href="http://en.wikipedia.org/wiki/Cyclic_redundancy_check" class="ml-smartlink" target="_blank">crc32</a> of the current working directory  trace.%c           trace.1258863198.xt<br>
; %p  pid                                     trace.%p           trace.5174.xt<br>
; %r  random number                           trace.%r           trace.072db0.xt<br>
; %s  script name                             cachegrind.out.%s  cachegrind.out._home_httpd_html_test_xdebug_test_php<br>
; %t  <a href="http://en.wikipedia.org/wiki/Timestamp" class="ml-smartlink" target="_blank">timestamp</a> (seconds)                     trace.%t           trace.1179434742.xt<br>
; %u  timestamp (microseconds)                trace.%u           trace.1179434749_642382.xt<br>
; %H  $_SERVER['HTTP_HOST']                   trace.%H           trace.kossu.xt<br>
; %R  $_SERVER['REQUEST_URI']                 trace.%R           trace._test_xdebug_test_php_var=1_var2=2.xt<br>
; %S  session_id (from $_COOKIE if set)       trace.%S           trace.c70c1ec2375af58f74b390bbdd2a679d.xt<br>
; %%  literal %                               trace.%%           trace.%%.xt<br>
xdebug.trace_output_name=trace.%c</p>
<p>; Controls the amount of array children and object's properties are shown when<br>
; variables are displayed with either xdebug_var_dump(), xdebug.show_local_vars<br>
; or through Function Traces. This setting does not have any influence on the<br>
; number of children that is send to the client through the Remote Debugging feature.<br>
xdebug.var_display_max_children=128</p>
<p>; Controls the maximum string length that is shown when variables are displayed<br>
; with either xdebug_var_dump(), xdebug.show_local_vars or through Function Traces.<br>
; This setting does not have any influence on the amount of data that is send to<br>
; the client through the Remote Debugging feature.<br>
xdebug.var_display_max_data=512</p>
<p>; Controls how many nested levels of array elements and object properties are<br>
; when variables are displayed with either xdebug_var_dump(),<br>
; xdebug.show_local_vars or through Function Traces. This setting does not have<br>
; any influence on the depth of children that is send to the client through the<br>
; Remote Debugging feature.<br>
xdebug.var_display_max_depth=</p><p><br></p></p></div>
