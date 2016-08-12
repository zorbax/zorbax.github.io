---
title: Hello world!
date: 2016-08-10T23:31:23.000Z
categories: [blog]
tags: [bash]
---

He sido usuario GNU/Linux desde 2007. Inicialmente utilicé Mandriva, posteriormente Ubuntu alternando entre Gnome y KDE, y a partir del 14 de Febrero de 2009 empecé a utilizar Debian, a excepción de un semestre que probé un *release* de Fedora (Verne). Tuve mi etapa de Conky, Cairo Dock, Compiz, Plasma, pero recientemente son fan de lo sobrio, por lo que MATE es mi entorno favorito desde 2014. Por qué tanto énfasis en las fechas, bueno, me he dado cuenta de que llevo varios años utilizando Linux y nunca he tenido el tiempo -ni las ganas- de compartir algo de lo aprendido. Bueno, nunca es tarde para empezar.

No pretendo hacer un tutorial, describir un pipeline, ni mucho menos explicar las cuestiones básicas de cada comando. La idea que tengo es compartir algunas utilidades y recomendaciones a la hora de usar herramientas GNU/Linux aplicadas a la Bioinformática. No soy especialista en ninguna rama de la computación, ni tengo educación formal en programación, por lo que mis recomendaciones quizá no sean las más estilizadas, pero funcionan. Todo lo aprendido ha sido de aquí y de allá. Buscando entre mis archivos más antiguos encontré mi *primer script*. Igual y fui yo, igual y fue Stackoverflow pero estas lineas fueron las primeras que ejecuté sabiendo qué hacía cada una de ellas.

```bash
#!/bin/bash
list=`ls | grep "7z"`

for i in $list
do
  7z x $i
done

exit 0
```
No era para tanto, bien pude haber ejecutado el loop para una lista utilizando el metacaracter *glob* (\*): ``for i in *7z; do 7z x $i; done`` en una sola linea. Lo interesante es que fue la primera vez que definí una variable como lista con la salida de dos comandos(``ls`` y ``grep``) y por cada elemento (``$i``) listado en esa variable-lista ejecuté ``7z`` para descomprimir dicho elemento.

```bash
#!/bin/bash

for i in File2.7z File4.7z file5.7z File4_.7z
do
  7z x $i
done
```
```bash
#!/bin/bash

for i in File{1..4}.7z
do
  7z x $i
done
```
```bash
#!/bin/bash
list="*txt"

for i in $list
do
  7z x $i
done
```
```bash
#!/bin/bash
ls *.xml > list

for i in `cat list`
do
  7z x $i
done
```
```bash
#!/bin/bash
for i in $(<list.txt);
do
  7z x $i
done
```
