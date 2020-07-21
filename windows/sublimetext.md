* Installation: download installer and follow the guide

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
