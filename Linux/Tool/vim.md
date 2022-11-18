# vim 常用按鍵
刪除一行：一般模式 dd
貼上文字：假如是從外部貼到vim裡面就用右鍵來貼
移動光標基本：數字 ＋ hjkl
移動到頁頂/頁底：gg/G
搜尋：/想搜尋的字
搜尋跳下一個字:n/N


# 進階按鍵

**光標定位**
- 最上面：zt
- 置中  ：zz
- 最下面：zb

**水平移動**
- 最後：$
- 最前：0


## vim 基礎設定

在vim裡面加入語法識別和行數
```vim
" 語法識別
syntax enable
" 顯示行數
set number
```
一般配置
```vim
" 支援 256 色
set t_Co=256

" 終端機背景色 : dark / light
set background=dark

" 內建風格 ( 縮寫指令 colo )
" 輸入 colorscheme 空一格，再按 Tab 可以依次預覽 : 
" blue / darkblue / default / delek / desert / eldlord
" evening / industry / koehler / morning / murphy / pable
" peachpuff / ron / shine / slate / torte / zollner
colorscheme default
```

增強編輯器功能
```vim
" 搜尋，高亮標註
set hlsearch

" 配置檔案路徑，讓 find 指令更好用
set path=.,/usr/include,,**

" ts = tabstop
set ts=4 "縮排 4 格

" tab 替換成空格
set expandtab

" 自動縮排 ｜ autoindent / smartindent / cindent
set autoindent " 跟上一行的縮進一致
```

**安裝Vundle**
1. 安裝git
2. 複製git 指令 <br> ``` git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim ``` 
3. 打開 vimrc 把東西都丟進去
 ```
set nocompatible              " be iMproved, required
filetype off                  " required

set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

Plugin 'VundleVim/Vundle.vim'

call vundle#end()            " required
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line
```
4. 進到編輯器打 :PluginInstall

**其他插件**
```
" 變漂亮、文字顏色功能
Plugin 'flazz/vim-colorschemes'
colorscheme molokai
" 側邊欄位
Plugin 'scrooloose/nerdtree'
Plugin 'jistr/vim-nerdtree-tabs'
" Markdown set
Plugin 'gabrielelana/vim-markdown'
Plugin 'tyru/open-browser.vim'
Plugin 'kannokanno/previm'

```

## vim & Markdown
上面重複的部分
```
" Markdown set
Plugin 'gabrielelana/vim-markdown'
Plugin 'tyru/open-browser.vim'
Plugin 'kannokanno/previm'

```
前面第一個是輔助Markdown語法
後面兩個可以打開瀏覽器預覽，但是要自己打指令(:PrevimOpen)

vim-instant-markdown 

1. 安裝白吃Node.js
2. 安裝完之後用Node.js下載東西
```
[sudo] npm -g install instant-markdown-d
```
3. 把東西打進.vimrc
```
Plug 'instant-markdown/vim-instant-markdown', {'for': 'markdown', 'do': 'yarn install'}
```

4. 建議再加上一點東西讓它可以顯示Markdown

~~~ 
let g:instant_markdown_mathjax = 1 
~~~

## vim & LaTeX

**vim LaTeX plug install**

```
Plugin 'vim-latex/vim-latex'

"-----------------latex-------------------------
" REQUIRED. This makes vim invoke Latex-Suite when you open a tex file.
filetype plugin on

" IMPORTANT: win32 users will need to have 'shellslash' set so that latex
" can be called correctly.
set shellslash

" IMPORTANT: grep will sometimes skip displaying the file name if you
" search in a singe file. This will confuse Latex-Suite. Set your grep
" program to always generate a file-name.
set grepprg=grep\ -nH\ $*

" OPTIONAL: This enables automatic indentation as you type.
filetype indent on
```   

**vim-latex-live-preview**
```
Plugin 'xuhdev/vim-latex-live-preview'
```   



## 參考資料

1. [用vim 編輯Markdown](https://fokayx.com/2018/01/21/markdown-extension-on-vim.html)
2. [vim Vundle](https://github.com/VundleVim/Vundle.vim)管理套件的一個東西
3. [配置vim](https://ithelp.ithome.com.tw/articles/10258222)裡面有夠詳細，有教把vim變好用之後還有教Vundle
4. [vim-instant-markdown](https://github.com/instant-markdown/vim-instant-markdown) 就酷
5. [vim 入門指南](https://ithelp.ithome.com.tw/articles/10255325?sc=pl)
6. [vim LaTeX配置教學](https://noootown.com/osx-vim-latex/)
7. [vim 學習影片（高見龍）](https://www.youtube.com/playlist?list=PLBd8JGCAcUAH56L2CYF7SmWJYKwHQYUDI)
8. [vim VSCode之類的推坑](https://medium.com/guy-chien/%E6%93%81%E6%8A%B1-vim-%E8%AE%93%E4%BD%A0%E7%9A%84%E6%99%82%E9%96%93%E4%B8%8D%E6%B5%AA%E8%B2%BB%E5%9C%A8%E7%B7%A8%E8%BC%AF%E4%B8%8A-f557d8e3e87e)
