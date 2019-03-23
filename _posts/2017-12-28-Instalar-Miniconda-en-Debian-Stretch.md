---
title: Instalar Miniconda2 en Debian Stretch
date: 2017-12-28T22:34:02.000Z
categories: [blog]
tags: [python, conda, debian]
---

wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh
mkdir -p $HOME/bin/miniconda2
bash Miniconda2-latest-Linux-x86_64.sh -b -p $HOME/bin/miniconda2

cat <<EOF >> $HOME/.bashrc

export PATH=$HOME/bin/miniconda2/bin:$PATH

EOF

source $HOME/.bashrc

$ conda info
finds the executable where you have just installed it. If you did add Anaconda or Miniconda to your PATH (the default option) you will have to supply its path explicitly.

It’s a useful habit to do:

$ conda update conda
with a fresh install. You can run the update command for any installed package, including conda itself. This intrinsic bootstrapping capacity makes conda very powerful. In fact, if you started with the Miniconda installation, you can expand it to the full Anaconda distribution with:

$ conda install anaconda
but that’s not the focus here.

What you do need to install is conda-build:

$ conda install conda-build
On Linux, you may also need to install patchelf.

$ conda install patchelf
