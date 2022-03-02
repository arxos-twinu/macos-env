# macos-env
Simple set-up for a fresh install of basic tools required for development.


# First boot

You are free to use a personal apple id or create a new independent. Have to keep in mind, if using the personal one, the computer will pull contacts/e-mails/password associated with your personal apple id account.

# Install package manager:

The first step will be to install the "brew" package manager for MAC-OS. This way we can easily verify the version of software we are using across the development environment. 
You can check more about it here: https://brew.sh/

To install brew, just open the terminal and run the following:

```/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" ```

Follow the instructions and wait until is ready. 

After the instalation is done, you will have to expose the binaries managed by brew to the terminal environment. To do this, create a '.zshrc' file on home exposing the new path:

``` echo 'export PATH=/opt/homebrew/bin:$PATH'>> ~/.zshrc | source ~/.zshrc ```

Done, brew is ready to go!

# Install Docker, NVM and Microsoft office

You can search the command to install different software using the search function in the brew website 'https://brew.sh/'

## Docker:
``` brew install --cask docker```

## Microsoft office (Includes Powerpoint, Word, Excel and OneDrive) :
``` brew install --cask microsoft-office ```
After installation you will need to log into OneDrive and Microsoft Word/Excel/Powerpoint to be able to use them. 

## NVM (Node version manager):
```brew install nvm ```


After installation, you need to open the .zshrc file and add the following:

```export NVM_DIR="$HOME/.nvm" 
[ -s "$(brew --prefix)/opt/nvm/nvm.sh" ] && \. "$(brew --prefix)/opt/nvm/nvm.sh" # This loads nvm 
[ -s "$(brew --prefix)/opt/nvm/etc/bash_completion.d/nvm" ] && \. "$(brew --prefix)/opt/nvm/etc/bash_completion.d/nvm" # This loads nvm bash_completion 
```

# Recommended
The following are not required but can be helpful for easier terminal usage.

## Install zplug for zsh configuration management:
```brew install zplug```

## Install TMUX for terminal management (terminal multiplexer):
```brew install tmux```


## Add plugings and themes to configuration
Example of a complete .zhrc configuration file

```# Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.
# Initialization code that may require console input (password prompts, [y/n]
# confirmations, etc.) must go above this block; everything else may go below.
if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi

# #Custom variables
ZSH_TMUX_AUTOSTART=true
ZSH_TMUX_AUTOSTART_ONCE=false
ZSH_TMUX_AUTOQUIT=false


# Exports

export PATH=/opt/homebrew/bin:$PATH
export ZPLUG_HOME=$(brew --prefix)/opt/zplug
export NVM_DIR="$HOME/.nvm"
[ -s "$(brew --prefix)/opt/nvm/nvm.sh" ] && \. "$(brew --prefix)/opt/nvm/nvm.sh" # This loads nvm
[ -s "$(brew --prefix)/opt/nvm/etc/bash_completion.d/nvm" ] && \. "$(brew --prefix)/opt/nvm/etc/bash_completion.d/nvm" # This loads nvm bash_completion


# sources
source $ZPLUG_HOME/init.zsh


# Plugins zplug
zplug "plugins/git",   from:oh-my-zsh
zplug "plugins/tmux",   from:oh-my-zsh
zplug "plugins/tmuxinator",   from:oh-my-zsh
zplug "plugins/osx",   from:oh-my-zsh
zplug "zsh-users/zsh-autosuggestions"
zplug "clvv/fasd"
zplug "b4b4r07/enhancd"
zplug "junegunn/fzf"
zplug "Peltoche/lsd"
zplug "g-plane/zsh-yarn-autocompletions"
zplug "romkatv/powerlevel10k", as:theme, depth:1

zplug "zplug/zplug", hook-build:'zplug --self-manage'

# Install plugins if there are plugins that have not been installed
if ! zplug check --verbose; then
    printf "Install? [y/N]: "
    if read -q; then
        echo; zplug install
    fi
fi

# Then, source plugins and add commands to $PATH
if zplug check || zplug install; then
  zplug load
fi

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh

```

source the new configuration to kick off the changes. Follow the instructions to set-up the theme with your preferences, as well as to install the plugins. Enjoy the new development environment. 

```source ~/.zshrc```
