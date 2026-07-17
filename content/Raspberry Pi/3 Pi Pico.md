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

El ecosistema de la Pico es muy flexible y soporta varios lenguajes dependiendo de la complejidad de tu proyecto.

## 1. MicroPython (Prototipado rápido)

Es la forma más sencilla de empezar. MicroPython es una versión optimizada de Python 3 para microcontroladores.

- **Herramienta:** **Thonny IDE**. Es ligero y viene con soporte nativo para la Pico. Te permite ver la consola (REPL) en tiempo real.
    

## 2. C / C++ (Máximo rendimiento)

Si estás haciendo proyectos de robótica avanzada que requieren sincronización perfecta (como leer encoders a alta velocidad) o necesitas exprimir al máximo el hardware, usar el SDK en C/C++ es la mejor opción.

- **El entorno:** Existe una extensión oficial de Raspberry Pi para VS Code que automatiza casi toda la instalación del SDK, la compilación de los archivos `.uf2` y la configuración del entorno.
    

## 3. CircuitPython

Un fork de MicroPython mantenido por Adafruit. Es ideal si planeas usar el enorme catálogo de sensores de Adafruit, ya que tienen librerías listas para usar (plug-and-play) para casi cualquier componente físico que le quieras conectar.

## Hola Mundo

El equivalente al "Hola Mundo" en el desarrollo de microcontroladores es hacer parpadear el LED que viene integrado en la placa (_Blink_).

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

### ¿Cómo probarlo?

1. Abre tu IDE (Thonny).
2. Conecta la Pico por USB.
3. Pega el código y presiona "Run" (Ejecutar).


>[!faq] Callout
>Para que el programa se ejecute solo cada vez que conectes la Pico a cualquier fuente de poder (como una batería o un cargador de celular), debes guardar el archivo directamente en la placa con el nombre exacto de **`main.py`**. El intérprete de MicroPython siempre busca ese archivo al arrancar.

