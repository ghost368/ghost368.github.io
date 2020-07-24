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
   

* Go to user settings -> look for Notebook File Root and change it to ```${workspaceFolder}``` 
(this will open interactive window in the root of the currently open project)

* Install Python Docstring Generator Extension

* Go to keyboard shortcuts, add Shift+Alt+D shortcut for Debug Current Cell

* Set Ctrl+Alt+Shift+0 shortcut to clear all python cell output
* can use %reset magic to restart window


* Add Debug: Disconnect shortcut : Ctrl+Shift+F10

* Run Open Keyboard Shortcuts (JSON) - to open json file (not menu)

* Set up commands to run code

  - run current line or selection in terminal (ipython) - may be useful occasionally

  ```
  {
          "key": "alt+enter",
          "command": "python.execSelectionInTerminal",
          "when": "editorTextFocus && !findInputFocussed &&  !replaceInputFocussed && editorLangId == 'python'"
  }
  ```

  - run current line or selection in python interactive window

  ```
      {
          "key": "ctrl+shift+enter",
          "command": "python.datascience.runcurrentcelladvance",
          "when": "editorTextFocus && python.datascience.featureenabled && python.datascience.hascodecells && !editorHasSelection && !notebookEditorFocused"
      }
  ```

  - Ctrl+Enter : run current cell  - by default (cell commands only apply to interactive window)

  - Run cell and advance

  ```
      {
          "key": "shift+enter",
          "command": "-python.datascience.runcurrentcelladvance",
          "when": "editorTextFocus && python.datascience.featureenabled && python.datascience.hascodecells && !editorHasSelection && !notebookEditorFocused"
      }
  ```

* set keyboard shortcut Clear All Notifications to Shift+Alt+N

* set setting Collapse Cell Input by default to false 

* set Python interactive window keybindings
  - Ctrl+Shift+Alt+P : start PIW
  - Ctrl+Shift+Alt+R : restart PIW
  - Ctrl+Shift+Alt+0 : clear PIW output
  - Ctrl+Shift+Alt+C : collapse all input cells
  - Ctrl+Shift+Alt+V : expand all input cells     

* set Refresh Explorer to Ctrl+Shift+Alt+N

* Change Open debug console shortcut to Ctrl+; (to be similar to terminal Ctrl+')

* Change Ctrl+1/2/3 to Alt+1/2/3 (Alt+nb is for tabs inside the same window -- not very useful, first 3 nbs is enough, can change all to 9 of course)


* To debug script of module use F5 - input script name or module name (module relative path is not supported so it must be in the current path - use ```. cwd-to-pypath``` in the currenly open terminal session in the parent dir); 
debug with stop at error or exception; 
use Shift+F5 to stop

* add shortcut Ctrl+Alt+J for toggle Maximized Panel (maximized terminal panel)

* add shortcut Alt+Shift+F10 for Run to cursor in debug

* Shortcuts
 
| Shortcut | Action |
| ------------ | ------------- |
| Alt + Shift + nb columns| Split view into multiple columns |
| Ctrl + col nb| Switch cursor to certain column |
| Ctrl+Shift+'| Open new terminal|
| Ctrl+'| Open current terminal (works in vim mode)|
| Ctrl + J| Hide/show terminal window|
| Ctrl + B| Hide/show sidebar|
|Ctrl+Shift+X| Open extensions|
|Ctrl+Shift+E| Open side explorer|
|Ctrl+Shift+G| Open git explorer|
|Ctrl+Shift+T| Open keyboard shortcuts|
|Ctrl+Shift+ slash| Split editor window vertically|
|Ctrl+Alt+ left/right| Moving files between views in split mode|
|Ctrl =/-| increase/descrease font in editor and consoles|
|Ctrl+F4| Close application tab (like settings, keybindings etc)|

* add shortcut Shift+Alt+B to remove all breakpoints  





