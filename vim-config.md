---
title: vim 配置
date: 2017-06-23 13:20:34
tag: vim
---

vim 是一个可以安装各种插件来丰富自己的编辑器，也是"编辑器之神"

<!-- more -->

### `~/.vimrc` 文件
> vim 编辑器的配置文件，所有插件和各种配置都在可以在这里配置，所以这个文件很重要


### vim 插件管理
> vim 自身是没有插件管理的， 所以需要安装一个插件管理器来管理插件 。[Vundle](http://github.com/VundleVim/Vundle.Vim) 是目前最好的插件管理器


* 安装方法

```bash
vim ~/.vimrc

set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'

"Custom Plugin list

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required

```

* 使用方法
```bash
https://github.com/VundleVim/Vundle.Vim
```

### 推荐的插件
* syntastic
* vim-autoformat
* SimpylFold
* Powerline

```vimrc
Plugin 'tmhedberg/SimpylFold'
Plugin 'Valloric/YouCompleteMe'
Plugin 'scrooloose/nerdtree'
" 这个插件可以显示文件的Git增删状态
Plugin 'Xuyuanp/nerdtree-git-plugin'
Plugin 'kien/ctrlp.vim'  " 全局搜索
Plugin 'Lokaltog/powerline', {'rtp': 'powerline/bindings/vim/'}
```

* NERDTree
```bash
Plugin 'scrooloose/nerdtree'
" 这个插件可以显示文件的Git增删状态
Plugin 'Xuyuanp/nerdtree-git-plugin'
```

```vimrc

" Ctrl+N 打开/关闭
map <C-n> :NERDTreeToggle<CR>
" 当不带参数打开Vim时自动加载项目树
autocmd StdinReadPre * let s:std_in=1
autocmd VimEnter * if argc() == 0 && !exists("s:std_in") | NERDTree | endif
" 当所有文件关闭时关闭项目树窗格
autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTreeType") && b:NERDTreeType == "primary") | q | endif
" 不显示这些文件
let NERDTreeIgnore=['\.pyc$', '\~$', 'node_modules'] "ignore files in NERDTree
" 不显示项目树上额外的信息，例如帮助、提示什么的
let NERDTreeMinimalUI=1

```
