# Unidad 7

## Bitácora de proceso de aprendizaje
### Actividad 01: 

-El proyecto Word as Image de Ji Lee propone transformar palabras en imágenes utilizando únicamente sus propias letras. La clave está en que la palabra sigue siendo legible, pero al mismo tiempo adquiere una dimensión visual que refuerza su significado.

#### Ejemplos:

-Ejemplo 1: “Smile”
La palabra se organiza formando una sonrisa.
Las letras se curvan o distribuyen de manera que construyen visualmente la forma de una boca.
Esto hace que la palabra no solo se lea, sino que también se “vea” como una sonrisa.

-Ejemplo 2: “Moon”
Las letras se adaptan para sugerir la forma circular de la luna o sus fases.
La composición tipográfica imita directamente el objeto, facilitando una comprensión inmediata.

-Ejemplo 3: “Exit”
Una de las letras se desplaza fuera de la estructura de la palabra.
Este gesto visual representa la acción de salir, alineando forma y significado.

-Ejemplo 4: “Idea”
La palabra se transforma en una bombilla.
Las letras se reorganizan para construir este símbolo, que culturalmente está asociado al concepto de idea.

#### Manipulación tipográfica y significado

En estos ejemplos, la tipografía deja de ser solo un medio de lectura para convertirse también en imagen.
El significado se refuerza porque la forma visual comunica lo mismo que el texto, generando una doble lectura: una textual y otra visual.

Esta relación directa entre forma y contenido hace que el mensaje sea más claro, inmediato y memorable.

#### Propuestas propias

-Palabra 1: “Caída”
Las letras se disponen en diagonal descendente, como si estuvieran cayendo.
Algunas podrían estar más abajo que otras para enfatizar el movimiento.

-Palabra 2: “Silencio”
La letra “i” podría representar un dedo sobre la boca.
El resto de la palabra podría ser más delgado o tenue, reforzando la idea de ausencia de sonido.

-Palabra 3: “Explosión”
Las letras se separan desde el centro hacia afuera.
Algunas partes podrían fragmentarse o deformarse para sugerir impacto.

#### Elección

La palabra seleccionada es “Silencio”, porque permite trabajar con contraste, sutileza y ausencia.
Es un concepto que puede representarse tanto desde lo visual como desde lo interactivo, especialmente al relacionarlo con sonido.

## Bitácora de aplicación 

### Actividad 2

Actividad 02: Exploración de Matter.js
1) Conceptos fundamentales

Engine
Es el sistema que procesa la simulación. Calcula movimiento, colisiones y fuerzas en cada frame.

World
Es el espacio donde existen todos los objetos físicos. Funciona como contenedor de los cuerpos.

Bodies
Son los objetos físicos dentro del mundo. Tienen propiedades como masa, velocidad y fricción.

Constraint
Permite conectar cuerpos entre sí, como si fueran unidos por cuerdas o ligas.

MouseConstraint
Permite interactuar con los cuerpos usando el mouse, simulando manipulación directa.

2) Experimentos realizados

Se realizaron dos pruebas básicas integrando p5.js con Matter.js:

Experimento 1: múltiples cajas cayendo por gravedad sobre un suelo
Experimento 2: interacción con una caja mediante el mouse

Estos experimentos permitieron entender cómo funcionan las fuerzas, colisiones e interacción en el sistema.

(Código y evidencias incluidas en la entrega)

3) Comportamiento físico de interés

Para la palabra “Silencio”, interesa explorar un comportamiento donde:

Las letras inicialmente estén separadas o inestables
Luego puedan reorganizarse o mantenerse en equilibrio
El usuario pueda intervenir en su estado

La idea es que la palabra no sea estática, sino que refleje estados de estabilidad y perturbación.

### Actividad 03: Exploración de audio en p5.js
1) Experimentos

Experimento 1 — Amplitud
Se utilizó la amplitud del audio para modificar el tamaño de un objeto.
Resultado: el objeto cambia de tamaño de forma continua según el volumen.

Experimento 2 — Frecuencias (FFT)
Se analizaron los bajos para modificar el color.
Resultado: los cambios de color responden a golpes específicos del audio.

2) Datos y comportamiento
Amplitud: genera cambios continuos (suavidad, respiración visual)
Frecuencias: permiten detectar eventos puntuales (beats, golpes)
3) Aplicación al concepto

Para la palabra “Silencio”, la relación propuesta es:

Volumen bajo → estabilidad (la palabra se mantiene clara)
Volumen alto → perturbación (la forma se deforma o pierde claridad)

Esto crea un contraste entre ausencia y presencia de sonido, que es central en el concepto.

### Actividad 04: Integración inicial
1) Prueba inicial

Se desarrolló una prueba utilizando la letra “S” de la palabra “Silencio”.
La letra fue representada como un conjunto de puntos, permitiendo manipular su forma de manera flexible.

2) Parte construida

Se trabajó únicamente con la letra “S”, enfocándose en su estructura interna y comportamiento visual.

3) Propiedad manipulada

En lugar de usar físicas tradicionales, se trabajó con:

deformación de la forma
desplazamiento de puntos
dispersión controlada

Esto genera un efecto similar a vibración o inestabilidad.

4) Relación con el audio
Volumen bajo → la forma permanece estable
Volumen medio → aparece vibración
Volumen alto → la forma se deforma significativamente

Esto establece una relación directa entre sonido y transformación visual.

5) Evaluación

Aspectos que funcionaron:

La deformación ocurre directamente sobre la letra
Existe una relación clara entre audio y forma
La letra conserva legibilidad en estados de baja energía

Aspectos a mejorar:

No hay interacción física real (sin colisiones o gravedad)
La deformación es poco controlada
Solo se trabaja con una parte de la palabra
6) Relación con el significado

El comportamiento logrado se acerca al concepto de “silencio”:

El estado base es estable
El sonido introduce perturbación

Sin embargo, aún es necesario reforzar el contraste para que el concepto sea más evidente, por ejemplo aumentando la intensidad de la deformación o haciendo que la forma colapse en momentos de mayor sonido.


## Bitácora de reflexión


