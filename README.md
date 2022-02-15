# **MAC OS BIG SUR SETUP**

- [**MAC OS BIG SUR SETUP**](#mac-os-big-sur-setup)
  - [**Software/Apps/Packages To Install**](#softwareappspackages-to-install)
    - [**Homebrew**](#homebrew)
    - [**zsh**](#zsh)
      - [**oh my zsh**](#oh-my-zsh)
      - [**powerlevel10k**](#powerlevel10k)
      - [**plugins**](#plugins)
        - [**zsh-syntax-highlighting**](#zsh-syntax-highlighting)
        - [**zsh-autosuggestions**](#zsh-autosuggestions)
        - [**k**](#k)
        - [**.zshrc**](#zshrc)
    - [**pyenv**](#pyenv)
    - [**tmux**](#tmux)
    - [**Compress And Extract File**](#compress-and-extract-file)
      - [Compress](#compress)
      - [Extract](#extract)
  - [**References**](#references)

## **Software/Apps/Packages To Install**

### **Homebrew**

- Run this line to install **homebrew**:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

- Install Fira Code Nerd Font:

```bash
curl -o ~/Library/Fonts/FiraCodeNF.ttf -LJO https://github.com/ryanoasis/nerd-fonts/raw/master/patched-fonts/FiraCode/Regular/complete/Fira%20Code%20Regular%20Nerd%20Font%20Complete.ttf
```

### **zsh**

#### **oh my zsh**

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

#### **powerlevel10k**

- Download powerlevel10k

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

- Set `oh my zsh` theme to powerlevel10k in `~/.zshrc`

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```

- Set `typeset -g POWERLEVEL9K_PYENV_PROMPT_ALWAYS_SHOW` to true in `~/.p10k.zsh`

#### **plugins**

##### **zsh-syntax-highlighting**

- Download the plugins

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

- Include zsh-syntax-highlighting in ~/.zshrc plugins

##### **zsh-autosuggestions**

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

- Include zsh-autosuggestions in ~/.zshrc plugins

##### **k**

```bash
git clone https://github.com/supercrabtree/k ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/k
```

- Include k in ~/.zshrc plugins

##### **.zshrc**

- Settings to change:

```bash
plugins=(
    git
    copydir
    sudo
    k
    zsh-syntax-highlighting
    zsh-autosuggestions
)
```

### **pyenv**

- Run lines below to install pyenv and python version. Change 3.6.0 to python version that you want to install

```bash
brew install tmux coreutils pyenv pyenv-virtualenv openssl readline sqlite3 xz zlib sqlite bzip2 libiconv libzip

echo '
export PATH="$HOME/.pyenv/bin:$PATH"

eval "$(pyenv init --path)"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"

#pyenv
#openssl
export LDFLAGS="-L/usr/local/opt/zlib/lib -L/usr/local/opt/openssl@1.1/lib"
export CPPFLAGS="-I/usr/local/opt/zlib/include -I/usr/local/opt/openssl@1.1/include"

#readline
export LDFLAGS="-L/usr/local/opt/zlib/lib -L/usr/local/opt/readline/lib"
export CPPFLAGS="-I/usr/local/opt/zlib/include -I/usr/local/opt/readline/include"

#sqlite3
export LDFLAGS="-L/usr/local/opt/zlib/lib -L/usr/local/opt/sqlite3/lib"
export CPPFLAGS="-I/usr/local/opt/zlib/include -I/usr/local/opt/sqlite3/include"

#xz
export LDFLAGS="-L/usr/local/opt/zlib/lib -L/usr/local/opt/xz/lib"
export CPPFLAGS="-I/usr/local/opt/zlib/include -I/usr/local/opt/xz/include"

#zlib
export LDFLAGS="-L/usr/local/opt/zlib/lib -L/usr/local/opt/zlib/lib"
export CPPFLAGS="-I/usr/local/opt/zlib/include -I/usr/local/opt/zlib/include"

#sqlite
export LDFLAGS="-L/usr/local/opt/zlib/lib -L/usr/local/opt/sqlite/lib"
export CPPFLAGS="-I/usr/local/opt/zlib/include -I/usr/local/opt/sqlite/include"

#bzip2
export LDFLAGS="-L/usr/local/opt/zlib/lib -L/usr/local/opt/bzip2/lib"
export CPPFLAGS="-I/usr/local/opt/zlib/include -I/usr/local/opt/bzip2/include"

#libiconv
export LDFLAGS="-L/usr/local/opt/zlib/lib -L/usr/local/opt/libiconv/lib"
export CPPFLAGS="-I/usr/local/opt/zlib/include -I/usr/local/opt/libiconv/include"

#libzip
export LDFLAGS="-L/usr/local/opt/zlib/lib -L/usr/local/opt/libzip/lib"
export CPPFLAGS="-I/usr/local/opt/zlib/include -I/usr/local/opt/libzip/include"

' >> ~/.zshrc
```

- If fail to install pyenv, do the following:

```bash
brew doctor
git -C $(brew --repo homebrew/core) checkout master
```

- Install python version. Change 3.7.7 to another version that you want.

```bash
pyenv install 3.7.7
```

If fail, try this:

```bash
CFLAGS="-I$(brew --prefix openssl)/include -I$(brew --prefix bzip2)/include -I$(brew --prefix readline)/include -I$(xcrun --show-sdk-path)/usr/include" LDFLAGS="-L$(brew --prefix openssl)/lib -L$(brew --prefix readline)/lib -L$(brew --prefix zlib)/lib -L$(brew --prefix bzip2)/lib" pyenv install --patch 3.7.7 < <(curl -sSL https://github.com/python/cpython/commit/8ea6353.patch\?full_index\=1)
```

- To change python version:

```bash
pyenv global 3.7.7
```

- To create virtual environment

```bash
pyenv virtualenv 3.7.7 venv_name
source ~/.pyenv/versions/3.7.7/bin/activate
```

### **tmux**

```bash
echo '
# Improve colors
set -g default-terminal "screen-256color"
' >> ~/.tmux.conf
```

### **Compress And Extract File**

#### Compress

```bash
tar -jcvf archive_name.tar.bz2 folder_to_compress
```

#### Extract

```bash
tar -jxvf archive_name.tar.bz2 -C <path>
```

## **References**

- [pynenv](https://chamikakasun.medium.com/how-to-manage-multiple-python-versions-in-macos-2021-guide-f86ef81095a6)
- https://github.com/pyenv/pyenv
