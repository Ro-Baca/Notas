---
title: Thonny IDE
tags:
  - software
noteOrder: "6"
---

Thonny es un **Entorno de Desarrollo Integrado (IDE)** para Python diseñado específicamente para prototipado. Fue creado por la Universidad de Tartu (Estonia) y destaca por tener una interfaz limpia.

Su mayor fortaleza es ser el IDE estándar para trabajar con microcontroladores que ejecutan [[7 MicroPython]] como la familia Raspberry Pi Pico y los ESP32.

# Ventajas
---

- Trae su propia versión de Python 3 integrada, por lo que no tienes que lidiar con variables de entorno ni configuraciones complejas al instalarlo.
    
- Tiene una consola en la parte inferior  que se conecta directamente al microcontrolador. Puedes escribir comandos allí y el hardware los ejecutará en tiempo real.
- Te permite ver simultáneamente los archivos de tu computadora y los archivos guardados _dentro_ del microcontrolador, facilitando arrastrar, soltar y editar archivos remotamente.

# Instalación en Linux
---

Existen varias formas de instalar Thonny en Linux, pero para trabajar con hardware, la forma más recomendada es a través del gestor de paquetes `apt`.

>[!Warning]  Evita usar la versión de Flatpak para programar microcontroladores, ya que las aplicaciones Flatpak están "aisladas" y a menudo tienen problemas de permisos para ver los puertos USB seriales._


Abre la terminal y ejecuta:

```
sudo apt update
sudo apt install thonny
```

## Troubleshooting

### Error de permisos (Error 13: Permission denied)

En Linux, por razones de seguridad, los usuarios normales no tienen permiso para interactuar directamente con puertos de hardware (como `/dev/ttyACM0` o `/dev/ttyUSB0`).

Si Thonny muestra un error de "Permission denied" al intentar conectar una placa, debes agregar tu usuario al grupo `dialout`:

```
sudo usermod -a -G dialout $USER
```

>[!Note]  Reinicia el sistema despues de ejecutar el comando para que el cambio surta efecto.

