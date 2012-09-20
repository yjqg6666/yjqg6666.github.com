---
layout: default
title: bash内建的变量
published: true
category: Linux
tags: [linux,bash,built-in,变量, bash编程]
---
<div id="detail" class="detail" style="line-height: 1.3;">
PPID : 该bash的caller process ID.
PWD : 目前的工作目录。
OLDPWD : 上一个工作目录。
REPLY : 当read命令没有参数时，直接设在REPLY上。
UID : User ID。
EUID : Effective User ID。
BASH : Bash的完整路径。
BASH_VERSION : Bash版本。
SHLVL : 每次有Bash执行时，数字加一。
RANDOM : 每次这个参数被用到时，就会产生一个随机数。
SECONDS : 从这个Shell一开始启动后的时间。
LINENO : Script的行数。
HISTCMD : 历史记录数。
OPTARG : getopts处理的最後一个选项参数。
OPTIND : 下一个要由getopts所处理的参数号码。
HOSTTYPE : 机器类型。
OSTYPE : 系统名称。
IFS : Internal Field Separator。
PATH : 命令搜索路径。 PATH="/usr/gnu/bin:/usr/local/bin:/usr/ucb:/bin:/usr/bin:."
HOME : 目前使用者的home directory;
CDPATH : cd命令的搜寻路径。
ENV : 如果这个参数被设定，每次有shell script被执行时，将会执行它所设定的档名做为环境设定。
MAIL : 如果这个参数被设定，而且MAILPATH没有被设定，那麽有信件进来时，bash会通知使用者。
MAILCHECK : 设定多久时间检查邮件一次。
MAILPATH : 一串的邮件检查路径。
MAIL_WARNING : 如果有设定的话，邮件被读取後，将会显示讯息。
PS1 : 提示讯息设定，内定为"bash$ "。(请详见提示讯息一节。)
PS2 : 第二提示讯息设定，内定为"> "。
PS3 : select命令所使用的提示讯息。
PS4 : 执行追踪时用的提示讯息设定，内定为"+ "。
HISTSIZE : 命令历史记录量，内定为500。
HISTFILE : 历史记录档，内定~/.bash_history。
HISTFILESIZE : 历史记录档行数最大值，内定500。
OPTERR : 如果设为1，bash会显示getopts的错误。
PROMPT_COMMAND : 如果设定的话，该值会在每次执行命令前都显示。
IGNOREEOF : 将EOF值当成输入，内定为10。
TMOUT : 如果设为大於零，该值被解译为输入等待秒数。若无输入，当成没有输入。
FCEDIT : fc命令的内定编辑器。
FIGNORE : 请详见READLINE。
INPUTRC : readline的startup file，内定~/.inputrc
notify : 如果设定了，bash立即报告被终结的背景程式。
history_control, HISTCONTROL : history使用。
command_oriented_history : 存入多行指令。
glob_dot_filenames : 如果设定了，bash将会把"."包含入档案路径中。
allow_null_glob_expansion : 如果设定了，bash允许路径明称为null string。
histchars : history使用。
nolinks : 如果设定了，执行指令时，不会跟随symbolic links。
hostname_completion_file, HOSTFILE : 包含与/etc/hosts相同格式的档名。
noclobber : 如果设定了，Bash不会覆写任何由">"、">&"及"<>"所操作的档案。
auto_resume : 请见任务控制一节。
no_exit_on_failed_exec : 如果该值存在，非互动的shell不会因为exec失败而跳出。
cdable_vars : 如果启动，而cd命令找不到目录，可切换到参数形态指定的目录下。
</div>
