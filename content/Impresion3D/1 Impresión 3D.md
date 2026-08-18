---
title: Impresión 3D
tags:
  - Impresion
noteOrder: "1"
---
Tecnología o tecnica que permite la creación de solidos a partir de un diseño digital mediante la adicción de capas sucesivas de material, construyendo el objeto capa por capa en un proceso aditivo.

**Usos:**
- Prototipado
- Producción personalizada
- Creacion de componentes livianos o resistentes echos a la medida
- Reducción de costos
- Creación de formas complejas

# Como funciona
---
Necesitamos un modelo 3D ya sea usando un escaner o un **Software de modelado** o usando paginas como [Thinkgiverse](https://www.thingiverse.com) o [Printables](https://www.printables.com). 

El formato de archivo que necesitamos para trabajar con la impresora debe ser **.stl**, **.obj**, **.amf** o **.3mf**. Este archivo contiene el modelo en 3D del objeto que deseamos, pero es necesario *traducir* el solido en instrucciones de movimiento con las que alimentaremos la maquina, usando un **slicer** como [[Cura]] o **Ultimaker**. 

Dentro de este programa podemos configurar otros valores de impresión, por ejemplo, el porcentaje de relleno, utilizar soportes, configurar el grosor de las capas de impresion, velocidad de traslado, etc. 

Con el **slicer** transformaremos el archivo del objeto 3D en un archivo de tipo **.gcode** que contiene todas las instrucciones de impresión.

Con esto podemos llevar el archivo a la impresora, donde la maquina seguirá las instrucciones para depositar el filamento, empujandolo por el extrusor para generar cada capa del solido.

Una vez finalizada la impresion puedes someter el objeto a procesos de [[Post Procesado]] como lijado, pintado, etc.



