---
title: Hello world!
date: 2016-08-10T23:31:23.000Z
categories: [blog]
tags: [bash]
---

He sido usuario GNU/Linux desde 2007. Inicialmente empecé con Mandriva, posteriormente con Ubuntu alternando entre Gnome y KDE, y a partir del 14 de Febrero de 2009 empecé a utilizar Debian. Tuve mi etapa de Cairo Dock, Compiz, Plasma, pero recientemente son fan de lo sobrio, por lo que MATE es mi entorno favorito desde 2012. Por qué tanto énfasis en las fechas, bueno, me he dado cuenta de que llevo varios años utilizando Linux y nunca he tenido el tiempo -ni las ganas- de compartir algo de lo aprendido. Bueno, nunca es tarde para empezar.

Buscando entre mis archivos más antiguos encontré mi *primer script*. Igual y fui yo, igual y fue Stackoverflow pero estas lineas fueron las primeras que ejecuté sabiendo qué hacía cada una de ellas.

```bash
#!/bin/bash
list=`ls | grep "7z"`

for i in $list
do
  7z x $i
done

exit 0
```
No era para tanto, bien pude haber ejecutado: ``for i in *7z; do 7z x $i; done``.
