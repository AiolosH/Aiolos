---
title: vim 中自动添加头注释
description: linux
date: 2016-12-03 18:43:51 +08:00
tags: linux
category: linux
---

```
"SET Comment START
autocmd BufNewFile *.cpp exec ":call SetComment()" |normal 10Go

func SetComment()
        call append(1, '#********************************************************')
        call append(2, '#')
        call append(3, '#       FileName:      '.expand("%"))
        call append(4, '#')
        call append(5, '#       Author:         ')
        call append(6, '#       Description:    ')
        call append(7, '#       Create:        '.strftime("%Y-%m-%d %H:%M:%S"))
        call append(8, '#       Last Modified: '.strftime("%Y-%m-%d %H:%M:%S"))
        call append(9, '#********************************************************')
"       call append(10, '')
endfunc

map <F2> :call SetComment()<CR>:10<CR>o
"Set Comment END

```

然后再编辑器中按下<F2>，就回自动出现这些注释。
