* add to ~/.vimrc 

```
imap jk <Esc>
set number
set wildmode=longest,list,full
set wildmenu
```
(map esc to jk, show line numbers in files, activate tab autocomplete)



--------------------

* vscode mappings (add to settings json)

```
"vim.insertModeKeyBindings": [
     {
         "before": ["j", "j"],
         "after": ["<esc>"]
     }
]
```

* switching to Insert mode

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

J : join current line with the next line

* navigation

|command |action|
|---------------|----------------|
|j k h l| down up left right (can have nb in front)|
|0 $| to line start/end|
|^| to first non-blank line character|
|g_| to last non-black character|
|Ctrl+F/B| page down/up|
|:n :$| to n-th line, to file end|

* Vim keeps track of your navigation using a jump list. You can go backward and forward
through that list

Ctrl+O/Ctrl+i : jump previous/next position

in VSCode vim: Atl left/right (general commands)


* Cut, Copy and Paste

|command |action|
|------|--------|
|x| Delete character from cursor position|
|X| Delete previous character from cursor position|
|y| Copy single character from cursor position|
|p| Paste character after cursor position|
|P| Paste character before cursor position|


u/Ctrl+r : undo/redo

|command |action|
|------|--------|
|dw| Delete word from cursor position|
|diw| Delete word with cursor inside|
|D| Delete entire line from cursor position|
|d| Delete entire line|
|Y| Copies entire line|
|yy| Copies entire line|
|gd| go to function/variable definition|
|gD| go to function/variable global definition|



* modes: command, insert, command line and visual


* ```:edit file.txt``` create or edit file in the current dir using vim

* ```:w``` save, ```:q``` quit, ```:q!``` quit w/o saving


* b and w : go back forward one word
* dd also saves the deleted text in the buffer (can be pasted with p, so it's like cut)

* Shift + V : select line

* v : go to visual mode


* form command mode : / to start search, then Enter and use n/N to go through search results forward/backward
* * (star) enable to search for the current word under cursor and use n/N to go through


* horizontal moves

|command |action|
|------|--------|
|f char| move to the next char in the current line (F for previous)|
|t char| move right before the next char in the current line (T for previous)|
|: ,| go through results fwd/backwd after applying f, F, t, T|


* can use d with other commands (0 $ w b j k 10j etc) to delete,
c with other commands : same as d but goes directly into insert mode after that


* vim requires the cursor to be visible at all times (this is not true in VSCode vim though), 
but can leave mark with ```mg```, go elsewhere and then go back with ````g``` 


* zt, zb, zz : move current line to the top, bottom and center of the screen

* daw caw - delete the word around the cursor (and switch to insert for caw)

* can copy and paste content using y and p combined with other commands between different files in vscode


-------------------------------------------

## working with multiple tabs

* run ```:tabe``` followed by file path to edit another file 

* tab autocomplete (see ~/.vimrc modif at the beginning) help with file path:
	- tab will auto comlete a level or
	- tab will show possible options if non-unique 
	- then pressing tab will cycle through possible options
	- use right arrow to confirm (or press Enter to enter a different file manager mode)

* when multiple tabs are open : use ```g t```, ```g T``` to swictch between tabs

* use usual q, wq, q! to exit each tab, or qa, wqa, etc to quit all tabs


* to command multiple lines (e.g. in python)
	- use Ctrl+V to vertically select the first symbols of the lines to comment
	- then Shift+I -> type ```# ``` -> Esc to exit visual mode



* install autocomplete for python in vim YouCompleteMe
```
sudo apt install vim-youcompleteme
vim-addon-manager install youcompleteme
```
(may also need to install vim addon manager via sudo apt-get install)


* add 
```vnoremap <C-r> "hy:%s/<C-r>h//gc<left><left><left>``` to .vimrc, they select text and 
Ctrl+R to replace it (will be prompted to enter replacing text)


* install ropevim code python code refactoring
```
sudo pip3 install rope ropemode ropevim
wget -P ~/.vim/ https://raw.githubusercontent.com/python-rope/ropevim/master/ftplugin/python_ropevim.vim
echo "source ~/.vim/python_ropevim.vim" >> ~/.vimrc
```
see command description here https://github.com/python-rope/ropevim

----------------
stopped at Searching (page 24)



--------------------------


questions:
- how to copy external content in vim mode

- understand better how copying with ```y``` works

- how to copy between different files in terminal vim