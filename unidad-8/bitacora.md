# Unidad 8

## Bitácora de proceso de aprendizaje
### Actividad 1:

Utilizaré la herramienta de Blender, debido a que es en la que más conocimientos manejo actualmente. Estoy enfocado en el área de animación y pues el programa que más utilizo es este.

Referentes hay mucho, he visto ciudades que quedan muy bacanas, y otros paisajes de varios tutoriales en Youtube. Además, no es la primera vez que utilizo los nodo.

### Actividad 2

El sistema que decidí transferir es principalmente el de aleatoriedad o ruido procedural, combinado con elementos de sistemas de partículas y oscilación.
La idea es utilizar reglas generativas para construir automáticamente un entorno natural compuesto por montañas, agua, vegetación y flores.

- ¿Cómo funcionaba ese sistema en p5.js?

En p5.js, el ruido procedural (noise) se utiliza para generar variaciones orgánicas y evitar resultados completamente aleatorios o rígidos. Este sistema permite controlar posiciones, movimiento, deformaciones y distribución de elementos de manera natural.

Por ejemplo, un valor de ruido puede modificar:

la altura de un terreno,
la dirección de movimiento,
la densidad de partículas,
o la aparición de elementos en ciertas zonas.

Además, los sistemas de partículas permiten distribuir múltiples elementos automáticamente siguiendo reglas específicas, como posición, separación o densidad.

### Actividad 3:

-¿Qué componentes o módulos necesito aprender?

Para poder transferir el sistema procedural a Blender, necesito aprender principalmente herramientas relacionadas con Geometry Nodes y distribución procedural.

Los componentes más importantes son:

Noise Texture, para generar deformaciones orgánicas en el terreno;
Set Position, para modificar la geometría de las montañas;
ColorRamp y Map Range, para controlar máscaras y zonas de distribución;
Distribute Points on Faces, para generar puntos automáticamente sobre el terreno;
Instance on Points, para distribuir vegetación y objetos;
Collection Info, para usar colecciones completas de modelos como árboles, flores o rocas;
Scene Time, para animar el movimiento del agua;
y sistemas de separación por altura para evitar que la vegetación aparezca debajo del agua.

Más que aprender toda la herramienta, el objetivo fue entender cómo conectar estos nodos para construir reglas visuales y ambientales.

#### Prueba técnica 1: Generación procedural del terreno
-¿Qué hice?

Realicé una prueba donde un grid es deformado utilizando Noise Texture conectado a Set Position.

La intensidad del ruido modifica la altura de los vértices, generando montañas y variaciones naturales en el terreno.

También se utilizó ColorRamp para controlar mejor las zonas altas y bajas.

-¿Qué resuelve esta prueba?

Esta prueba resuelve la construcción procedural del paisaje.

Permite:

generar montañas automáticamente;
modificar la forma del terreno mediante parámetros;
crear variaciones orgánicas;
y controlar visualmente la topografía sin modelar manualmente.
¿Qué parte del sistema logré reconstruir?

Con esta prueba logré reconstruir:

el sistema de ruido procedural;
la deformación automática del entorno;
y el control paramétrico del terreno.

Esto representa la base estructural del paisaje.

#### Prueba técnica 2: Distribución procedural de vegetación
-¿Qué hice?

En esta prueba utilicé:

Distribute Points on Faces
e Instance on Points

para distribuir automáticamente flores y césped sobre el terreno.

También se creó un segundo grid que funciona como agua. La vegetación solo aparece en zonas cuya altura supera el nivel del agua.

Además, se añadieron máscaras usando Noise Texture y ColorRamp para controlar mejor las zonas donde aparecen los elementos.

-¿Qué resuelve esta prueba?

Esta prueba resuelve:

la generación automática de vegetación;
la distribución procedural basada en reglas;
y la relación entre agua y entorno.

También ayuda a que el paisaje se vea más natural y menos uniforme.

-¿Qué parte del sistema logré reconstruir?

Con esta prueba logré reconstruir:

sistemas de distribución procedural;
uso de partículas e instancias;
separación de zonas mediante máscaras;
y control ambiental basado en altura.

### Actividad 4: 

## Bitácora de aplicación 

### Actividad 5:

-Herramienta: Blender

-El sistema principal transferido fue el uso de:

Aleatoriedad / ruido
Distribución procedural
Sistemas generativos basados en campos

En p5.js estos sistemas se usaban para controlar movimiento, posición o comportamiento visual mediante ruido Perlin y reglas algorítmicas.

-La pieza fue pensada como un entorno cinematográfico procedural, similar a escenarios usados en:

videojuegos,
visualización ambiental,
cinemáticas,
fondos para animación,
renders conceptuales.

La idea es que funcione como una demostración visual para portafolio, mostrando generación procedural de naturaleza mediante Geometry Nodes.

-En p5.js, el ruido se utilizaba para generar variaciones dinámicas en posición, movimiento o comportamiento.

Por ejemplo:

mover partículas,
deformar formas,
crear flow fields,
controlar trayectorias.

En Blender, ese mismo principio se transfirió mediante Geometry Node.

-La pieza final consiste en:

un terreno procedural con montañas,
un sistema de agua independiente,
distribución procedural de:
flores,
vegetación,
control por altura para evitar generación bajo el agua,
variación mediante ruido procedural,
composición cinematográfica con cámara e iluminación.



La escena puede mostrarse mediante render animado o recorrido de cámara.

## Bitácora de reflexión
