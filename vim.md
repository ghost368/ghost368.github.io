### Shortcuts


|command |action|
|---------------|----------------|
|i| insert before cursor|
|I| insert at the beginning of the line|
|a| insert after cursor|
|A| insert at the end of line|
|o | insert to a new line below the current line|
|O | insert to a new line above the current line|
|s| substitute single character at cursor|
|S or cc| substitute the entire line|
|C| substitute the rest of line starting from cursor|
|J|join current line with the next line |
|j k h l| down up left right (can have nb in front)|
|0 $| to line start/end|
|^| to first non-blank line character|
|g_| to last non-black character|
|Ctrl+F/B| page down/up|
|:n :$| to n-th line, to file end|
|d_| delete completely without copying|
|{}|go to the previous/next blank line|
|x| Delete character from cursor position|
|X| Delete previous character from cursor position|
|y| Copy single character from cursor position|
|p| Paste character after cursor position|
|P| Paste character before cursor position|
|u/Ctrl+r|undo/redo|
|dw| Delete word from cursor position|
|diw| Delete word with cursor inside|
|cw|Same as dw but go to insert mode, the same for other commands|
|D| Delete entire line from cursor position|
|d| Delete entire line|
|Y| Copies entire line|
|yy| Copies entire line|
|gd| go to function/variable definition|
|gD| go to function/variable global definition|
|b / w| go back forward one word (from alpha-numerics)|
|B / W| go back forward one word (from non-whitespece chars, includes :,. etc)|
|v| go to visual mode|
|V| go to visual mode and select current line|
|# *| to the previous/next occurent of the current token, add it to n/N search|
|/smth + Enter|search for smth, then use n/N|
|:%s/smth/replacement/gc| replace smth|
|f char| move to the next char in the current line (F for previous)|
|t char| move right before the next char in the current line (T for previous)|
|: ,| go through results fwd/backwd after applying f, F, t, T|
|zt, zb, zz| move current line to the top, bottom and center of the screen|
|daw caw| delete the word around the cursor (and switch to insert for caw)|
|<line number>G| jump to a specific line number (e.g. 32G)|
|Shift zz| save and quit, like :wq|

* can combine commands and use e.g. vf, vt, vF, cF, cf, ct, dt, yF etc 

* ```:noh``` to remove highlighting from the seach 

* select to the next search result : v/text+enter - then use n/N to adjust selection; 
the same will work with c, d, y etc 


* to insert/delete smth vertically along multiple lines (e.g. in comment python)
	- use Ctrl+V to vertically select the first symbols of the lines to comment
	- then Shift+I -> type e.g. ```# ``` or anything, or select and remove -> Esc to exit visual mode
	- in terminal vim the new characters will first appear in the first line, then appear in the other line after going normal mode

* Ctrl+r is setup to replace the currently selected text
* deleting also saves the deleted text in the buffer (can be pasted with p, so it's like cut, use d_ to avoid cutting)


* can use d with other commands (0 $ w b j k 10j etc) to delete; 
c with other commands : same as d but goes directly into insert mode after that;
y will copy (yank), v will select


* vim requires the cursor to be visible at all times (this is not true in VSCode vim though), 
but can leave mark with ```mg```, go elsewhere and then go back with ```g``` 


* can copy and paste content using y and p combined with other commands between different files in vscode


* Vim keeps track of your navigation using a jump list. You can go backward and forward
through that list
	- Ctrl+O/Ctrl+i : jump previous/next position
	- most usefull when:
		- used search, went to result, did smth there and want to go back
		- went to function definition using ```gd```, then want to go back 
		- if did some actions - several go-backs may be need to reach the previous place


* to copy from vim terminal : usually Ctrl+Shift+C, Ctrl+Shift+V to paste into terminal
(vim VSCode can switch off vim and select using mouse, this is a rare task)

* to copy to vim : can use Ctrl+Shift+V or Ctrl+V depending on the system, editor;
(in MobaXterm I setup for the paste be Shift+Space)


* add leader specification to , in .vimrc
```
let mapleader = ","
let g:mapleader = ","
```
(can use <leader> in the mappings)

* key mapping:
	- :map is a usulal map, :noremap is a nonrecursive map
	- further need to specify mode in which to remap (i, n or v for insert, normal and visual)
	- hence get nnoremap, imap, vmap, vnoremap etc

### Terminal vim configuration

* add to ~/.vimrc 

```
imap jk <Esc>
set number
set wildmode=longest,list,full
set wildmenu
```
(map esc to jk, show line numbers in files, activate tab autocomplete)


* d and c in vim will actually cut the text (delete and add to buffer), 
to delete completely the black hole buffer is used ("_d, "_c), map it to simplfy (add to ~/.vimrc)
```
nnoremap <leader>d "_d
nnoremap <leader>c "_c
```



* to use Ctrl+R to replace selected text:
add ```vnoremap <C-r> "hy:%s/<C-r>h//gc<left><left><left>``` to .vimrc



### Terminal vim plugins


* install pathogen
```
mkdir -p ~/.vim/autoload ~/.vim/bundle && \
curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim
```
then add ```execute pathogen#infect()``` line to ~/.vimrc

* install autocomplete for python in vim YouCompleteMe
```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
cd ~/.vim/bundle
git clone https://github.com/Valloric/YouCompleteMe.git
cd YouCompleteMe
git submodule update --init --recursive
./install.sh --clang-completer
```


* install ropevim code python code refactoring
```
sudo pip3 install rope ropemode ropevim
wget -P ~/.vim/ https://raw.githubusercontent.com/python-rope/ropevim/master/ftplugin/python_ropevim.vim
echo "source ~/.vim/python_ropevim.vim" >> ~/.vimrc
```
see command description here https://github.com/python-rope/ropevim



* install vim-slime and vim-ipython-cell
	- need xclip and xsel
	```
	sudo apt-get install xclip xsel
	```
	- install using pathogen
	```
	cd ~/.vim/bundle
	git clone https://github.com/jpalardy/vim-slime.git
	git clone https://github.com/hanschen/vim-ipython-cell.git
	git clone https://github.com/preservim/nerdtree.git
	```
	- vim-ipython-cell page here https://github.com/hanschen/vim-ipython-cell


* pluging allwing to use vim as mini-IDE
	* NERDTree
	* YouCompleteMe
	* RopeVim
	* vim-ipython-cell


* can open folder with vim, in this case the tree will open

* add the following to .vimrc (slime and ipython-cell configuration)
```
"------------------------------------------------------------------------------
" slime configuration 
"------------------------------------------------------------------------------
" always use tmux
let g:slime_target = 'tmux'

" fix paste issues in ipython
let g:slime_python_ipython = 1

" always send text to the top-right pane in the current tmux tab without asking
let g:slime_default_config = {
            \ 'socket_name': get(split($TMUX, ','), 0),
            \ 'target_pane': '{top-right}' }
let g:slime_dont_ask_default = 1

"------------------------------------------------------------------------------
" ipython-cell configuration
"------------------------------------------------------------------------------
" Keyboard mappings. <Leader> is \ (backslash) by default

nnoremap <F9> :IPythonCellExecuteCellVerbose<CR>

nnoremap <F10> :IPythonCellExecuteCellJump<CR>
```



* shortcuts for NERDTree
```
let map_leader = ","
nmap <leader>ne :NERDTreeToggle<cr>
nmap <leader>nem :NERDTreeMirror<cr>
```

* splitting editor window:
	- :sp to split horizontally
	- : vsp to split vertically
	- close each split as usual
	- Ctrl+w then h j k l to move between panes



### file work


* ```:e file.txt``` create or edit file in the current dir using vim
* ```:w``` save, ```:q``` quit, ```:q!``` quit w/o saving
* ```:e``` to renew an already open file




### working with multiple tabs

* run ```:tabe``` followed by file path to edit another file 

* tab autocomplete (see ~/.vimrc modif at the beginning) help with file path:
	- tab will auto comlete a level or
	- tab will show possible options if non-unique 
	- then pressing tab will cycle through possible options
	- use right arrow to confirm (or press Enter to enter a different file manager mode)

* when multiple tabs are open : use ```g t```, ```g T``` to swictch between tabs

* use usual q, wq, q! to exit each tab, or qa, wqa, etc to quit all tabs

--------------------------------------

### VSCode Vim 

* mappings (add to settings json)

```
"vim.insertModeKeyBindings": [
     {
         "before": ["j", "k"],
         "after": ["<esc>"]
     }
], 
"vim.normalModeKeyBindingsNonRecursive": [
        {
            "before": [
                ",",
                "d"
            ],
            "after": [
                "\"",
                "_",
                "d"
            ]
        },
        {
            "before": [
                ",",
                "c"
            ],
            "after": [
                "\"",
                "_",
                "c"
            ]
        }
    ],
```
