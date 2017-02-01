## 島根支社勉強会

2016.7.11

清水　祐太

---
## Vim Plugin

---
### Vim
* vi から派生したエディタ

* Emacs 派とよく争いがおきる

---
### Vim Plugin
* Vim で使えるプラグイン
 + dein.vim
 + NERDTree
 + lightline.vim 他

* Vim script で記述

---
### dein.vim によるプラグイン管理例
.vimrc
```
if has('vim_starting')
  set nocompatible
  set runtimepath+=~/.vim/dein/repos/github.com/Shougo/dein.vim
endif

call dein#begin(expand('~/.vim/dein'))

call dein#add('Shougo/dein.vim')
call dein#add('Shougo/vimproc', {'build': 'make'})
call dein#add('Shougo/vimshell.vim')
call dein#add('Shougo/unite.vim', {
  \ 'depends': ['vimproc'],
  \ 'on_cmd': ['Unite'],
  \ 'lazy': 1})
...
```

---
### 作成

---
### 雛形
```
 .
 ├── autoload
 |          └── sample.vim
 └── plugin
            └── sample.vim
```

---
### plugin/sample.vim
```
if exists("g:loaded_sample")
  finish
endif
let g:loaded_sample = 1

let s:save_cpo = &cpo
set cpo&vim

" Vim script
command! -nargs=0 Sample call sample#sample()

let &cpo = s:save_cpo
unlet s:save_cpo
```

---
### autoload/sample.vim
```
if exists("g:loaded_sample_al")
  finish
endif
let g:loaded_sample_al = 1

let s:save_cpo = &cpo
set cpo&vim

function! sample#sample()
...
endfunction

let &cpo = s:save_cpo
unlet s:save_cpo
```

---
## プラグインを Python で書く

---
```
 .
 ├── python
 |          └── sample.py
 ├── autoload
 |          └── sample.vim
 └── plugin
            └── sample.vim
```

autoload/sample.vim
```
pyfile <sfile>:h:h/python/sample.py
python import vim

function! sample#sample()
  python sample()
endfunction
```

sample.py
```
def sample():
...
```

---
## デモ

