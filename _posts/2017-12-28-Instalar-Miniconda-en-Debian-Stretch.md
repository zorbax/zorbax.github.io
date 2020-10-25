---
title: Instalar Miniconda3 en Debian Stretch
date: 2017-12-28T22:34:02.000Z
categories: [blog]
tags: [python, conda, debian]
---

**Actualización: 16 de julio de 2020**

En lo personal me gusta instalar Miniconda ya que es una versión
más ligera de Anaconda, incluye python y conda, principalmente. 

Para instalar en una ubicación personalizada utilizamos la opción `-p` del instalador.

```
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
mkdir -p $HOME/bin/miniconda3
bash Miniconda3-latest-Linux-x86_64.sh -b -p $HOME/bin/miniconda3
```
Agregamos los ejecutables que viene con miniconda al $PATH

```
cat <<EOF >> $HOME/.bashrc

export PATH=$HOME/bin/miniconda3/bin:$PATH

EOF
```
Recargamos el $PATH

```
source $HOME/.bashrc
```

En terminal para obtener la información correspondiente a nuestro
entorno base de conda.
```
conda info
```

Actualizamos conda a la nueva versión, si es que la hay, disponible para conda.
```
conda update conda
```

Agregamos algunos canales útiles:

```
cat <<EOF >> $HOME/.condarc
channels:
  - conda-forge
  - bioconda
  - r
  - defaults
EOF
```

Para una experiencia más rápida podemos utilizar Mamba, la cual es una 
reimplementación de conda en C++

```
conda install -yc conda-forge mamba
```

A partir de ahora podemos usar **conda** con la rapidez de **mamba** para instalar todos los paquetes necesarios.

```
mamba update --all
```
