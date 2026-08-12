---
title: LAN Wake-up
tags:
  - PC
  - linux
  - Raspberry
noteOrder: "6"
---
Para lograr encender la PC de forma remota es necesario hacer una serie de configuraciones tanto en la PC como en un dispositivo externo que se quedará conectado 24/7 al módem local, funcionando como un portero que le enviará una señal de encendido a la computadora de escritorio.

# Configurar PC
---
## Optener la direccion MAC
Primero necesitamos conocer la direccion MAC del puerte de ethernet que tiene la PC, para esto solo necesitamos correr el comando

```Bash
ip a
```
Esto arrojará un listado de los adaptadores de red de la maquina. Debes de buscar la conexión por cable usualmente llamada enp3s0, enp4s0 o eth0

En mi caso el nombre encontrado fue `eno1` con un altname `enp10s0`, debajo de este nombre encontramos un renglón que dice `link/ether` seguido de 6 pares de caracteres alfanumericos separados por dos puntos ( `a1:b2:c3:d4:e5:f6`).

## Configurar WakeUp LAN
Ahora vamos a confirmar si la tarjeta de red tiene la función de *wakeup* habilitada. Corre este comando para instalar y ejecuta la herramienta:

```Bash
sudo apt install ethtool
sudo ethtool TU_INTERFAZ
```
Remplanza TU_INTERFAZ con el nombre que encontras del puerto, en este caso `eno1`

Esto te soltará un bloque de texto. Buscas dos líneas en específico:
- `Supports Wake-on:` Nos dice de qué es capaz la tarjeta de red.
- `Wake-on:` Nos dice qué modo está activado actualmente.

En nuestro caso tenemos el valor `pumbg`  para el `Support Wake-on`, indica todas las formas en que la tarjeta de red puede despertar.
Para `Wake-on` tenemos el valor de `g` significa que actualmente está configurada para reaccionar al *Magic Packet* **(la "g" viene de magic)**. Este es el estándar más seguro.

Con esto sabemos que el sistema operativo ya está configurado correctamente para dejar la tarjeta escuchando.

## Configurar BIOS
Hay que entrar a la BIOS del systema **(Encendiendo la PC mientras presionamos F2)**.
Una vez dentro, debemos de ir al apartado de configuracion avanzada, `AMP Configuration`.
>[!note] Las tarjetas madre modernas agrupan el Wake-on-LAN bajo el bus de comunicaciones PCI-E y tienen reglas estrictas de ahorro de energía.

Debemos de confiurar esta pantalla de la siguiente forma:
- **Power On by PCI-E:** Debes ponerlo en **Enabled**. La tarjeta de red (incluso si está integrada en la placa) utiliza el bus PCI-E para comunicarse con el procesador. Esta es la opción que activa el Wake-on-LAN.
- **ErP Ready:** Debes ponerlo en **Disabled**. Esta es una normativa europea de ahorro de energía. Si está activada, la fuente de poder corta absolutamente toda la electricidad al apagar la PC, dejando a la tarjeta de red sin la energía mínima necesaria para "escuchar" el paquete de *WakeUp*.
- **Max Power Saving:** Debes ponerlo en **Disabled**. Funciona igual que el ErP y puede interferir con la energía de los puertos.
- **Restore AC Power Loss / Power on By RTC:** Estas puedes dejarlas como están. La primera es para saber qué hacer si se va la luz y regresa, y la segunda es para encender la PC a una hora específica.

Guarda los cambios y sal. Permite que el sistema operativo inicie de forma normal una vez y luego apaga la computadora.

Puedes confirmar la nueva configuración observando la parte de atrás de la PC; el puerto donde está conectado el cable de ethernet debería tener un LED encendido o parpadeando aunque este apagada.
# Configurar Portero
---
Para el portero usaremos una raspberry pi zero, ya que es un dispositivo de bajo consumo que es facil de usar y comunicar con la PC.

## Configuración basica
Primero es necesario hacer la [[2 Configuración Básica]].

## Instalar wakeonlan
Conéctate por SSH a tu Raspberry Pi y ejecuta lo siguiente:

```Bash
sudo apt update
sudo apt install wakeonlan
```

Con esto ya puedes mandar el **Paquete Mágico** para encender la pc, con el siguiente comando (sustituye las letras por la direccion MAC real):

```Bash
wakeonlan AA:BB:CC:DD:EE:FF
```

Si todo está configurado correctamente, la terminal de la Raspberry te confirmará que el paquete fue enviado y tu computadora encenderá instantaneamente.

## Configurar la conexión remota
Como ultimo paso, vamos a instalar Tailscale ya que es fundamental para crear un túnel seguro que evite los bloqueos de red y el aislamiento de dispositivos.
Ejecuta este comando para descargar e instalar el script oficial de Tailscale:

```Bash
curl -fsSL https://tailscale.com/install.sh | sh
```

El proceso tomará uno o dos minutos. Cuando termine, sigue las instrucciones que te aparecen en la termina, deberas lanzar el servicio de talescale, y esto te entregara un enlace al cual debes acceder desde una computadora donde tengas activada tu cuenta de talescale, autorizando asi la nueva conección a la red virtual.

Con esto tendras asignada una dirección IP fija en talescale, con el que podras conectarte remotamente a la rasp.