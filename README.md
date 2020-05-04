# Awesome shell

## Basics

![Screenshot](https://i.imgur.com/2hPWFO2.png)

Install oh-my-zsh and [Powerline10k](https://github.com/romkatv/powerlevel10k) as a theme.
````bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k

# Modify .zshrc to use the new theme
ZSH_THEME="powerlevel10k/powerlevel10k"

# Disable aggressive auto-update
export UPDATE_ZSH_DAYS=365
````

## Extensions

````bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# Add them as plugins to .zshrc
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
````

Tip: If you are using iTerm2, modify colors so that autocomplete is visible.

### Faster pasting

````
# This speeds up pasting w/ autosuggest
# https://github.com/zsh-users/zsh-autosuggestions/issues/238
pasteinit() {
  OLD_SELF_INSERT=${${(s.:.)widgets[self-insert]}[2,3]}
  zle -N self-insert url-quote-magic # I wonder if you'd need `.url-quote-magic`?
}

pastefinish() {
  zle -N self-insert $OLD_SELF_INSERT
}
zstyle :bracketed-paste-magic paste-init pasteinit
zstyle :bracketed-paste-magic paste-finish pastefinish
````

## Arrow support

````
bindkey "[D" backward-word
bindkey "[C" forward-word
bindkey "^[a" beginning-of-line
bindkey "^[e" end-of-line
````

## Automatic ls after cd

````bash
function chpwd() {
  emulate -L zsh
  ls -a
}
````

## Better ls

````
brew install exa
alias ls="exa --color=auto --icons"
````

## Aliases

````
alias gitbranch="git for-each-ref --color=always --sort=committerdate refs/heads/ --format='%(HEAD) %(color:yellow)%(refname:short)%(color:reset) - %(color:red)%(objectname:short)%(color:reset) - %(contents:subject) - %(authorname) (%(color:green)%(committerdate:relative)%(color:reset))' | tail -15"
alias gpu='git push -u origin $(git symbolic-ref --short HEAD)'
alias changed='git diff HEAD'
alias acommit='git add -A :/ && git commit -a'
alias lock="/System/Library/CoreServices/Menu\ Extras/user.menu/Contents/Resources/CGSession -suspend"
````
