# VSCode setup intructions

* Color theme
 Ctrl+Shift+P -> Color Scheme -> choose NetBeans light scheme (Ctrl+Shift+X -> search in extensions)

---------------------------

* If working through remote ssh - need first to establish a connection, and then install extensions there (in the remote session):
  - Ctrl+Shift+P -> add host and connect using ssh username@ip_address
  - for virtualBox may need to create host-only adapter first and check a separate ip-address (```ip a``` in the terminal), localhost with port 2200 (default NAT adapter) may not work
  - see ssh tutorial on how to connect using ssh-key and not being asked for password every time

-------------------------------
 
* Install Python extension
 
* Ctrl+Shift+P -> Settings -> Font size -> make 15
 
* Open project -> Select Interpreter
 be sure jupyter is installed in the environment
 
  then : select interpreter to start Jupyter -> then can open python interactive window

* Ctrl+Shift+P -> Settings -> Send selection to interactive window -> Check the box
 
---------------------------
 
* Adding black python formatter
    - go to user settings and search python formatting provider -> select black
    - Now create python files and go to Ctrl+Shift+P -> Format Document -> this will apply black
    - Follow black installation tip
    - in user settings look for 'format on save' and check the box (now Format will apply at each saving)
    - in user settings search for Black Args and add ```--skip-string-normalization``` (to avoid using " ")
    

* Install extensions:
  - html preview, Ctrl+K V to preview html
  - vscode-pdf to view pdfs
 
-------------------------

* jupyter notebook exporting to other formats (setup)
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
  
-------------------------------------------------

 
 * Install relative line number extension
 run Ctrl+Shift+P -> enable relative line number
 
 * Install vim emulator extension
   then Ctrl+Shift+P -> Open keyboard shortcuts -> search to toggleVim -> add Alt+Shift+V shortcut 
   to switch between vim and normal mode
   

 * Add to settings.json
 ```
 "vim.handleKeys": {
        "<C-f>": false,
        "<C-h>": false
    }
  ```
  (in general add any keys that I wan't to preserve from vscode in vim mode)

------------------------------------------------


* Go to user settings -> look for Notebook File Root and change it to ```${workspaceFolder}``` 
(this will open interactive window in the root of the currently open project)

* Install Python Docstring Generator Extension, use Ctrl+Shift+2 to generate docstring

* Go to keyboard shortcuts, add Shift+Alt+D shortcut for Debug Current Cell

* Set Ctrl+Alt+Shift+0 shortcut to clear all python cell output
* can use %reset magic to restart window


* Add Debug: Disconnect shortcut : Ctrl+Shift+F10

* Run Open Keyboard Shortcuts (JSON) - to open json file (not menu)

* Set up commands to run code (add to keybindings.json)

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


* Create new file: Ctrl+N -> Ctrl+S -> specify the path and the file name

* set Python interactive window keybindings
  - Ctrl+Shift+Alt+P : start PIW
  - Shift+Alt+R : restart PIW
  - Ctrl+Shift+Alt+0 : clear PIW output
  - Ctrl+Shift+Alt+C : collapse all input cells
  - Ctrl+Shift+Alt+V : expand all input cells     

* set Refresh Explorer to Ctrl+Shift+Alt+N

* Change Open debug console shortcut to Ctrl+; (to be similar to terminal Ctrl+')

* Change Ctrl+1/2/3 to Alt+1/2/3 (Alt+nb is for tabs inside the same window -- not very useful, first 3 nbs is enough, can change all to 9 of course)


---------------------------------


* To debug script of module use F5 - input script name or module name (module relative path is not supported so it must be in the current path - use ```. cwd-to-pypath``` in the currenly open terminal session in the parent dir); 
debug with stop at error or exception; 
use Shift+F5 to stop

* add shortcut Ctrl+Alt+J for toggle Maximized Panel (maximized terminal panel)

* add shortcut Alt+Shift+F10 for Run to cursor in debug

* add shortcut Shift+Alt+B to remove all breakpoints  


* open remote settings -> add the following to remote settings.json
```
 "python.dataScience.alwaysTrustNotebooks": true
```


* to write markdown in a vscode cell
  - start with ```#%% [markdown]```
  - write markdown code in comments, such as ```# * first item```




* install regreplace extension 
  - add the code below to settings.json to help with black lines while converting cell .py file to jupyter notebook
  - put on-save to false, only run at the very end before convertion (Ctrl+Shift+P -> run regreplace)
```
 "regreplace.commands": [
        {
            "name": "jupyter.export.helper",
            "language": "python",
            "regexp": "# %%",
            "global": true,
            "replace": "#%%"
        },
        {
            "name": "jupyter.export.helper",
            "language": "python",
            "regexp": "\n\n\n\n\n#%%",
            "global": true,
            "replace": "\n#%%"
        },
        {
            "name": "jupyter.export.helper",
            "language": "python",
            "regexp": "\n\n\n\n#%%",
            "global": true,
            "replace": "\n#%%"
        },
        {
            "name": "jupyter.export.helper",
            "language": "python",
            "regexp": "\n\n\n#%%",
            "global": true,
            "replace": "\n#%%"
        },
        {
            "name": "jupyter.export.helper",
            "language": "python",
            "regexp": "\n\n#%%",
            "global": true,
            "replace": "\n#%%"
        },
        {
            "name": "jupyter.export.helper",
            "language": "python",
            "regexp": "#%%\n\n\n\n\n",
            "global": true,
            "replace": "#%%\n"
        },
        {
            "name": "jupyter.export.helper",
            "language": "python",
            "regexp": "#%%\n\n\n\n",
            "global": true,
            "replace": "#%%\n"
        },
        {
            "name": "jupyter.export.helper",
            "language": "python",
            "regexp": "#%%\n\n\n",
            "global": true,
            "replace": "#%%\n"
        },
        {
            "name": "jupyter.export.helper",
            "language": "python",
            "regexp": "#%%\n\n",
            "global": true,
            "replace": "#%%\n"
        }
    ],
    "regreplace.on-save": false
```

* to write a markdown cell
```
#%% [markdown]
"""
## Header
* add any markdown content
* second item
  - subitem
"""
```

* to disable minimap : Ctrl+Shift+P -> toggle minimap


* in settings Open folder in a new window -> switch to on (will open another folder without closing the current one)

---------------------------------------------------

* Shortcuts (vscode default)
 
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

--------------------------------------------------

**big problem: how to make python refactoring : works ok inside a function, but not for global varialbles**




