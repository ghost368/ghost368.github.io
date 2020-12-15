* tmux shortcuts: Ctrl+B to activate tmux command mode, then
	- % to split horizontally
	- " to split vertically
	- up/down/left/right to navigate between open terminals
	- Ctrl up/down/left/right to adjust terminal relative size
	- [ to start scroll mode, the use up/down, pgUp/pgDown to scroll through history, 
	q to exit scroll mode
	- exit to close a terminal
	- exit pand : Ctrl+d

* more tmux shortcuts:
https://tmuxcheatsheet.com/

* install ```xclip``` and ```xsel```

* tmux config : add the following to ~/.tmux.conf
```
set -g default-terminal "screen-256color"
setw -g mouse on

set-window-option -g mode-keys vi
bind-key -T copy-mode-vi v send -X begin-selection
bind-key -T copy-mode-vi V send -X select-line
bind-key -T copy-mode-vi y send -X copy-pipe-and-cancel 'xclip -in -selection clipboard'

set-option -s set-clipboard off
bind-key -T copy-mode-vi MouseDragEnd1Pane send-keys -X copy-pipe-and-cancel "xclip -se c -i"
```
explanation:
	- make bash prompts colorful and in usual bash
	- make mouse working - can use to scroll history (q to exit scroll mode, of scroll down), change pane sizes, select text, move focus to another pane
	- set vim commands to use with history (scroll mode active with scroll or ```Ctrl+B [``` then can use vim to find and select smth in the bash pane history)
	- last 2 commands make possible mouse copying to clipboard from tmux : select smth with mouse, release mouse click will automatically copy to clipboard
	(in vim might need to get rid of line numbers before selection, do ```:set nonumber```)


* to make bash always start in tmux by default - add this to ~/.bashrc
```
if command -v tmux &> /dev/null && [ -n "$PS1" ] && [[ ! "$TERM" =~ screen ]] && [[ ! "$TERM" =~ tmux ]] && [ -z "$TMUX" ]; then
  exec tmux
fi
```

* to list all tmux sessions
```
tmux list-sessions
```
(when making change to ~/.tmux.conf may need to close all sessions before they will take effect)

* to start each bash command on new line (useful then having long env paths, almost no place for the command itself in the line)
go to ~/.bashrc and find PS1 variable - can adjust it to anything (e.g. I added \n after :, to get ~$ on the next line)

* can setup colors, text style and output for PS1 (strings shown at the start of each command) in ```~/.bashrc```
