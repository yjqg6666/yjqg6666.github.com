---
layout: default
title: 修改NERDtree的行号为相对行号
published: true
category: vim
tags: [vim,NERDtree,相对行号,relative line number]
---
<div id="detail" class="detail" style="line-height: 1.3;">
    版本大于7.03的vim支持相对行号功能 开启方式是 :set rnu 也可以加入.vimrc中 set rnu启动即开启此功能
    NERDtree启用显示行号功能: 在.vimrc文件的NERDtree配置中添加 
    <pre> let NERDTreeShowLineNumbers=1 </pre>
    在用户目录下.vim/plugin/NERD_tree.vim中搜索ShowLineNumbers找到下列行
    <pre>
        if g:NERDTreeShowLineNumbers
            setlocal nu
        else
            setlocal nonu
            if v:version >= 703
                setlocal nornu
            endif
        endif
    </pre>
    将其修改为
    <pre>
        if g:NERDTreeShowLineNumbers
            if v:version >=703
                setlocal rnu
            else
                setlocal nu 
            endif
        else
            setlocal nonu
            if v:version >= 703
                setlocal nornu
            endif
        endif
    </pre>

</div>
