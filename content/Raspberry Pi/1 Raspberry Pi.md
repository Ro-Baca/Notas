---
title: Raspberry Pi
tags:
  - Raspberry
  - hardware
  - linux
noteOrder: "1"
---
# Raspberry Pi

## Recursos Oficiales
Enlaces esenciales para configuración y documentación técnica.

* **Sitio Web Oficial:** [raspberrypi.com](https://www.raspberrypi.com/)
* **Documentación:** [Raspberry Pi Documentation](https://www.raspberrypi.com/documentation/)
* **Software:** [Raspberry Pi Imager](https://www.raspberrypi.org/software/) (Necesario para flashear las tarjetas SD).

---
## ¿Qué es?
La **Raspberry Pi** son una serie de SBC (Single Board Computers) y microcontroladores de bajo coste desarrollados en el Reino Unido por la [Raspberry Pi Foundation](https://www.raspberrypi.org).

Originalmente diseñada para la educación, su uso se ha expandido a la robótica, domótica, servidores caseros y prototipado industrial debido a su gran comunidad y flexibilidad.

> [!INFO] Diferencia Clave
> No todas las Raspberry Pi son iguales. Es vital distinguir entre los **SBC** (que corren Linux, como la Pi 4 o Zero) y los **Microcontroladores** (que corren código directo sin SO, como la Pico).

---

## Familias de Hardware
### Single Board Computers (SBC)
Son ordenadores completos. Tienen procesador, RAM, puertos USB y salida de video. Funcionan con un Sistema Operativo.

| Característica   | Raspberry Pi 4/5     | Raspberry Pi Zero 2 W  | Raspberry Pi Pico W     |
| :--------------- | :------------------- | :--------------------- | :---------------------- |
| **Tipo**         | SBC                  | SBC                    | Microcontrolador        |
| **SO**           | Linux                | Linux                  | Firmware                |
| **Voltaje GPIO** | 3.3V                 | 3.3V                   | 3.3V                    |
| **Uso ideal**    | Servidor, AI, Visión | IoT, Wearables, Robots | Sensores, Motores       |
| **Consumo**      | Alto (~600mA - 3A)   | Medio (~100mA - 400mA) | Muy bajo (~20mA - 90mA) |

### Microcontroladores
No tienen sistema operativo. Ejecutan un solo programa en bucle.

* **Raspberry Pi Pico / Pico W:** Basada en el chip RP2040.
    * **Uso:** Control de hardware en tiempo real, sensores, actuadores.
    * **Lenguajes:** C/C++, MicroPython, CircuitPython.
    * *Nota:* La versión "W" incluye WiFi y Bluetooth.

