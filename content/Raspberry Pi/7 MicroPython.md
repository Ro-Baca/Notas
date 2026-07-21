---
title: MicroPython
tags:
  - software
  - linux
noteOrder: "7"
---

MicroPython es una implementación ligera y eficiente de Python 3, diseñada específicamente para ejecutarse en microcontroladores y entornos con recursos muy limitados (poca memoria RAM y poco almacenamiento).

A diferencia de un script de Python normal que corre sobre el núcleo de Linux o Windows, **MicroPython se ejecuta en Bare-Metal**. Esto significa que el propio intérprete de MicroPython actúa como un mini "sistema operativo" que gestiona el hardware subyacente.

# ¿Cómo funciona?
---

Para usar MicroPython en una placa nueva (como un [[ESP32]] o una [[3 Pi Pico]]), el proceso consta de dos fases:

1. Primero debes "flashear" el intérprete de MicroPython en la placa (generalmente un archivo `.bin` o `.uf2`). Esto convierte a la placa en una máquina que entiende Python nativamente.
    
2. Una vez instalado, conectas la placa a tu PC y usas un entorno como [[6 Thonny]] para enviarle archivos de texto con extensión `.py`.
    

### El ciclo de arranque: `boot` y `main`

Cuando un microcontrolador con MicroPython recibe energía, siempre busca y ejecuta los archivos en este orden específico:

1. `boot.py`: Se ejecuta primero. Rara vez se modifica, pero sirve para configuraciones de muy bajo nivel (como iniciar el hardware de red o configurar el USB).
    
2. **`main.py`**: Es el archivo principal. Aquí es donde debe ir el código de tu proyecto. Si guardas tu programa con este nombre en la placa, se ejecutará automáticamente sin necesidad de estar conectada a una PC.
    

# Pros y Contras
---

El estándar histórico para microcontroladores ha sido C/C++. MicroPython ofrece una alternativa con ventajas y desventajas claras:

| **Pros**                                                                                                                                                       | **Contras**                                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **Prototipado ultra rápido:** No hay que esperar a que el código "compile". Escribes, guardas y se ejecuta al instante.                                        | **Menor rendimiento:** Al ser un lenguaje interpretado, es mucho más lento que C/C++. No es ideal para microsegundos estrictos.               |
| **El REPL (Consola interactiva):** Puedes enviar comandos en tiempo real al hardware (ej. encender un motor pulsando 'Enter') sin escribir un script completo. | **Consumo de memoria:** El propio intérprete de MicroPython ya ocupa una porción vital de la (poca) RAM y Flash del microcontrolador.         |
| **Sintaxis limpia y familiar:** Hereda la legibilidad de Python, ideal para análisis de datos, manipulación de texto o APIs de internet.                       | **Falta de librerías estándar:** No puedes hacer un `pip install` tradicional; solo soporta un subconjunto de la librería estándar de Python. |
    

# Librerias 
---
## El módulo `machine`
La magia de MicroPython radica en sus librerías específicas para hardware. La más importante es `machine`, que te da acceso directo a los pines físicos, buses I2C, SPI, y conversores analógicos.
