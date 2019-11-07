---
title: Cambiar la ubicación del Docker Root Dir
date: 2017-12-05T16:02:01.000Z
categories: [blog]
tags: [docker, debian]
---

El siguiente post es una guía para cambiar la ubicación de la carpeta que Docker tiene por default para almacenar
sus contenedores: `/var/lib/docker`.

La razón principal porque es práctico hacerlo es la falta de espacio en `/dev`. Estas instrucciones fueron probadas en Debian 9, supongo que funcionará
en cualquier otro sistema que utilice systemd. No tiene mayor complicación, sigue las instrucciones:

Lo primero que tenemos que hacer es modificar el script de inicio de Docker en el systemd. Como root abre el archivo con tu editor favorito.
`/lib/systemd/system/docker.service` y reemplaza `/path/to/docker` con la nueva ubicación que deseas, `/home/zorbax/bin/docker`, en mi caso:

```
FROM:
ExecStart=/usr/bin/dockerd -H fd://
TO:
ExecStart=/usr/bin/dockerd -g /path/to/docker -H fd://
```
Una vez editado el archivo hay que detener el servicio de docker:

```
# systemctl stop docker
```

Es importante asegurarse que el demonio de Docker no se está ejecutando. En el siguiente comando no debe de aparecer el proceso:

```
# ps aux | grep -i docker | grep -v grep
```

Reiniciamos el demonio `systemd` una vez que nos aseguramos que no se estaba ejecutando docker:

```
# systemctl daemon-reload
```

Ahora hay que crear el directorio que especificaste en el primer paso y opcionalmente
sincronizar los datos que tengas actualmente a la neuva ubicación:

```
# mkdir -p /home/zorbax/bin/docker
# rsync -aqxP /var/lib/docker/ /home/zorbax/bin/docker
```

Iniciamos el demonio de docker:
```
# systemctl start docker
```

Verificamos que docker se está ejecutando en el nuevo directori:

```
#  ps aux | grep -i docker | grep -v grep
root     27004  0.0  0.2 540456 45396 ?        Ssl  01:06   0:06 /usr/bin/dockerd -g /home/zorbax/bin/docker -H fd://
root     27014  0.0  0.0 383052 10416 ?        Ssl  01:06   0:01 docker-containerd -l unix:///var/run/docker/libcontainerd/docker-containerd.sock --metrics-interval=0 --start-timeout 2m --state-dir /var/run/docker/libcontainerd/containerd --shim docker-containerd-shim --runtime docker-runc
```

¡Listo!
