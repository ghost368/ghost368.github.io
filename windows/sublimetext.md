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
