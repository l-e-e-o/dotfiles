# ZSH config
I usually use [oh-my-zsh](https://ohmyz.sh/), so all of this might work on a plain zsh but I have not tested it there.

## git
Shortcut aliases because I'm lazy:

```sh
alias gca='git commit --amend'
alias gap='git add --patch'
```

## kubectl
Alias allowing quick namespace switches like `kn kube-system`:

```sh
kn(){
    kubectl config set-context --current --namespace=$1 > /dev/null
}
```

## SSH
Alias to switch to an ssh-agent session:

```sh
alias sa='ssh-agent $SHELL'
if (( ${+SSH_AUTH_SOCK} )) ; then
    if [ "$(ssh-add -l 2>/dev/null)" = "The agent has no identities." ]; then
        ssh-add ~/.ssh/id_ed25519
    fi
fi
```

You might want to include some automatism to make your prompt show that the ssh-agent is active so you don't forget you still have an unlocked ssh key in this shell (see [here](#Bullettrain) for an example).


## Theme-specific stuff
### Bullettrain
Customize the prompt to display the parent process if not running directly in my terminal (`alacritty`):

```sh
BULLETTRAIN_CUSTOM_MSG=$(if ! test $(ps -o comm= $(ps -o ppid= $$)) = "alacritty"; then if (( ${+SSH_AGENT_PID} )); then echo "ssh-agent"; else echo $(ps -o comm= $(ps -o ppid= $$)); fi; fi)
```

## WSL-specific stuff

### git
There is currently a major performance issue related to accessing the Windows filesystem from WSL which makes git very slow if the repository is outside the WSL filesystem. The following snippet fixes this to some degree:

```sh
# WSL2 performance issue workaround
isWinDir(){
    return $(! $(wslpath -w . | grep -q '\\wsl'))
}
git (){
    if isWinDir; then
        git.exe "$@"
    else
        /usr/bin/git "$@"
    fi
}
```

For this to work with the oh-my-zsh git plugin, the following snippet has to be included as well: 

```sh
# Fix for git prompt
__git_prompt_git() {
    if isWinDir; then
        git.exe --no-optional-locks $@
    else
        /usr/bin/git --no-optional-locks $@
    fi
}
```
