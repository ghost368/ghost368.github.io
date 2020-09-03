
* Color Scheme: Install Colorsublime package, then install NetBeans scheme

* Hide minimap

```
# by eugene-kim 

# Save it as minimap_setting.py in the User directory (in Preferences -> Browse Packages).
# Then, you just add "show_minimap": false in your settings and you're good to go!

import sublime
import sublime_plugin

class MinimapSetting(sublime_plugin.EventListener):

    def on_activated(self, view):
        show_minimap = view.settings().get('show_minimap')
        if show_minimap:
            view.window().set_minimap_visible(True)
        elif show_minimap is not None:
            view.window().set_minimap_visible(False)
```

* Ctrl+Shift+P -> Settings, 
in the right panel add 

```
"font_face": "Consolas",
"font_size": 12,
```

* Install MarkdownPreview package
add to KeyBindings
```
 { "keys": ["alt+m"], "command": "markdown_preview", "args": {"target": "browser", "parser":"markdown"} }
```

* Do not add MarkdownEditing package since it will change color scheme (will be hard to restore)

* add open folder shortcut to key bindings (folder will be added to the current window)

```
{ "keys": ["ctrl+shift+o"], "command": "prompt_add_folder"}
```

* Install Git package through package control
use Ctrl+Shift+P -> Git (with all standard commands; key binding not really necessary here)

* Install Terminal package
press Ctrl+Alt+Shift+t to open powershell in the current project folder (if e.g. need to work with git in console)
(can change powershell to cmd by setting terminal as cmd.exe in Preferences > Package Settings > Terminal > Settings Default)

* Shortcuts

| Shortcut | Action |
| ------------ | ------------- |
| Alt + Shift + nb columns| Split view into multiple columns |
| Ctrl + col nb| Switch cursor to certain column |
|Esc | Close build window |


* Ctrl+P : go to anything (including the currently open files)


* To use vim inside sublime 
	- remove Vintage and/or ActualVim from ignored packages in settings json file
	- add the following to keybindings to map Esc to jk
	```
	{ "keys": ["j", "k"], "command": "exit_insert_mode",
            "context":
            [
                { "key": "setting.command_mode", "operand": false },
                { "key": "setting.is_widget", "operand": false }
            ]
    }
	```

* to create command to toggle vim on/off
	- add this file (named anyway, e.g. toggle_vintage_command.py)
	```
	import sublime
	import sublime_plugin

	class ToggleVintageCommand(sublime_plugin.TextCommand):
	    def run(self, edit):
	        settings = sublime.load_settings('Preferences.sublime-settings')
	        ignored = settings.get("ignored_packages")
	        if "Vintage" in ignored:
	            ignored.remove("Vintage")
	        else:
	            ignored.append("Vintage")
	        settings.set("ignored_packages", ignored)
    ```
    to Packages/User (will open when running Browse Packages in sublime)

    - add the following key binding
    ```
    { "keys": ["shift+alt+v"], "command": "toggle_vintage" }
    ```


* it's possible to add custom commands or settings to sublime in this way
(see more details here https://stackoverflow.com/questions/24276143/can-i-create-my-own-command-in-sublime-and-how-to-associate-python-implementatio)

* to use SublimeText via remote connection using rmate:
	- install rsub package in sublime (local)
	- install rmate on the server (use sudo if necessary): 
	```
	wget -O /usr/local/bin/rsub \https://raw.github.com/aurora/rmate/master/rmate
	chmod a+x /usr/local/bin/rsub
	```
	- create ssh tunnel via MobaXterm: port 52698 to 52698 (should work with both NAT and Host only adapter IP address), must make it Remote port forwarding (!)
	- ```run rsub text_file``` to open remote file 

