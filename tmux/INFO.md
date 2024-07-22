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

## Concepts
In order to understand the commands and shortcuts properly, it is necesary to define some essential concepts.

### Sessions

### Windows
While working with Tmux you are using at least 1 window.

### Pane
Panes are sections inside a window.

## Commands and Shortcuts

To be able to handle Tmux correctly, we need to know some essentials commands, as well as the most frequently used shortcuts.

## Commands

> [!NOTE]
> There are some cases where you can achieve the same result by using a command and/or a shortcut. In those cases the shortcut will obtain preference over the command because of its ease of use. That means that I wont be adding the command to this file to avoid redundancy.

> [!IMPORTANT]
> There are commands that you can use either outside or inside a tmux window, and others that can only be use outside a tmux window. I will put them separately.

### Outside Tmux
-Initialize a new session:
```
tmux
```
-Attatch to an existing session:
```
tmux a -t <NUMBER OF SESSION>
```

### Outside and Inside Tmux
-Show a list of existing sessions:
```
tmux ls
```

## Shortcuts
>[!NOTE]
>The default `Prefix`is `C+b` (But you can change the `Prefix` by customizing the `.tmux.conf` file located in the `$HOME` directory.
>On Linux the C key is Control, the S key is Shift, and the M key is Alt.

### Sessions
- `Prefix w` Shows a sessions preview (Kill session with `x` or change session with `Enter`).
- `Prefix d` Detach the current tmux session.
- `Prefix $` Rename session.
  
### Windows
- `Prefix &` Kill the active window.
- `Prefix c` New window.
- `Prefix ,` Rename window.
- `Prefix n` Next window.
- `Prefix p` Previous window.
  
### Panes
- `Prefix x` Kill the active pane.
- `Prefix C+%` Vertical pane split. 
- `Prefix C+"` Horizontal pane split.
- `Prefix [h,j,k,l]` Pane move h-left, j-down, k-up, l-right.
- `Prefix  hold C+[h,j,k,l]` Pane resize.
- `Prefix M+[1-5]` Change the pane layout to:
  - 1. even-horizontal
  - 2. even-vertical
  - 3. main-horizontal
  - 4. main-vertical
  - 5. tiled
