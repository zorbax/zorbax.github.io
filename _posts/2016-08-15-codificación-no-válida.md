---
title: Codificación no valida
date: 2016-08-15T10:54:18.000Z
categories: [blog]
tags: [bash, debian]
---

Un detalle bastante molesto y bastante común para mí es el error "Codificación no válida" generalmente al descomprimir archivos rar/zip, principalmente cuando el nombre contiene acentos, eñes y diéresis. Esto se debe a la que la codificación de descompresión es diferente a la codificación de origen. Por ejemplo: ``BÃ¤nd - Some T�tle.file``

Los archivos que tengo fueron comprimidos(?) en Güindos, utilizando la codificación latina ISO-8859-1 o la codificación ISO-8859-5, utilizada para alfabetos cirílicos que es de donde obtengo... bueno, no tengo por qué dar explicaciones.

Primeramente se instala ``convmv`` para convertir el archivo a la codificación correspondiente:

```bash
apt-get install convmv
```

Luego, buscamos los archivos que contengan alǵún caracter desconocido `?`, usando `xargs` ejecutamos `convmv` a la búsqueda.

```bash
find . -name '?' | xargs convmv -r --notest -f ISO-8859-1 -t UTF-8
```
