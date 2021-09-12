# **MAC OS BIG SUR SETUP**

- [**MAC OS BIG SUR SETUP**](#mac-os-big-sur-setup)
  - [**Software/Apps/Packages To Install**](#softwareappspackages-to-install)
    - [**Homebrew**](#homebrew)
    - [**pyenv**](#pyenv)
  - [**References**](#references)

## **Software/Apps/Packages To Install**

### **Homebrew**

- Run this line to install ***homebrew***:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### **pyenv**

- Run lines below to install pyenv and python version. Change 3.6.0 to python version that you want to install

```bash
brew install openssl readline sqlite3 xz zlib sqlite bzip2 libiconv libzip

echo '
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

curl https://pyenv.run | bash
sed -i '.bak' '/#pyenv/a\
export PATH="$HOME/.pyenv/bin:$PATH"\
eval "$(pyenv init -)"\
eval "$(pyenv virtualenv-init -)"\
' ~/.zshrc
rm ~/.zshrc.bak
```

- Install python version. Change 3.7.7 to another version that you want.

```bash
CFLAGS="-I$(brew --prefix openssl)/include -I$(brew --prefix bzip2)/include -I$(brew --prefix readline)/include -I$(xcrun --show-sdk-path)/usr/include" LDFLAGS="-L$(brew --prefix openssl)/lib -L$(brew --prefix readline)/lib -L$(brew --prefix zlib)/lib -L$(brew --prefix bzip2)/lib" pyenv install --patch 3.7.7 < <(curl -sSL https://github.com/python/cpython/commit/8ea6353.patch\?full_index\=1)
```

- To change python version:

```bash
pyenv global 3.7.7
```

## **References**

- [pynenv](https://chamikakasun.medium.com/how-to-manage-multiple-python-versions-in-macos-2021-guide-f86ef81095a6)
