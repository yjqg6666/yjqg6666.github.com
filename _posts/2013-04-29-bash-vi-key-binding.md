---
layout: default
title: bash_vim模式
published: true
category: linux
tags: [linux,key-binding]
---
<div id="detail" class="detail" style="line-height: 1.3;">
	#man readline 搜索DEFAULT KEY BINDINGS
VI Mode bindings VI模式键绑定
VI Insert Mode functions vi插入模式

"C-D"  vi-eof-maybe
"C-H"  backward-delete-char
"C-I"  complete
"C-J"  accept-line
"C-M"  accept-line
"C-R"  reverse-search-history
"C-S"  forward-search-history
"C-T"  transpose-chars
"C-U"  unix-line-discard
"C-V"  quoted-insert
"C-W"  unix-word-rubout
"C-Y"  yank
"C-["  vi-movement-mode
"C-_"  undo
" " to "~"  self-insert
"C-?"  backward-delete-char

VI Command Mode functions vim命令模式

"C-D"  vi-eof-maybe
"C-E"  emacs-editing-mode
"C-G"  abort
"C-H"  backward-char
"C-J"  accept-line
"C-K"  kill-line
"C-L"  clear-screen
"C-M"  accept-line
"C-N"  next-history
"C-P"  previous-history
"C-Q"  quoted-insert
"C-R"  reverse-search-history
"C-S"  forward-search-history
"C-T"  transpose-chars
"C-U"  unix-line-discard
"C-V"  quoted-insert
"C-W"  unix-word-rubout
"C-Y"  yank
"C-_"  vi-undo
" "  forward-char
"#"  insert-comment
"$"  end-of-line
"%"  vi-match
"&"  vi-tilde-expand
"*"  vi-complete
"+"  next-history
","  vi-char-search
"-"  previous-history
"."  vi-redo
"/"  vi-search
"0"  beginning-of-line
"1" to "9"  vi-arg-digit
";"  vi-char-search
"="  vi-complete
"?"  vi-search
"A"  vi-append-eol
"B"  vi-prev-word
"C"  vi-change-to
"D"  vi-delete-to
"E"  vi-end-word
"F"  vi-char-search
"G"  vi-fetch-history
"I"  vi-insert-beg
"N"  vi-search-again
"P"  vi-put
"R"  vi-replace
"S"  vi-subst
"T"  vi-char-search
"U"  revert-line
"W"  vi-next-word
"X"  backward-delete-char
"Y"  vi-yank-to
"\"  vi-complete
"^"  vi-first-print
"_"  vi-yank-arg
"`"  vi-goto-mark
"a"  vi-append-mode
"b"  vi-prev-word
"c"  vi-change-to
"d"  vi-delete-to
"e"  vi-end-word
"f"  vi-char-search
"h"  backward-char
"i"  vi-insertion-mode
"j"  next-history
"k"  prev-history
"l"  forward-char
"m"  vi-set-mark
"n"  vi-search-again
"p"  vi-put
"r"  vi-change-char
"s"  vi-subst
"t"  vi-char-search
"u"  vi-undo
"w"  vi-next-word
"x"  vi-delete
"y"  vi-yank-to
"|"  vi-column
"~"  vi-change-case
</div>
