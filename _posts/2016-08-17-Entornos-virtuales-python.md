---
title: Entornos virtuales en *Python*
date: 2016-08-17T12:02:47.000Z
categories: [blog]
tags: [python, debian]
---

En Python es común utilizar diferentes versiones de un mismo paquete. Les menciono nos casos partículares utilizados en bioinformática: ``biom-format`` y ``matplotlib``. Puede ser que simplemente hagas *downgrade* o *upgrade* a la versión que desees cada vez que vayas a utilizar el programa, pero honestamente resulta un poco molesto porque luego no recuerdo qué versión necesita qué programa. La solución es instalar las dos o más versiones de la misma librería a fin de poder ejecutar cada programa con su respectiva dependencia. Para ello se utiliza los *entornos virtuales* o ``virtualenv``. En pocas palabras, un entorno virtual de Python es un espacio independiente en el que puedes instalar paquetes diferentes a los del sistema y te permite utilizar tantos entornos como aplicaciones tengas.

Para poder crear dichos entornos es necesario instalar la utilidad ``virtualenv``. Para Python 2.7 :

```bash
# Debian, Ubuntu

apt-get install virtualenv python-virtualenv
```

También es posible instalar virtualenv utilizando pip, el cual es un gestor de paquetes de Python:

```bash
#En caso de no tener previamente instalado pip
# apt-get install python-pip

pip install virtualenv

```

Normalmente todos los entornos virtuales los tengo en un sólo lugar: ``$HOME/bin/python/``. Para crear un *virtualenv* simplemente se ejecuta:

```bash
$ virtualenv $HOME/bin/python/my_project
```

Creo un link simbólico en la carpeta del programa que requiera la versión particular de la librería:

```bash
cd my_program
ln -s $HOME/bin/python/my_project .
```

El directorio my_project/ tiene la siguiente estructura:

```bash
my_project/ -> /home/zorbax/bin/python/my_project/
├── bin
├── include
│   └── python2.7 -> /usr/include/python2.7
├── lib
│   └── python2.7
│       ├── distutils
│       ├── encodings -> /usr/lib/python2.7/encodings
│       ├── lib-dynload -> /usr/lib/python2.7/lib-dynload
│       └── site-packages
└── local
    ├── bin -> /home/zorbax/bin/python/my_project/bin
    ├── include -> /home/zorbax/bin/python/my_project/include
    └── lib -> /home/zorbax/bin/python/my_project/lib
```

En el directorio ``bin/`` se encuentran los ejecutables necesarios para interactuar con el *virtualenv*. En ``include/`` se encuentran algunos archivos de cabecera de C (*.h) necesarios para compilar algunas librerías de Python. Y en ``lib/`` se encuentra una copia de Python así como un directorio llamado ``site-packages/`` en el cual se aloja el código fuente de los paquetes Python instalados en el virtualenv. Para activar el entorno virtual, se procesa el archivo ``bin/activate`` que se encuentra en la carpeta *my_project*:

```bash
██ zorbax@beatrix
██ ~
██ ┗(-_- )┓ $ source my_project/bin/activate


(my_project) ██ zorbax@beatrix
██ ~
██ ┗(-_- )┓ $
```

El prompt de la terminal indica que el virtualenv en my_project ya está activado y se procede a instalar las librerías necesarias en las versiones deseadas. Para ello se utiliza ``pip``:

```
(my_project)$ pip install my_library_version1.1.3
```

Al terminar la instalación estaremos utilizando la versión específica requerida para el programa.

El prompt de la terminal indica que el *virtualenv* está activado. Esto nos permitirá utilizar los paquetes instalados e instalar paquetes adicionales. Para desactivar un *virtualenv* porque se necesita trabajar en otro diferente se ejecuta el comando ``deactivate``. No es necesario ir a la carpeta del virtualenv para realizar la operación:

```
(my_project) ██ zorbax@beatrix
██ ~
██ ┗(-_- )┓ $ deactivate


El prompt de la terminal indica que el virtualenv ha sido desactivado. Si se utiliza demasiados entornos virtuales podría ser un poco confuso, pero para ese inconveniente podremos utilizar una extensión de ``virtualenv`` llamada ``virtualenvwrapper``, pero esa es otra historia.
