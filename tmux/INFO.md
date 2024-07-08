# INFO

Welcome to my personal Tmux configuration. I hope you find it useful.
If you like it or not, or if you would change anything, you can let me know at:
- [X](https://x.com/josepmorgado)

First of all I would like you to keep in mind that this is a custom-made file with the aim of making my workflow
and the workflow of those who follow my path much more comfortable. 

People often ask me how I configure my tools, so by making this file I want to solve the issue of having to continually
explain how I do it by referring those who want to know my configuration to this file, saving time for all of us. 

I will edit this file whenever I feel the need to add new shortcuts or modify existing ones.

Feel free to download this file and add your own changes and personal preferences.


## Commands and Shortcuts

To be able to handle Tmux correctly, we need to know some essentials commands, as well as the most frequently used shortcuts.

### Commands
-Initialize a new session:
```
tmux
```
-Show a list of existing sessions:
```
tmux list-sessions
```
-Start an existing session:
```
tmux attach -t <NUMBER OF SESSION>
```

### Shortcuts
- `ctrl+b d` Detach the current tmux session.
- `ctrl+b x` Kill the active pane.
- `ctrl+b &` Kill the active window and all panes within it.
- `ctrl+b w` Shows a sessions preview (Kill session with `x` or change session with `Enter`).
- ``
