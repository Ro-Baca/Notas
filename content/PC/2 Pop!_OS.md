---
title: Pop!_OS
draft: false
tags:
  - PC
  - linux
noteOrder: "2"
---
# El sistema operativo
----
Pop! os es una distribución de Linux basada en Ubuntu, desarrollada y mantenida por el fabricante de computadoras estadounidense **System76**. 
Aunque esta diseñado para laptops, es posible usarla para cualquier tipo de computadora.

El entorno gráfico esta hecho con una version personalizada de **GNOME**  llamado COSMIC y sus ventajas son:
- Auto-tiling
- Workspaces
- Launcher con la tecla super

Cuenta con soporte tanto para **NVIDIA** como **AMD**, esta pensado para desarrolladores y profesionales STEM. 

Cuenta con la pop! shop donde puedes encontrar los packetes de software que quieras, de forma segura ya que pop! os usa flatpack.

https://system76.com/pop

## Comandos útilies de linux
---

``` Batch
sudo reboot # Reinica el sistema

sudo apt update _app_ # Actualiza _app_
sudo apt upgrade # Upgradea _app_

sudo apt install _app_ # Instala _app_
sudo apt remove --purge _app_ # Desinstalla _app_
sudo apt autoremove # Limpia cualquier archivo o dependencia sobrante 

sudo nano /PATH # Modifica o crea un archivo en el PATH
```

## Comandos de programas de terceros
---
``` Batch
glmark2 # Para ver un puntaje de renderizado de la pc

systemd-analyze # Para ver el tiempo de inicio del sistema

htop # Para ver el rendimiento del sistema

neofetch # Para ver informacion del sistema

sudo amdgpu_top --gui # Para ver una GUI con graficas de rendimiento vs tiempo
```

# Flatpack
---
Flatpak es un sistema universal para instalar y ejecutar aplicaciones. Funciona en casi cualquier distribución de Linux porque trae sus propias piezas necesarias y corre en un espacio seguro y separado del sistema principal.

Permite instalar aplicaciones y actualizarlas al margen del gestor de paquetes de la distribución. Las aplicaciones Flatpak se instalan al margen de los paquetes instalados por la distribución y no pueden interferir el software base.

Además estas aplicaciones se ejecutan en un entorno aislado  ([sandbox](https://en.wikipedia.org/wiki/Sandbox_\(computer_security\))) y cuentan con sus propio sistema de permisos; acceso al sistema de archivos, red, bluetooth, etc.

Todas estas aplicaciones se pueden encontrar en [Flathub](https://flathub.org/home) que hace las veces de repositorio oficial.

Para instalar una aplicación con Flatpak manualmente solo es necesario ejecutar el comando `flatpak install` indicando la URL de su referencia `.flatpakref`.`
``` Bash
flatpak install https://dl.flathub.org/repo/appstream/org.gimp.GIMP.flatpakref
```
En el repositorio Flathub se puede copiar la referencia `.flatpakref` de una aplicación utilizando su botón **INSTALL**.

## Trobleshooting

Para revisar las aplicaciones que tienes instaladas usando flatpack usa el comando.
```Bash
flatpak list
```
esto te regresara el **nombre**, **aplication id**, **version**, **branch** y **origin installation**

Si alguna aplicacion no esta funcionando como deberia puedes tratar de correr el programa desde la terminal, para poder ver el log de error que regresa.
```Bash
flatpak run ApplicationID
```

O como alternativa siempre puedes intentar reinstalar el paquete por si fallo alguna actualización.
```Bash
flatpak install --reinstall flathub ApplicationID
```

