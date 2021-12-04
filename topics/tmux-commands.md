# Tmux Commands

## Create new pane

* To the right: `CTRL+b %`

* To the bottom: `CTRL+b "`

* Switch between panes: `CTRL+b ← or →`

## Create new window

* `CTRL+b c`

* Switch between windows: `CTRL+b 0 or 1`

## Rename window

* `CTRL+b ,`

## List tmux sessions

* `tmux ls`

# Detach from a session

* `tmux detach`

* `CTRL+b d`

## Attach to a session

* `tmux attach -t 0`

## Rename a session

* `tmux rename-session -t 0 <new-name>`

## Create new session

* `tmux new -s <session-name>`

* e.g. `tmux new -s repos`