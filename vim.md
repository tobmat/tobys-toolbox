# VIM - All the things I've learned but can't remember about the best file editor in the world!

---

#### Tricks

Get rid of ^M \(Usually found if copying a file from windows\):

```
:ed ++ff=dos %

OR

:%s/\r//g
```

sort a file:

```
:%!sort
```

show end of line:

```
:set list
```

---

#### Plugin Manager Setup - This is for vimplug

Find instructions here:  [https://github.com/junegunn/vim-plug](https://github.com/junegunn/vim-plug) OR

Setup ~/.vimrc file to autoinstall vim-plug, and autoload plugin files:

```
" Silent vim-plug setup and initial PlugInstall
if empty(glob('~/.vim/autoload/plug.vim'))
  silent !curl -fLo ~/.vim/autoload/plug.vim --create-dirs
    \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  autocmd VimEnter * PlugInstall --sync | source $MYVIMRC
endif
" Specify a directory for plugins (for Neovim: ~/.local/share/nvim/plugged)
call plug#begin('~/.vim/plugged')

" Color schemes
Plug 'altercation/vim-colors-solarized'

" UI
Plug 'scrooloose/nerdtree'
Plug 'scrooloose/syntastic'

" Initialize plugin system
call plug#end()
```

---

#### Plugins I use

###### Nerdtree - vim file manager, can open multiple files at ones

Setup  - I have the following pieces in my ~/.vimrc file:

```
"Show hidden files in NerdTree
"let NERDTreeShowHidden=1

"autopen NERDTree and focus cursor in new document
"autocmd VimEnter * NERDTree
"autocmd VimEnter * wincmd p

" Give a shortcut key to NERD Tree
map <F2> :NERDTreeToggle<CR>
```

Cheatsheet

```
Lets open some windows
s open new vertical split window
i open new horizontal spilt window

The next question I had was how do I switch back and forth between NERDTree and the other windows. 
All window commands start with ctrl+w

ctrl+ww cycle though all windows
crtl+wh takes you left a window
crtl+wj takes you down a window
crtl+wk takes you up a window
crtl+wl takes you right a window

Lets open some tabs
t open new tab
T open new tab while staying in current tab
gt cycle though all tabs
gT cycle though all tabs (moves to the left)

Toggle NerdTree
Fn+F2

Toggle paste from insert
Fn+F2

Toggle line numbers
con

Create a new file
ma

Hidden Files toggle
I

Set tree root
C

Directories
o: open & close
O: recurs­ively open
x: close parent
X: close all children recurs­ively
e: explore selected dir
```

###### Syntastic - checks syntax for many common scripting languages

~/.vimrc setup

```
" Syntastic Settings
set statusline+=%#warningmsg#
set statusline+=%{SyntasticStatuslineFlag()}
set statusline+=%*

let g:syntastic_always_populate_loc_list = 1
let g:syntastic_auto_loc_list = 1
let g:syntastic_check_on_open = 1
let g:syntastic_check_on_wq = 0
```

---

#### ~/.vimrc

vimrc file setup to customize vim.  Here are the current ones I'm using:

```
" turn off smart indentation when pasting - this will turn off auto comment and indent when pasting
set pastetoggle=<F2>

" default to paste mode
set paste

" shortcut to turn off line numbers
map <silent> con :set number!<CR>
```



