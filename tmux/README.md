# tmux
## Install tmux.config
For user:

```sh
curl https://raw.githubusercontent.com/l-e-e-o/dotfiles/main/tmux/tmux.conf > ~/.tmux.conf
```

For user + root:

```sh
curl https://raw.githubusercontent.com/l-e-e-o/dotfiles/main/tmux/tmux.conf | sudo tee /root/.tmux.conf > ~/.tmux.conf
```

## Use tmux
Start personalized root tmux session with own preferences (zsh + vim). This is useful for hosts with shared administration where simply changing the config for the root user is not feasible:

```sh
sudo tmux new -A -s lfr 'export SHELL=/usr/bin/zsh; export EDITOR='vim'; export VISUAL=$EDITOR; tmux set-option default-shell /usr/bin/zsh; exec zsh'
```

As shell alias:

```sh
alias admin="sudo tmux new-session -A -s lfr 'export SHELL=/usr/bin/zsh; export EDITOR='vim'; export VISUAL=$EDITOR; tmux set-option default-shell /usr/bin/zsh; exec zsh'"
```
