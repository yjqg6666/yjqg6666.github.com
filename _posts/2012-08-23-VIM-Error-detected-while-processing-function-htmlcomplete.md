---
layout: default
title: [转载]VIM-Error-detected-while-processing-function-htmlcomplete
published: true
category: vim
tags: [vim,html,补全报错]
---
<div id="detail" class="detail" style="line-height: 1.3;"><p>Error detected while processing function htmlcomplete#CompleteTags<div><br></div><div>使用第二个quote 解决问题且觉得合理就是这个原因引起的bug<br><div><br></div><div><br></div><div><br></div><div>&lt;quote from="https://bitbucket.org/ns9tks/vim-autocomplpop/issue/37/undefined-variable-classlines-e15-invalid"&gt;</div><div><br></div><div>Undefined variable: classlines, E15: Invalid expression: classlines</div><div><div><br></div><div><br></div><div>I use AutoComplPop in a HTML file, complete belowing: &lt;p class="c</div><div><br></div><div>Error detected while processing function htmlcomplete#CompleteTags: line 304: E121: Undefined variable: classlines Press ENTER or type command to continue Error detected while processing function htmlcomplete#CompleteTags: line 304: E15: Invalid expression: classlines Press ENTER or type command to continue</div></div><div><div>&nbsp; &nbsp;</div><div>&nbsp; &nbsp; You can fix this issue by inserting the following above line 288 of autoload/htmlcomplete.vim:</div><div><br></div><div>&nbsp;&lt;code&gt; &nbsp; let classlines = [] &nbsp; &lt;/code&gt;</div><div><br></div><div>&nbsp; &nbsp; The for loop will now look like this:</div><div>&lt;code&gt;</div><div>&nbsp; &nbsp; for file in cssfiles</div><div>&nbsp; &nbsp; &nbsp;let classlines = []</div><div>&nbsp; &nbsp; &nbsp;if filereadable(file)</div><div>&nbsp; &nbsp; &nbsp; let stylesheet = readfile(file)</div><div>&nbsp; &nbsp; &nbsp; let stylefile = join(stylesheet, ' ')</div><div>&nbsp; &nbsp; &nbsp; let stylefile = substitute(stylefile, '+&gt;\*[,', ' ', 'g')</div><div>&nbsp; &nbsp; &nbsp; if search_for == 'class'</div><div>&nbsp; &nbsp; &nbsp; &nbsp;let stylesheet = split(stylefile)</div><div>&nbsp; &nbsp; &nbsp; &nbsp;let classlines = filter(copy(stylesheet), "v:val =~ '\\([a-zA-Z0-9:]\\+\\)\\?\\.[a-zA-Z0-9_-]\\+'")</div><div>&nbsp; &nbsp; &nbsp; else</div><div>&nbsp; &nbsp; &nbsp; &nbsp;let stylesheet = split(stylefile, '[{}]')</div><div>&nbsp; &nbsp; &nbsp; &nbsp;" Get all lines which fit id syntax</div><div>&nbsp; &nbsp; &nbsp; &nbsp;let classlines = filter(copy(stylesheet), "v:val =~ '#[a-zA-Z0-9_-]\\+'")</div><div>&nbsp; &nbsp; &nbsp; &nbsp;" Filter out possible color definitions</div><div>&nbsp; &nbsp; &nbsp; &nbsp;call filter(classlines, "v:val !~ ':\\s*#[a-zA-Z0-9_-]\\+'")</div><div>&nbsp; &nbsp; &nbsp; &nbsp;" Filter out complex border definitions</div><div>&nbsp; &nbsp; &nbsp; &nbsp;call filter(classlines, "v:val !~ '\\(none\\|hidden\\|dotted\\|dashed\\|solid\\|double\\|groove\\|ridge\\|inset\\|outset\\)\\s*#[a-zA-Z0-9_-]\\+'")</div><div>&nbsp; &nbsp; &nbsp; &nbsp;let templines = join(classlines, ' ')</div><div>&nbsp; &nbsp; &nbsp; &nbsp;let stylelines = split(templines)</div><div>&nbsp; &nbsp; &nbsp; &nbsp;let classlines = filter(stylelines, "v:val =~ '#[a-zA-Z0-9_-]\\+'")</div><div><br></div><div>&nbsp; &nbsp; &nbsp; endif</div><div>&nbsp; &nbsp; &nbsp;endif</div><div>&nbsp; &nbsp; &nbsp;" We gathered classes definitions from all external files</div><div>&nbsp; &nbsp; &nbsp;let classes += classlines</div><div>&nbsp; &nbsp; endfor</div><div>&lt;/code&gt;</div></div><div>&lt;/quote&gt;</div><div><br></div><div><br></div><div>&lt;quote from="http://msf6300.blog.163.com/blog/static/1777190222011626105919952/"&gt;</div><div><div>使用autocomplpop编辑html文件时，比如输入"&lt;div " （DIV空格），这时会弹出提示来，当选择[class=" CDATA]或者[id=" ID]时，vim会报错：</div><div><br></div><div>Error detected while processing function htmlcomplete#complete tags:</div><div>line 304</div><div>E121: Undefined variable :classlines</div><div><br></div><div>原因是autoload/htmlcomplete.vim文件中在处理检测外连css文件的时候判断文件可读的地方写作了，后来作者从2006年以后就没有更新过。</div></div><div><br></div><div><p>問題發生的原因是，這個 html 自動完成函式會去檢查你的 <a rel="nofollow" href="http://www.hz328.com/web/">CSS </a>，包括外連的檔案，去裡面把 class name, id name 抽出送回作自動完成的選項，不過他有一個動作應該是要檔案可讀才要跑的，卻放到 if 的外面，所以只要把它移過去就好了</p><p>把</p><p><a href="/attachment/201208/23/22355887_13456886598rzW.png" target="_blank"><img src="/attachment/201208/23/22355887_13456886598rzW.png" width="604.38" height="249.06" onload="imgResize(this, 650);" border="0" ;=""></a></p><p>改为</p><p><a href="/attachment/201208/23/22355887_1345688688OKW0.png" target="_blank"><img src="/attachment/201208/23/22355887_1345688688OKW0.png" width="604.38" height="266.28" onload="imgResize(this, 650);" border="0" ;=""></a></p></div><div>是把312行let classes += classlines注释掉 复制这两行到endif（与if filereadable(file)配对的endif, 从缩进可以看出）的上面并取消注释&nbsp;</div><div>&lt;/quote&gt;</div></div></p></div>