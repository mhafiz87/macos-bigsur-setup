# **MAC OS BIG SUR SETUP**

- [**MAC OS BIG SUR SETUP**](#mac-os-big-sur-setup)
  - [**Software To Install**](#software-to-install)
  - [**Homebrew**](#homebrew)
  - [**pyenv**](#pyenv)

## **Software To Install**

## **Homebrew**

- Run this line to install ***homebrew***:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## **pyenv**

- Run lines below to install pyenv and python version. Change 3.6.0 to python version that you want to install

```bash
brew install zlib sqlite bzip2 libiconv libzip
brew install pyenv pyenv-virtualenv
nano ~/.zshrc

...
export PATH="$HOME/.pyenv/bin:$PATH"
export PATH="/usr/local/bin:$PATH"

eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
export LDFLAGS="-L/usr/local/opt/zlib/lib -L/usr/local/opt/bzip2/lib"
export CPPFLAGS="-I/usr/local/opt/zlib/include -I/usr/local/opt/bzip2/include"
...

. ~/.zshrc
CFLAGS="-I$(brew --prefix openssl)/include -I$(brew --prefix bzip2)/include -I$(brew --prefix readline)/include -I$(xcrun --show-sdk-path)/usr/include" LDFLAGS="-L$(brew --prefix openssl)/lib -L$(brew --prefix readline)/lib -L$(brew --prefix zlib)/lib -L$(brew --prefix bzip2)/lib" pyenv install --patch 3.6.0 < <(curl -sSL https://github.com/python/cpython/commit/8ea6353.patch\?full_index\=1)
```

- To change python version:

```bash
pyenv global 3.7.7
pyenv versions
echo -e $'if command -v pyenv 1>/dev/null 2>&1; then\\n  export PYENV_ROOT="$HOME/.pyenv"\\n  export PATH="$PYENV_ROOT/bin:$PATH"\\n  eval "$(pyenv init --path)"\\n  eval "$(pyenv init -)"\\nfi' >> ~/.zshrc
```
