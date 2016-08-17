---
title: for-do-done
date: 2016-08-12T14:09:06.000Z
categories: [blog]
tags: [bash]
---

Buscando entre mis archivos más antiguos encontré mi *primer script*. No hackeé nada, no me conecté a la *deep web*, no hice nada espectacular, simplemente hice un loop para descomprimir archivos. Igual y fui yo, igual y fue Stackoverflow pero estas lineas fueron las primeras que ejecuté sabiendo qué hacía cada una de ellas.

```bash
#!/bin/bash
list=`ls | grep "7z"`

for i in $list
do
  7z x $i
done

exit 0
```
No era para tanto, bien pude haber ejecutado el loop para una lista utilizando el metacaracter *glob* (\*): ``for i in *7z; do 7z x $i; done`` en una sola linea. Lo interesante es que fue la primera vez que definí una variable como lista con la salida de dos comandos(``ls`` y ``grep``) y por cada elemento (``$i``) listado en esa variable-lista ejecuté ``7z`` para descomprimir dicho elemento. Con el tiempo aprendí que existen muchas maneras diferentes, pero la manera más simple es mejor, apelando un poco al principio de la Navaja de Ockham.

```bash
#!/bin/bash

#Si sólo con 4 archivos, pero son muy grandes y descomprimirlos
#uno por uno tomaría mucho tiempo.
#Útil con set de metagenomas o transcriptoma
for i in File2.7z File4.7z file5.7z File4_.7z
do
  7z x $i
done
```
```bash
#!/bin/bash

#Si tienes archivos seriados, como en el caso de un output
#de Illumina en el que se usaron identificadores consecutivos.
for i in File{1..4}.7z
do
  7z x $i
done
```
```bash
#!/bin/bash
list="*7z"

#Para todos aquellos archivos que tengan
#extensión 7z.
for i in $list
do
  7z x $i
done
```
```bash
#!/bin/bash
ls *.7z > list.txt

#Listar archivos, eviar a un archivo, abrie el archivo
#cada momento que se ejecuta el loop... No es lo más eficiente
#pero es una forma de hacerlo.
for i in `cat list.txt`
do
  7z x $i
done
```
```bash
#!/bin/bash
#En este caso el archivo no se abre con cat sino que
#"pasa" directamente como input al shell.
for i in $(<list.txt);
do
  7z x $i
done
```

Este tipo de loops es extremadamente útil, pero la característica principal que noto es que el *output* del comando ejecutado en cada *loop* es diferente al *input* y se genera automáticamente por el comando utilizado. Es decir, tengo un archivo ``reads.fasta`` el programa automáticamente generará ``reads.something.fasta``. Si tengo que definir el nombre del output y lo defino como ``command -i $i -o $i.something.fasta`` y mi ``$i`` es ``reads.fasta``, obtendré algo como ``reads.fasta.something.fasta``, que tendrá el resultado esperado del comando pero tendrá un nombre redundante.

Originalmente definía una variable que me permitiera obtener el nombre, empleando sustituciones en caso de que el nombre fuera muy largo:

```bash
name=`echo $i | cut -d\. -f1 | sed 's/blablabla//g'`
```

Posteriormente descubrí que era más práctico usar ``basename`` para obtener sufijos de los nombres de archivos. Más adelante les compartiré algunos ejemplos prácticos.

```bash
for i in list
do
  name=$(basename "$i" .fasta)
  command option something_else -i $i -o $name.output
done
```
