# vim
## Install vimrc
For user:

```sh
curl https://raw.githubusercontent.com/l-e-e-o/dotfiles/main/vim/vimrc > ~/.vimrc
```

For user + root:

```sh
curl https://raw.githubusercontent.com/l-e-e-o/dotfiles/main/vim/vimrc | sudo tee /root/.vimrc > ~/.vimrc
```

## Additional features
Automatically load updated vimrc when saving:

```vimrc
" Automatic reloading of .vimrc on :w
autocmd! bufwritepost .vimrc source %
```
