---
layout: post
title:  "Ubuntu 14.04 Environment Setup"
categories: Ubnutu
comments: true
tags:  Ubuntu Environment 
author: Jaehyek
---

### .vimrc

set tabstop=4
set shiftwidth=4
set cindent
set autoindent
set smartindent
set expandtab
set number
set showmatch
set ignorecase
set smarttab
set showcmd
set hlsearch
set incsearch
set ruler
filetype on
set mouse=a
syntax on
set tags=./tags,./TAGS,tags,TAGS

filetype indent on
set ff=unix
colorscheme desert

autocmd vimenter * if !argc() | NERDTree | endif
map <C-n> :NERDTreeToggle<CR>
autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTreeType") && b:NERDTreeType == "primary") | q | endif


### .bashrc

alias a='alias'
alias vi='vim'
alias dir='ls -al --color=auto'
alias ls='ls -a --color=auto'
alias h='history'
alias sb='source .bashrc'
alias vb='vi .bashrc'
alias pstree='pstree -apcl'
alias scrr='screen -li'
HISTFILESIZE=5000

### 한글 설정하기
참조 할 site <http://ngee.tistory.com/326>

효과를 보기 위해서는  language support 에서 한글 language을 선택하고 reboot한다. 


### ssh server setup

$> sudo apt-get install openssh-server openssh-client

