---
title: Pi Pico
tags:
  - hardware
  - Raspberry
noteOrder: "3"
---
La Raspberri Pico **NO es un microcomputadora.** Es un **microcontrolador**, similar a un Arduino, pero mucho más potente y con lógica de 3.3V. No ejecuta un sistema operativo completo como Linux; en su lugar, corre un solo programa en bucle (bare-metal).

Es el primer dispositivo de la familia Raspberry Pi, que esta pensado para trabajar directamiente leyendo sensores, controlando motores, manejando luces y comunciandoce con otros dispositivos.

# Funcionamiento
---
Al no tener sistema operativo, es necesario ca rgarle un programa a la placa, el cual correra en bucle activando sus pines de entrada y de salida.

## Especificaciones (Chip RP2040)

| **Componente**       | **Especificación**                                                       |
| -------------------- | ------------------------------------------------------------------------ |
| **Microcontrolador** | RP2040 (Diseño propio de Raspberry Pi)                                   |
| **Procesador**       | ARM Cortex-M0+ de doble núcleo a 133 MHz                                 |
| **Memoria RAM**      | 264 KB de SRAM en el chip                                                |
| **Almacenamiento**   | 2 MB de memoria Flash integrada                                          |
| **Pines GPIO**       | 26 pines multifunción (3 de ellos con soporte analógico/ADC)             |
| **Periféricos**      | 2 × UART, 2 × controladores SPI, 2 × controladores I2C, 16 × canales PWM |
| **Energía**          | Funciona entre 1.8V y 5.5V                                               |


# Pinout
---

<p align="center"> <img src="Picopinout.svg" alt="Picopinout"> </p>

# Modelos
---
- **Pico (Original):** La placa base verde. Sin conectividad inalámbrica y sin pines soldados (viene con los agujeros para que tú mismo sueldes los headers o la montes directamente sobre otra placa).
    
- **Pico H (Headers):** Es idéntica a la original, pero ya trae los pines metálicos (headers) soldados de fábrica, lista para conectarse a una protoboard. También incluye un conector de depuración (debug) pre-soldado.
    
- **Pico W (Wireless):** Incluye un chip de red Infineon (CYW43439) visible como un cuadrado metálico en la placa. Esto le otorga conectividad Wi-Fi 4 (802.11n) y Bluetooth 5.2. Excelente para proyectos de IoT o telemetría.
    
- **Pico WH:** La combinación de las dos anteriores: incluye el módulo inalámbrico (Wi-Fi/Bluetooth) y los pines ya soldados de fábrica.
    
- **Pico 2 (Lanzada en 2024):** Utiliza el nuevo chip **RP2350**. Tiene más memoria, mayor velocidad (150 MHz) y una arquitectura dual única que te permite elegir entre usar núcleos ARM Cortex-M33 o núcleos RISC-V.


<p align="center"> <img src="PicoVers.jpeg" alt="PicoVers"> </p>


# Como trabajar con ella?
---

## El botón BOOTSEL

La Pico no necesita programadores externos. Su chip tiene grabado de fábrica un modo de almacenamiento masivo. Solo necesita un archivo de flasheo:
[Pico](https://micropython.org/download/rp2-pico/rp2-pico-latest.uf2) | [Pico W](https://micropython.org/download/rp2-pico-w/rp2-pico-w-latest.uf2) | [Pico 2](https://micropython.org/download/RPI_PICO2/RPI_PICO2-latest.uf2) | [Pico 2 W](https://downloads.raspberrypi.com/micropython/mp_firmware_unofficial_latest.uf2)

El proceso de bootsel es el siguiente:
1. Desconecta la Pico del cable USB.
2. Mantén presionado el botón blanco **BOOTSEL**.
3. Conécta a la PC por USB y suelta el botón un segundo después.
4. Aparecerá en el sistema como una memoria USB llamada `RPI-RP2`.
5. Arrastras tu archivo `.uf2`

El ecosistema de la Pico es muy flexible y soporta varios lenguajes dependiendo de la complejidad de tu proyecto.

1.  **MicroPython (Prototipado rápido):** Es la forma más sencilla de empezar. MicroPython es una versión optimizada de Python 3 para microcontroladores. Ver [[7 MicroPython]]

2. **C / C++ (Máximo rendimiento):** Si estás haciendo proyectos que requieren sincronización perfecta (como leer encoders a alta velocidad) o necesitas exprimir al máximo el hardware, usar el SDK en C/C++ es la mejor opción.

3. **CircuitPython:** Un fork de MicroPython mantenido por Adafruit. Es ideal si planeas usar el catálogo de sensores de Adafruit, ya que tienen librerías listas para usar estilo  ***plug-and-play*** para casi cualquier componente que quieras conectar.

# Hola Mundo
---

El equivalente al "Hola Mundo" es hacer parpadear el LED que viene integrado en la placa.
Para esto podemos hacer uso de diferentes librerias, un ejemplo usando la libreria *machine* (ver [[7 MicroPython]]) es el siguiente

``` Python
from machine import Pin
import time

# Configura el LED integrado como un pin de salida
# Nota: Usa 'LED' para la Pico W. Si tienes la Pico original (sin Wi-Fi), cambia 'LED' por el número 25.
led = Pin('LED', Pin.OUT)

# El "Super Loop" infinito
while True:
    led.value(1)      # Enciende el LED (envía voltaje)
    time.sleep(0.5)   # Espera medio segundo
    led.value(0)      # Apaga el LED (corta el voltaje)
    time.sleep(0.5)   # Espera medio segundo
``` 

De forma mas simple es usando la libreria **picozero**, que cuenta con una funcion especifica para este "Hola mundo"
``` Python
from picozero import pico_led

pico_led.blink()
``` 

### ¿Cómo probarlo?

1. Abre tu IDE ([[6 Thonny]]).
2. Conecta la Pico por USB.
3. Pega el código y presiona "Run" (Ejecutar).


>[!faq] Callout
>Para que el programa se ejecute solo cada vez que conectes la Pico a cualquier fuente de poder (como una batería o un cargador de celular), debes guardar el archivo directamente en la placa con el nombre exacto de **`main.py`**. El intérprete de MicroPython siempre busca ese archivo al arrancar.

# Troubleshooting
---

Si la computadora no detecta la Pico, sigue este diagnóstico:

1. **La trampa del cable** 
   El 90% de las veces, estás usando un cable USB que _solo transfiere energía_ y no tiene pines de datos. 
   **La solución:** Cambia el cable.
    
2. **Verificación a bajo nivel**
    - Ejecuta `sudo dmesg -w` y conecta la placa. Si el kernel de Linux no imprime nada nuevo, o tira un `error -71 (unable to enumerate)`, es un fallo eléctrico/físico entre el cable, el puerto de tu laptop, o el puerto micro-USB de la placa.
    - Si usas un Hub USB-C moderno, a veces estos fallan al traducir el protocolo USB antiguo (Full-Speed) de los microcontroladores. Intenta conectarla directo a la PC o usar un Hub USB 2.0 antiguo.
        
3. **Permisos de Puerto Serie (Error 13):**
    - Si ves la placa en `lsusb`, pero [[6 Thonny]] te dice *Permission denied*, tu usuario de Linux no tiene permisos para hablar con los puertos de hardware (`/dev/ttyACM0`).
    - **Solución**: Ejecuta `sudo usermod -a -G dialout $USER`, y luego reinicia tu computadora.