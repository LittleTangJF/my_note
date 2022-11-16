```js
#PHP

 echo 'export PATH="/usr/local/opt/php@7.3/bin:$PATH"' >> ~/.zshrc

  echo 'export PATH="/usr/local/opt/php@7.3/sbin:$PATH"' >> ~/.zshrc

# mysql

PATH=$PATH:/usr/local/mysql/bin

  

# code

alias code="/Applications/Visual\ Studio\ Code.app/Contents/Resources/app/bin/code"

  

#node

export NODE_OPTIONS=--max_old_space_size=8192

  

# nvm

export NVM_DIR="$HOME/.nvm"

[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm

[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

  

# export PATH=$HOME/bin:/usr/local/bin:$PATH

  

# proxy

function proxy_off(){

    unset http_proxy

    unset https_proxy

    echo -e "已关闭代理"

}

function proxy_on() {

    export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com"

    export http_proxy="http://127.0.0.1:7890"

    export https_proxy=$http_proxy

    echo -e "已开启代理"

}

  

# Path to your oh-my-zsh installation.

export ZSH="$HOME/.oh-my-zsh"

ZSH_THEME="amuse"

source $ZSH/oh-my-zsh.sh

  

# brew

export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles/bottles

export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.ustc.edu.cn/brew.git"

export PATH="/usr/local/opt/php@7.3/bin:$PATH"

export PATH="/usr/local/opt/php@7.3/sbin:$PATH"
```