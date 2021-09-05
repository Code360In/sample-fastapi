# 0. Default Info

```sh
admin@gw-mac ~ % pwd
/Users/admin
admin@gw-mac ~ % ls /usr/bin | grep python
python
python-config
python2
python2.7
python2.7-config
python3
pythonw
pythonw2.7
admin@gw-mac ~ % python -V
Python 2.7.16
admin@gw-mac ~ % python3 -V
Python 3.8.2
admin@gw-mac ~ %
```

# 1. Install Homebrew

```sh
admin@gw-mac ~ %
admin@gw-mac ~ % which brew
brew not found
admin@gw-mac ~ % /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
==> Checking for `sudo` access (which may request your password).
Password:
==> This script will install:
/opt/homebrew/bin/brew
/opt/homebrew/share/doc/homebrew
/opt/homebrew/share/man/man1/brew.1
/opt/homebrew/share/zsh/site-functions/_brew
/opt/homebrew/etc/bash_completion.d/brew
/opt/homebrew
==> The following new directories will be created:
/opt/homebrew/bin
...
...
...
Receiving objects: 100% (1034675/1034675), 418.14 MiB | 4.56 MiB/s, done.
Resolving deltas: 100% (708937/708937), done.
From https://github.com/Homebrew/homebrew-core
 * [new branch]            master     -> origin/master
HEAD is now at 017c694c16 scrollkeeper: fix test (#84622)
Warning: /opt/homebrew/bin is not in your PATH.
  Instructions on how to configure your shell for Homebrew
  can be found in the 'Next steps' section below.
==> Installation successful!
==> Next steps:
- Run these two commands in your terminal to add Homebrew to your PATH:
    echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/admin/.zprofile
    eval "$(/opt/homebrew/bin/brew shellenv)"
- Run `brew help` to get started
- Further documentation:
    https://docs.brew.sh
admin@gw-mac ~ %
admin@gw-mac ~ % which brew
brew not found
admin@gw-mac ~ % /opt/homebrew/bin/brew shellenv
export HOMEBREW_PREFIX="/opt/homebrew";
export HOMEBREW_CELLAR="/opt/homebrew/Cellar";
export HOMEBREW_REPOSITORY="/opt/homebrew";
export HOMEBREW_SHELLENV_PREFIX="/opt/homebrew";
export PATH="/opt/homebrew/bin:/opt/homebrew/sbin${PATH+:$PATH}";
export MANPATH="/opt/homebrew/share/man${MANPATH+:$MANPATH}:";
export INFOPATH="/opt/homebrew/share/info:${INFOPATH:-}";
admin@gw-mac ~ %
admin@gw-mac ~ % echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/admin/.zprofile
admin@gw-mac ~ % cat /Users/admin/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
admin@gw-mac ~ % eval "$(/opt/homebrew/bin/brew shellenv)"
admin@gw-mac ~ % which brew
/opt/homebrew/bin/brew
admin@gw-mac ~ %
admin@gw-mac ~ % brew -v
Homebrew 3.2.10
Homebrew/homebrew-core (git revision 017c694c16; last commit 2021-09-04)
admin@gw-mac ~ %
admin@gw-mac ~ % brew list
admin@gw-mac ~ %
```

# 2. Install Python3

```sh
admin@gw-mac ~ % brew install python3
==> Downloading https://ghcr.io/v2/homebrew/core/gdbm/manifests/1.20
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/gdbm/blobs/sha256:5c3247c107b
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/
...
...
...
Python has been installed as
  /opt/homebrew/bin/python3

Unversioned symlinks `python`, `python-config`, `pip` etc. pointing to
`python3`, `python3-config`, `pip3` etc., respectively, have been installed into
  /opt/homebrew/opt/python@3.9/libexec/bin

You can install Python packages with
  pip3 install <package>
They will install into the site-package directory
  /opt/homebrew/lib/python3.9/site-packages

tkinter is no longer included with this formula, but it is available separately:
  brew install python-tk@3.9

See: https://docs.brew.sh/Homebrew-and-Python
admin@gw-mac ~ %
admin@gw-mac ~ % brew list

==> Formulae
gdbm		openssl@1.1	readline	xz
mpdecimal	python@3.9	sqlite
admin@gw-mac ~ % exit
admin@gw-mac ~ % python3 -V
Python 3.9.6
admin@gw-mac ~ % python -V
Python 2.7.16
admin@gw-mac ~ %
admin@gw-mac ~ % python3 -m pip --version
pip 21.1.3 from /opt/homebrew/lib/python3.9/site-packages/pip (python 3.9)
admin@gw-mac ~ %
admin@gw-mac ~ % which pip3
/opt/homebrew/bin/pip3
admin@gw-mac ~ % ls -l /opt/homebrew/bin/pip3
lrwxr-xr-x  1 admin  admin  35 Sep  4 06:25 /opt/homebrew/bin/pip3 -> ../Cellar/python@3.9/3.9.6/bin/pip3
admin@gw-mac ~ %
admin@gw-mac sample-fastapi % ls -la /opt/homebrew/Cellar/python@3.9/3.9.6/
Frameworks/               INSTALL_RECEIPT.json      Python\ Launcher\ 3.app/  bin/                      libexec/
total 64
drwxr-xr-x  13 admin  admin    416 Sep  5 09:23 .
drwxr-xr-x   3 admin  admin     96 Sep  5 09:23 ..
drwxr-xr-x   3 admin  admin     96 Jun 28 17:57 .brew
drwxr-xr-x   3 admin  admin     96 Jun 28 17:57 Frameworks
drwxr-xr-x   3 admin  admin     96 Jun 28 17:57 IDLE 3.app
-rw-r--r--   1 admin  admin   2452 Sep  5 09:23 INSTALL_RECEIPT.json
-rw-r--r--   1 admin  admin  13925 Jun 28 17:57 LICENSE
drwxr-xr-x   3 admin  admin     96 Jun 28 17:57 Python Launcher 3.app
-rw-r--r--   1 admin  admin  10140 Jun 28 17:57 README.rst
drwxr-xr-x  15 admin  admin    480 Sep  5 09:23 bin
drwxr-xr-x   3 admin  admin     96 Jun 28 17:57 lib
drwxr-xr-x   4 admin  admin    128 Jun 28 17:57 libexec
drwxr-xr-x   3 admin  admin     96 Jun 28 17:57 share
admin@gw-mac sample-fastapi % 
admin@gw-mac sample-fastapi % ls -la /opt/homebrew/lib/                    

total 0
drwxrwxr-x  22 admin  admin  704 Sep  5 09:24 .
drwxr-xr-x  31 admin  admin  992 Sep  4 06:12 ..
-rw-r--r--   1 admin  admin    0 Sep  4 06:24 .keepme
lrwxr-xr-x   1 admin  admin   39 Sep  4 06:24 libgdbm.6.dylib -> ../Cellar/gdbm/1.20/lib/libgdbm.6.dylib
lrwxr-xr-x   1 admin  admin   33 Sep  4 06:24 libgdbm.a -> ../Cellar/gdbm/1.20/lib/libgdbm.a
lrwxr-xr-x   1 admin  admin   37 Sep  4 06:24 libgdbm.dylib -> ../Cellar/gdbm/1.20/lib/libgdbm.dylib
lrwxr-xr-x   1 admin  admin   46 Sep  4 06:24 libgdbm_compat.4.dylib -> ../Cellar/gdbm/1.20/lib/libgdbm_compat.4.dylib
lrwxr-xr-x   1 admin  admin   40 Sep  4 06:24 libgdbm_compat.a -> ../Cellar/gdbm/1.20/lib/libgdbm_compat.a
lrwxr-xr-x   1 admin  admin   44 Sep  4 06:24 libgdbm_compat.dylib -> ../Cellar/gdbm/1.20/lib/libgdbm_compat.dylib
lrwxr-xr-x   1 admin  admin   38 Sep  4 06:24 liblzma.5.dylib -> ../Cellar/xz/5.2.5/lib/liblzma.5.dylib
lrwxr-xr-x   1 admin  admin   32 Sep  4 06:24 liblzma.a -> ../Cellar/xz/5.2.5/lib/liblzma.a
lrwxr-xr-x   1 admin  admin   36 Sep  4 06:24 liblzma.dylib -> ../Cellar/xz/5.2.5/lib/liblzma.dylib
lrwxr-xr-x   1 admin  admin   52 Sep  4 06:24 libmpdec++.2.5.1.dylib -> ../Cellar/mpdecimal/2.5.1/lib/libmpdec++.2.5.1.dylib
lrwxr-xr-x   1 admin  admin   48 Sep  4 06:24 libmpdec++.3.dylib -> ../Cellar/mpdecimal/2.5.1/lib/libmpdec++.3.dylib
lrwxr-xr-x   1 admin  admin   42 Sep  4 06:24 libmpdec++.a -> ../Cellar/mpdecimal/2.5.1/lib/libmpdec++.a
lrwxr-xr-x   1 admin  admin   46 Sep  4 06:24 libmpdec++.dylib -> ../Cellar/mpdecimal/2.5.1/lib/libmpdec++.dylib
lrwxr-xr-x   1 admin  admin   50 Sep  4 06:24 libmpdec.2.5.1.dylib -> ../Cellar/mpdecimal/2.5.1/lib/libmpdec.2.5.1.dylib
lrwxr-xr-x   1 admin  admin   46 Sep  4 06:24 libmpdec.3.dylib -> ../Cellar/mpdecimal/2.5.1/lib/libmpdec.3.dylib
lrwxr-xr-x   1 admin  admin   40 Sep  4 06:24 libmpdec.a -> ../Cellar/mpdecimal/2.5.1/lib/libmpdec.a
lrwxr-xr-x   1 admin  admin   44 Sep  4 06:24 libmpdec.dylib -> ../Cellar/mpdecimal/2.5.1/lib/libmpdec.dylib
drwxr-xr-x   7 admin  admin  224 Sep  5 09:23 pkgconfig
drwxr-xr-x   3 admin  admin   96 Sep  4 06:25 python3.9
admin@gw-mac sample-fastapi % 
admin@gw-mac sample-fastapi % ls -la /opt/homebrew/lib/python3.9/site-packages/
_distutils_hack/              pip/                          pkg_resources/                setuptools-57.0.0.dist-info/  wheel-0.36.2.dist-info/
total 8
drwxr-xr-x  11 admin  admin   352 Sep  5 09:23 .
drwxr-xr-x   3 admin  admin    96 Sep  4 06:25 ..
drwxr-xr-x   5 admin  wheel   160 Sep  5 09:23 _distutils_hack
-rw-r--r--   1 admin  wheel   152 Sep  5 09:23 distutils-precedence.pth
drwxr-xr-x   8 admin  wheel   256 Sep  5 09:23 pip
drwxr-xr-x  11 admin  wheel   352 Sep  5 09:23 pip-21.1.3.dist-info
drwxr-xr-x   7 admin  wheel   224 Sep  5 09:23 pkg_resources
drwxr-xr-x  41 admin  wheel  1312 Sep  5 09:23 setuptools
drwxr-xr-x  12 admin  wheel   384 Sep  5 09:23 setuptools-57.0.0.dist-info
drwxr-xr-x  13 admin  wheel   416 Sep  5 09:23 wheel
drwxr-xr-x  11 admin  wheel   352 Sep  5 09:23 wheel-0.36.2.dist-info
admin@gw-mac sample-fastapi % 
```


# 3. Install tree and jq command

```sh
admin@gw-mac sample-fastapi % brew install tree
==> Downloading https://ghcr.io/v2/homebrew/core/tree/manifests/1.8.0
######################################################################## 100.0%
==> Downloading https://ghcr.io/v2/homebrew/core/tree/blobs/sha256:b9d1925b5b306e098
==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256
######################################################################## 100.0%
==> Pouring tree--1.8.0.arm64_big_sur.bottle.tar.gz
🍺  /opt/homebrew/Cellar/tree/1.8.0: 8 files, 158.5KB
admin@gw-mac sample-fastapi % 

admin@gw-mac sample-fastapi % which tree        

/opt/homebrew/bin/tree
admin@gw-mac sample-fastapi % which jq

/opt/homebrew/bin/jq
admin@gw-mac sample-fastapi % 
```

# Appendix
https://www.python.jp/install/macos/index.html
https://brew.sh/
