---
title: Vim 에디터
date: 2021-08-31
excerpt: "vim의 사용법에 대해 알아보고 테크닉을 익혀보자:)"
categories:
- LINUX
tags:
- Linux
- Vim
---


<br />
<br />

---

# 개요

---

vi는 BSD의 C shell을 개발한 빌 조이가 만든 편집기이다. Visual edit의 줄임말이다.

vi의 최대 장점은 마우스 없이 키보드로 모든 것이 가능하는 점이다.

vim은 Vi Improved의 줄임말로 Vi의 기본기능에 여러가지 기능들이 추가된 것으로 우리는 이 편집기를 사용할 것이다.

이제 vim 에디터의 사용법을 알아보고 테크닉, 설치할 플러그인, 기타 팁들을 알아보겠다.

<br />
<br />



# Vim 모드의 이해

vim에는 3가지의 모드가 있다. 표준 모드, 입력 모드, 명령라인 모드이다. 

vim을 처음 실행시키면 표준 모드에서 시작한다. 그 상태에서 입력모드로 진입하는 키를 누르면 입력모드로 전환되고 `esc`키를 누르면 다시 표준모드로 간다.

명령라인 모드는 이제 자세히 살펴 보도록 하겠다.


## 파일의 저장

<br />

| 명령 | 설명 |
| --- | --- | 
| :w | 저장 | 
| :w file.txt | file.txt 파일로 저장 | 
| :w >> file.txt | file.txt 파일에 덧붙여 저장 | 
| :q | vim 에디터 종료 | 
| ZZ | 저장후 종료 |
| :wq! | 강제 저장 후 종료 | 
| :e file.txt | file.txt 파일을 불러옴 | 

<br />

## 입력모드로의 전환

<br />

| 명령 | 설명 |
| --- | --- | 
| a | 커서 위치 다음 칸부터 입력 | 
| A | 커서 행의 맨 마지막부터 입력 | 
| i | 커서의 위치에 입력 | 
| I | 커서 행의 맨 앞에서부터 입력 | 
| o | 커서의 다음 행에 입력 |
| O | 커서의 이전 행에 입력 | 
| s | 커서 위치의 한 글자를 지우고 입력 | 
| cc | 커서 위치의 한 행을 지우고 입력 | 

<br />

## 커서의 이동

<br />

| 명령 | 설명 |
| --- | --- | 
| h | 왼쪽 | 
| j | 아래 | 
| k | 위 | 
| l | 오른쪽 | 
| w | 다음 단어 첫 글자 |
| b | 이전 단어 첫 글자 |
| ^ | 행의 제일 첫 글자 |
| $ | 행의 제일 마지막 글자 |
| { | 이전 문단으로 이동 | 
| } | 다음 문단으로 이동 |  
| gg | 문서의 맨 처음 |
| G | 문서의 맨 마지막 |
| :숫자 | 숫자 행으로 이동 |
| / | 정방향으로 탐색 |
| ? | 역방향으로 탐색 |

<br />

## 파일의 편집

<br />

| 명령 | 설명 |
| --- | --- | 
| x | 커서 위치의 글자 삭제 | 
| dw | 한 단어를 삭제 | 
| dd | 한 행을 삭제 |
| yy | 한 행을 복사 |
| yw | 한 단어를 복사 |
| p | 붙여넣기 |
| u | 되돌리기 |
| `Ctrl` r | 다시 실행하기 |
| `Ctrl` v | 블럭 지정 |
| `Shift` v | 한 행 블럭 지정 |

<br />

# 나의 vim 설정

```
set hlsearch " 검색어 하이라이팅
set nu " 줄번호
set autoindent " 자동 들여쓰기
set scrolloff=2
set wildmode=longest,list
set ts=4 "tag select
set sts=4 "st select
set sw=1 " 스크롤바 너비
set autowrite " 다른 파일로 넘어갈 때 자동 저장
set autoread " 작업 중인 파일 외부에서 변경됬을 경우 자동으로 불러옴
set cindent " C언어 자동 들여쓰기
set bs=eol,start,indent
set history=256
set laststatus=2 " 상태바 표시 항상
"set paste " 붙여넣기 계단현상 없애기
set shiftwidth=4 " 자동 들여쓰기 너비 설정
set showmatch " 일치하는 괄호 하이라이팅
set smartcase " 검색시 대소문자 구별
set smarttab
set smartindent
set softtabstop=4
set tabstop=4
set ruler " 현재 커서 위치 표시
set incsearch
set statusline=\ %<%l:%v\ [%P]%=%a\ %h%m%r\ %F\
" 마지막으로 수정된 곳에 커서를 위치함
au BufReadPost *
\ if line("'\"") > 0 && line("'\"") <= line("$") |
\ exe "norm g`\"" |
\ endif
" 파일 인코딩을 한국어로
if $LANG[0]=='k' && $LANG[1]=='o'
set fileencoding=korea
endif
" 구문 강조 사용
if has("syntax")
 syntax on
endif
" 컬러 스킴 사용
colorscheme jellybeans
set guifont=Monaco:h10 noanti
nmap <F8> :TagbarToggle<CR>

set shell=/bin/bash

set rtp+=~/.vim/bundle/Vundle.vim

call plug#begin('~/.vim/plugged')
Plug 'airblade/vim-gitgutter'
Plug 'editorconfig/editorconfig-vim'
Plug 'itchyny/lightline.vim'
Plug 'junegunn/fzf'
Plug 'junegunn/fzf.vim'
Plug 'mattn/emmet-vim'
Plug 'scrooloose/nerdtree'
Plug 'terryma/vim-multiple-cursors'
Plug 'tpope/vim-eunuch'
Plug 'tpope/vim-surround'
Plug 'w0rp/ale'
Plug 'gmarik/Vundle.vim'
Plug 'nanotech/jellybeans.vim'
Plug 'majutsushi/tagbar'
Plug 'nathanaelkane/vim-indent-guides'
Plug 'tpope/vim-fugitive' " vim with git command(e.g., Gdiff)
Plug 'vim-airline/vim-airline' " vim status bar
Plug 'vim-airline/vim-airline-themes'
Plug 'blueyed/vim-diminactive'
call plug#end()
set t_Co=256

" for jellybeans
colorscheme jellybeans

" for taglist
nmap <F8> :Tagbar<CR>

" for indent guide
let g:indentguides_spacechar = '┆'
let g:indentguides_tabchar = '|'
let g:indent_guides_enable_on_vim_startup = 1
let g:indent_guides_start_level=2
let g:indent_guides_guide_size=1

" for vim-airline
let g:airline#extensions#tabline#enabled = 1 " turn on buffer list
let g:airline_theme='hybrid'
set laststatus=2 " turn on bottom bar
let mapleader = ","
nnoremap <leader>q :bp<CR>
nnoremap <leader>w :bn<CR>

" for blueyed/vim-diminactive
let g:diminactive_enable_focus = 1

syntax enable
filetype indent on
```

플러그인을 설치하려면 `PlugInstall Plug`를 사용하면 된다.

