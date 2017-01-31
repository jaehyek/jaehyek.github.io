---
layout: post
title:  "Ubuntu 14.04 Environment Setup"
categories: Ubnutu
comments: true
tags:  Ubuntu Environment 
author: Jaehyek
---

### .vimrc

set tabstop=4 <br/>
set shiftwidth=4 <br/>
set cindent <br/>
set autoindent <br/>
set smartindent <br/>
set expandtab <br/>
set number <br/>
set showmatch <br/>
set ignorecase <br/>
set smarttab <br/>
set showcmd <br/>
set hlsearch <br/>
set incsearch <br/>
set ruler <br/>
filetype on <br/>

syntax on <br/>
set tags=./tags,./TAGS,tags,TAGS <br/>

filetype indent on <br/>
set ff=unix <br/>
colorscheme desert <br/>

autocmd vimenter * if !argc() | NERDTree | endif <br/>
map <C-n> :NERDTreeToggle<CR> <br/>
autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTreeType") && b:NERDTreeType == "primary") | q | endif <br/>


### .bashrc

alias a='alias' <br/>
alias vi='vim' <br/>
alias dir='ls -al --color=auto' <br/>
alias ls='ls -a --color=auto' <br/>
alias h='history' <br/>
alias sb='source .bashrc' <br/>
alias vb='vi .bashrc' <br/>
alias pstree='pstree -apcl' <br/>
alias scrr='screen -li' <br/>
HISTFILESIZE=5000 <br/>

### 한글 설정하기 <br/>
참조 할 site <http://ngee.tistory.com/326>

효과를 보기 위해서는  language support 에서 한글 language을 선택하고 reboot한다. 


### ssh server setup

$> sudo apt-get install openssh-server openssh-client

