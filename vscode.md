* Installation
  * Linux
  * Windows
  download installer and follow the instructions
  
  
* Color theme
 Ctrl+Shift+P -> Color Scheme -> choose Light (Visual Studio)
 
* Install Python extension
 
* Ctrl+Shift+P -> Settings -> Font size -> make 15
 
* Open project -> Select Interpreter
 be sure jupyter is installed in the environment
 
then : select interpreter to start Jupyter -> then can open python interactive window

* Ctrl+Shift+P -> Settings -> Send selection to interactive window -> Check the box
 
 
* Adding black python formatter
    - go to user settings and search python formatting provider -> select black
    - Ctrl+Shift+P -> Format Document -> follow black installation tip
    - Now Format Document command will apply black
    - in user settings look for 'format on save' and check the box (now Format will apply at each saving)
    - in user settings search for Black Args and add ```--skip-string-normalization``` (to avoid using " ")
    
* Create new file: Ctrl+N -> Ctrl+S -> specify the path and the file name

* Install extensions:
  - html preview, Ctrl+K V to preview html
  - vscode-pdf to view pdfs
 
 
* Using jupyter notebook
  - need latex to convert to pdf, run 
  
  ```
  sudo apt-get install texlive-xetex texlive-fonts-recommended texlive-generic-recommended
  ```
  
  - install ```pandoc``` to convert markdown to other formats than html
  
  ```
  sudo apt-get install pandoc
  ```
  
  - if problem with inkscape, need to manually install it
  
  ```
  sudo apt-get install inkscape
  ```
  
  - then run convertion as follows
  
  ```
  jupyter nbconvert --to pdf file.ipynb
  ```
  
  - can use ``` --to pdf, --to html, --to latex ``` etc
  - can add ``` --no-input --no-prompt ``` to skip code and cell numbers respectively
  
  
 
 * Install relative line number extension
 run Ctrl+Shift+P -> enable relative line number
 
 * Install vim emulator extension
   then Ctrl+Shift+P -> Open keyboard shortcuts -> search to toggleVim -> add Alt+Shift+V shortcut 
   to switch between vim and normal mode
   
* Go to keyboard shortcuts and add ```Ctrl+Alt+P``` for opening python interactive window

* Go to user settings -> look for Notebook File Root and change it to ```${workspaceFolder}``` 
(this will open interactive window in the root of the currently open project)
 
 * Shortcuts
 
| Shortcut | Action |
| ------------ | ------------- |
| Alt + Shift + nb columns| Split view into multiple columns |
| Ctrl + col nb| Switch cursor to certain column |
| Ctrl+Shift+'| Open terminal|
| Ctrl + J| Hide/show terminal window|
| Ctrl + B| Hide/show sidebar|
|Ctrl+Shift+X| Open extensions|
|Ctrl+Shift+E| Open side explorer|
|Ctrl+Shift+ slash| Split editor window vertically|
|Ctrl+Alt+ left/right| Moving files between views in split mode|








