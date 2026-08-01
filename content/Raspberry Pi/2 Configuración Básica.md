---
title: Configuración Básica
tags:
  - Raspberry
noteOrder: "2"
---
# Pasos Basicos
___

La RaspberryPi requiere instalarle un sistema operativo:

1. **Descarga Raspberry pi imager**
   En tu computadora, usas el software [Raspberry Pi Imager](https://www.raspberrypi.com/software/). Conecta tu tarjeta MicroSD o disco SSD y graba una imagen de Raspberry Pi OS. 

2. **Selecciona el hardware y SO** 
   Abre Raspberry Pi Imager y haz las siguientes selecciones:
   - **Choose Device:** Selecciona el dispositivo (Pi 5 / Pi Zero).
   - **Choose OS :** Selecciona el OS que desees (en _Raspberry Pi OS (Other)_ esta **Raspberry Pi OS Lite (64-bit)**. (La versión de 64 bits es la más recomendada para el procesador de la Pi 5).
   - **Choose Storage :** Selecciona tu tarjeta microSD.

3. **Configura los ajustes avanzados:**
   Haz clic en el botón de **Next** y el programa te preguntará si quieres aplicar ajustes de personalización, seleccion *Edit Settings*.
   En la pestaña **General**:
   - Configura un **nombre de usuario y contraseña**    
   - Configura tu **Wi-Fi** y el país.  
   - Ajusta tu zona horaria.
   
   En la pestaña **Services**: Marca la casilla para **Enable SSH**. Usa la opción de autenticación por contraseña. Esto te permitirá conectarte remotamente.
   
4. **Flashea**
   Guarda los ajustes y dale clic a **"Yes"** para comenzar a escribir en la memoria. Te saldrá una advertencia de que se borrarán todos los datos de la SD. Confirma y espera a que termine el proceso de escritura y verificación.
   
5. **Arranca tu Raspberry Pi**
   Saca la microSD de tu computadora, inserta en la Raspberry y conécta a la corriente.
   Dale un par de minutos para que arranque por primera vez, se conecte a tu Wi-Fi y configure las particiones.
   
6. **Conectate a la tarjeta**
   Por defecto, la Raspberry Pi transmite su nombre en la red local. Abre tu terminal y escribe: `ping -c 4 raspberrypi.local`. Si el comando responde, verás que traduce el nombre a una dirección IP (algo como `192.168.x.x`). Esa es la Pi.
   
   Si en el _Imager_ le configuraste un nombre de host, cambia *raspberrypi* per ese nombre.
   Como alternativa, puedes escanear la red usando el comando `sudo nmap -sn -n 192.168.1.0/24`
   
   Si nada de esto funciona, puedes usar una pantalla y conectarte directamene a la tarjeta para corroborar que la pre-configuracion se efectuó correctamente, usando el comando `sudo raspi-config`. Finalmente para saber la IP de la tarjeta solo es necesario el comando `hostname -I`.
   
   Cuando tengas la IP, puedes conectarte a la tarjeta usando `ssh tu_usuario@192.168.1.x` o alternativamente `tu_usuario@hostname.local` por ejemplo ` ssh ro@herb.local`

# Configurar Multiples redes
___

Para conectarte a multiples redes puedes usar otra herramienta **NetworkManager TUI**. Una vez que estés conectado por ssh, usa el comando `sudo nmtui`, esto abrirá una interfaz gráfica con la que podrás configurar la reed que desees.

Si es necesario puedes forzar un nuevo escaneo usando el comando 
```Bash
sudo nmcli device wifi rescan
```

Después puedes mostrar la lista de las redes encontradas usando 
``` Bash 
nmcli device wifi list
``` 
con esto puedes volver a ejecutar nmtui o conectar a la red directamente usando 
``` Bash
sudo nmcli device wifi connect "NOMBRE_DE_RED" password "CONTRASEÑA_DE_RED"
``` 

>[!note] Asegúrate de mantener las comillas `"` envolviendo tanto el nombre de la red como la contraseña. Esto es vital, sobre todo si alguno de los dos tiene espacios en blanco.

# Configuración manual
___

Si el Imager es incapaz de asignar los valores de configuracion avanzada, es necesario hacerlo de forma manual.

Una vez que el Imager termine de flashear (aunque no haya aplicado la configuración), retira y vuelve a insertar la tarjeta SD en tu computadora. Te aparecerá una partición nueva llamada `bootfs`.

## Crear un usuario
### Crear la contraseña
Para crear la contraseña del usuario, no podemos usar texto plano, requerimos un hash; abre la terminal y ejecuta:

``` Bash
openssl passwd -6
```

Te pedirá que escribas una contraseña (no se verá nada en la pantalla mientras tecleas). Al terminar, copia la cadena que te devolverá, debe empezar con `$6$`. 

### Crear el archivo de usuario
En la raíz de la partición `bootfs`, crea un archivo de texto llamado exactamente `userconf.txt`. Ábrelo y escribe el nombre de usuario que quieras, seguido de dos puntos (`:`), y luego pega el hash que copiaste. 
>[!Warning] No dejes espacios.
``` Bash
ro:$6$dfsfdskndndkcdscjsdkf kjdsnfsjk
```

Guarda y cierra el archivo

## Crear archivo de Red
Crea un archivo que contendrá todos los detalles de configuración de tu red
``` Bash
sudo nano mi-red.nmconnection
```

El archivo debe de tener:
``` toml
[connection]
id=Red1
uuid=7c4b4a58-4499-4d4b-bd81-0f3cc956350c
type=wifi
interface-name=wlan0

[wifi]
mode=infrastructure
ssid=NOMBRE_RED

[wifi-security]
key-mgmt=wpa-psk
psk=CONTRASEÑA

[ipv4]
method=auto

[ipv6]
method=auto
```

Y debes reemplazar los valores de **NOMBRE_RED** Y **CONTRASEÑA** 
Guarda y cierra el archivo.

Copia el archivo usando privilegios de administrador usando la ruta  real del archivo
``` Bash
sudo cp ~/Desktop/mi-red.nmconnection /media/tu_usuario/rootfs/etc/NetworkManager/system-connections/
```

Aplica el candado de seguridad 
``` Bash
sudo chmod 600 /media/ro/rootfs/etc/NetworkManager/system-connections/mi-red.nmconnection
```

## Habilitar SSH
Abre la partición `bootfs`, haz clic derecho en un espacio vacío y crea un archivo nuevo. Nómbralo exactamente `ssh` (todo en minúsculas y asegúrate de que no tenga extensión `.txt`). Déjalo completamente vacío. Esto le indica al sistema que debe abrir el acceso remoto en el primer arranque.

Una vez que apliques estas configuraciones, puedes expulsar la memoria SD, insertarla en tu Raspberry Pi Zero y conectarla a la corriente. Con esto, leerá la configuración de forma nativa y se conectará a tu Wi-Fi.