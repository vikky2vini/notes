## tmux

###### Start a new session:
  `$ tmux new -s mysession`

###### Start a new session from within tmux:
  `:new -s mysession`

###### Set copy mode to emacs
    Prefix, :
    set-window-option mode-keys emacs

###### Set copy mode to vi
    Prefix, :
    set-window-option mode-keys vi

###### Copy and paste text (emacs mode)
    Prefix, [
    CTRL Space to start selecting
    After selecting, press ALT+W (might be CTRL+W on some configurations) to copy to tmux's clipboard
    Paste with Prefix, ]

##### Copy and base text (vi mode)
    Prefix, [
    Space (or v) to start selecting
    After selecting, press enter (or y) to copy to tmux's clipboard
    Paste with Prefix, ]
