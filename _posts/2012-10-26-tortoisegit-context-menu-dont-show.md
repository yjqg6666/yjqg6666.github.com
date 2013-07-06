---
layout: default
title: tortoisegit右键菜单不显示解决方法
published: true
category: Windows
tags: [git,windows,tortoisegit,乌龟git,右键菜单,无响应]
---
<div id="detail" class="detail" style="line-height: 1.3;">
    windows下的tortoisegit跟tortoisesvn一样，仍是一款相当优秀的版本控制前端软件, 因为在tortoisegit设置中的常规设置上下文菜单(context menu)和扩展菜单(Set Extend Menu Item)全部选中了导致右键菜单中的tortoisegit二级菜单无法显示.  软件重装仍然无法打开， 查看项目主页的faq找到一行 
    <quote>
Q: How to show extended menu item
A: Press "shift" key, right-click

Q: How to hide some menu items
A: setting -> Set Extend Menu Item. Choose menu you want to hide 
    </quote>
    按着shift键并在任一文件夹上点右键, 此时右键菜单中就有了tortoisegit的一些常用操作， 此时选择"设置"取消全部选择的上下文菜单(context menu)和扩展菜单(Set Extend Menu Item) 只选择常用的即可
</div>
