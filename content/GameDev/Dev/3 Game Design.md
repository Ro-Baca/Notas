---
title: Game Design
noteOrder: "3"
tags:
  - Design
  - videojuego
---
Los juegos estan diseñados con el unico objetivo de ser jugados; tienen **reglas** con las que se explican los comportamientos esperados por parte de los jugadores, tambien se plantean **objetivos** que los jugadores deben completar; tambien tienen **interacciones** o **inputs** para interactuar e influenciar el juego.

>[!quote] Los juegos son motores de emociones.   Tynan Sylvester

El diseño es una disciplina creativa que busca la resolución de problemas. Existen diferentes tipos de diseño, pero comparten un conceptos basico: siempre esta orientado al usuario, buscando su comodidad o diversion.

# Basicos del Game Design
---
El diseñador esta encargado de crear la **experiencia de juego** para el jugador a traves del diseño de reglas, sistemas y mecanicas del juego.

> El *Game design* es un diseño de segunda orden.

> El *Game design* usa mecanicas para crear las emociones deseadas.

El atributo de todos los diseñadores es que cuentan con un alto grtado de curiosidad, siempre esta buscando nuevo conocimiento que puede ser util en el diseño.
## Toma de decisiones
La toma de decisiones es el atributo que diferencia los juego de otro elementos como las peliculas o la musica. Aprender a trabajar con una perspectiva de toma de decisiones es crucial para ser un buen diseñador de juegos.

## Game Mechanics & Sistemas
-  **Game part:** es cualquier parte del juego que es interactiva, en juegos de mesa incluso la caja es una parte del juego. Usualmente una *game part* tiene **mecánicas** usualmente dinamicas, son acciones que lis jugadores usan para poner el juego en movimiento. Las mecanicas son la parte mas critica del juego.
- **Input:** que tan facil o dificil es activar una mecanica.
- **Output:** el numero de elementos que un jugador puede conseguir tras usar una mecanica del juego.

Las mecanicas complejas representan *inputs* y *outputs* complejos y le presentan al jugador con mas decisiones, sin embargo los jugadores tiene resistencia mental y fisica limitadas; demasiados *Inputs* significa que los jugadores necesitan mas habilidad; mientras que demasiados *Outputs* pueden tener demaciados resultados, creando confución en la función de la mecanica o su proposito.

Las mecanicas complejas aumentan el valor del *gameplay* a traves de comportamientos mas dinamicos entre las mecanicas y los sistemas del juego. Mientras que mecanicas simples pueden ser usadas para evitar que los jugadores interactuen profundamente con las mecanicas.

Las mecanicas pueden estar conectadas con los *Outputs*, dandole a los jugadores mas valor por sus *Inputs*.

Mecanicas complicadas representan aumentar la carga mental del jugador, mas *Input* por menos *Output* y esto puede sentirce castigador en cada fallo del jugador.

> Los sistemas son una coleccion de mecanicas.

Una caracteristica relevante para definir el impacto de una mecanica en el juego es en sus parametros, que es la unidad mas pequeña de un juego, se pueden definir como **adjetivos**.

>[!example] El personaje A corre **lento**, El personaje B corre **rapido**.


## Roles en GD

- Programador: Comunmente un experto tecnico, encargado de codificar todos los elementos del arte y diseño en el motor del juego.
- Artista/modelador/animador: Encargados de crear el arte del juego;el arte de personajes, el arte de fondo, *riggers*, el arte de los modelos, animaciones, etc. Estan a cargo de dar una personalidad y apariencia única al juego. El arte y el diseño deben trabajar de la mano para tener un juego consistente en todo momento.
- Project Manager: Estan encargados de mantener el desarrollo del juego tan suave como sea posible, garantizando la entrega del producto en los tiempos estipulados y reduciendo el *crunch* (trabajar horas extras).
- Marketing: La primera linea entre el juego y el jugador, deben encargarse de que el juego llegue al publico objetivo y que el veneficio económico sea sostenible. El diseño afecta directamente el como el equipo de marketing puede presentar el juego.
- Musica/diseñador de sonido: La musica ayuda a conectar con el jugador, se encargan de diseñar la musica para crear la atmosfera deseada para el juego.

Aprender de otros roles te puede ayudar a comunicarte de forma mas efectiva con el resto de tu equipo.

## Especializaciones del Diseñador

- **Generalista:** es el rol mas común, se espera que conozca e interactue con todas las areas del diseño.
- **Gameplay:** se enfoca en diseñar y balancear la jugabilidad, mecanicas, etc.
- **System:** Analiza, crea, diagrama y comunica los complejos sistemas del juego. Debe tener un buen entendimiento de sistemas abstractos.
- **Contenido:** Tambien conocidos como LiveOps. Crean el contenido del sistema, llenandolo con los elementos especificos dentro de las restrtucciones del sistema.
	- **Nivel:** Un subtipo de contenido, crea los niveles paraque interactuen con el sistema y las mecanicas.
	- **Narrativa:**  Un subtipo de contenido, Crea la historia o la narrativa relacionada con el juego.
- **Tecnico:** Es el enlace entre el diseño y el codigo. Diseñan las herramientas para que los diseñadores puedan implementar el contenido. Permitiendo hacer el diseño dentro de las restricciones tecnicas.
- **UX/UI:** Trabajan con las mejores practicas para crear elementos accesibles, confiables, etc.

## Framework MDA
**Mechanics, Dynamics, Aestetics**

Este Framework define:
- **Mecanicas** como la parte interna del juego y la que esta en control del diseño.
-  **Dinamica** es el *gameplay*, el juego en movimiento. 
- **Aestetics** es la fantacía que los jugadores viven mientras estan en tu juego.

## Framework MGE
**Mechanics, Gameplay and Experience**

- **Mecanicas**, son acciones aisladas, al unirlas forman un sistema. El *game loop*.
- **Gameplay**, son las mecanicas en movimiento, generan varias permutaciones y conmutaciones.
- **Experiencia**, son las emociones que busca el juego, se generan a traves de las mecanicas. El jugador interactua con el **Gameplay** y vive las **Experiencias**.

# Proceso de pensamiento de GD
---
Una metodología que te permitira mejorar tus juegos al dividir el proceso de diseño en pasos iterativos es la siguiente:


![[GD Thinking.png]]

## Game Concept
Lo que quieres que sea el juego, y que quieres que provoque en los jugadores; esta es la parte mas creativa.

Para que sea un juego atractivo debes ser conciente de varias cosas para poder usar como ideas o referencias.

Al final, necesitas tener el concepto del juego y elementos como el **concept docuement**, **GDD**, **10 pager**, etc.

## Pilares del juego
Este paso es critico para establacer las expectativas del proyecto. Las caracteristicas de los pilaes incluyen:
- Listado de *Guidelines*, expectativas y restricciones.
- De 3 a 5 como basicos.
- Mas pilares representan mas restricciones y estructuras.
- Menos pilares representan menos guias, menos metas a cambio de mayor libbertad creativa.

Al final del proceso tendras el documento de pilares. 

Este proceso es iterativo, por lo que debes pivotar entre la definicion del concepto del juego y la creacion de los pilares; al final del proceso pondras un candado o *Lock*, lo que significa que no volveremos a cambiar lo definido hasta este punto.

## Idear los features
Utilizando lo definido anteriormente: el concepto, los pilares y las restricciones; Ahora debemos idear las caracteristicas o *Features* del juego, aterrizando las ideas en caracteristicas usables.

Al final de este paso tendras una idea para empujar al siguiente paso.

## Definir
En este paso llevamos dos procesos: 
1. Definir la idea, buscar por posibles problemas y definir los detalles del *feature* de forma iterativa.
2. Escribir las caracteristicas del feature en el **GDD**

Al final tendras un docimento conocido como el **Feature spec**.

## Prototipado
El nivel del prototipado depende del tamaño de tu juego. En el prototipo debemos crear, implementar y probar el *feature*. 

Si detectas algun error en las especificaciones y la implementación, necesita un cambio, debes tomarlo de regreso al principio del proceso hasta que el *feature* pasa el *testing*.

## Tecnicas de ideación
Algunas tecnicas que pueden ser utiles para generar ideas usables en el desarrollo del juego se presentan a continuación 
### Brainstorming
- Todos los participantes deben tener claro el problema a resolver y tener todo el contexto posible.
- Preparar un timepo limite (ej. 2 o 3 bloques de 15 minutos).
- Evitar el uso de "*lenguaje negativo*", busca siempre ideas asociativas.
- Es posible hacer el brainstorming de forma escrita en lugar de hablada.

### SCAMPER
**S**ustitute
**C**ombine
**A**dapt
**M**odify
**P**ut to another use
**E**liminate
**R**everse

Util para mejorar ideas o diseños existentes, aplicando una o mas de las letras 

### El modelo de los 3 Cerebros
Este metodo divide el cerebro en 3 secciones: **Cerebro primitivo o de lagartija, cerebro medio o emocional y cerebro nuevo o racional**.

- El cerebro de **lagartija**, se asigna para las necesidades básicas y regula el impulso de correr o pelear. Esta conectado directamente con el sistema nervioso, lo relacionamos con los impulsos de respuesta al peligro.
- El cerebro **emocional**, es lo conocemos comunmente como el "cerebro" aqui es donde se encuentra la mente, ayuda a la toma de decisiones usando las emociones. Aqui es donde vive la mente inconciente.  
- El cerebro **racional**, el cerebro pensante y esta a cargo de procesar la información para darle un significado. Es el cerebro mas lento y en ocaciones pasa la información a otro cerebro.

La intencion es alocar el diseño dependiendo del producto y el cerebro especifico para el cual se quiere diseñar:

El diseño visual de los niveles es para el cerebro **lagartija**, usa elementos como graficos y visuales para ser agradable para el usuario.

La capa de comportamiento de los niveles se concentra en el cerebro emocional; trabaja en que tan facil o dificil es para los jugadores el interactuar con el juego, desde las restricciones fisicas hasta las mecanicas del juego. Debe ser **efectivo**, **eficiente** y **satisfactorio**.

El nivel reflextivo esta relacionado con el cerebro racional; **este es el mas importante para el exito**. Los jugadores deben de refleccionar respecto a la conección del juego con su propia vida o su propia personalidad. Algunas herramientas que ayudan a esto son: Personalización, diferentes formas de ljugar el juego, reflexionar en experencias previas, usar sistemas reales, conocimiento de la perspectiva del jugador.

## Toma de dcisiones
### Las 5 fases de la toma de decisiones de un jugador
*Zach Miller* decribe que la toma de decisiones pasa a traves de 5 fases.

- **Before**
	¿ Qué estaba pasando en el momento antes de tomar la decision?
	Dependiendo de cuanta informacion tiene el jugador es como va a actuar.
- **Availability**
	Como es que el jugador sabe que una decision está disponible
- **Action**
	¿Como es que el jugador toma la decision?
- **Concecuences**
	¿Cuáles son las consecuencias de la decision?
- **Feedback**
	Como son comunicadas estas consecuancias al jugador.

## Decisiones automaticas VS Racionales
Los humanos no somos tan racionales como queremos creer, *Daniel Kahrseman* señala que temos dos sistemas de toma de decisiones; **automatico** para decisiones rapidas o reactivas y **Racional** o lenta donde se usan mas recursos para tomar decisiones.

Normalmente al tomar una decision usamos racionalidad limitada, usando las restrucciones de informacion que tenemos en ese momento.
Cuando adivinamos, sabemos que no tenemos toda la informacion por lo que usamos el sistema rapido.


















