# Unidad 6

## Bitácora de proceso de aprendizaje

### Actividad 1

Obra 1: Flow Field Lines

<img width="798" height="790" alt="image" src="https://github.com/user-attachments/assets/2bae44a6-7c16-438d-a71a-dd9d248c8d9d" />

Composición
La imagen está llena de líneas que cubren todo el espacio, sin dejar zonas vacías importantes. No hay un punto focal único, sino que todo el plano tiene relevancia.
Densidad
Hay zonas más densas que otras. Algunas áreas tienen muchas líneas juntas y otras están más abiertas.
Dirección del movimiento
Las líneas siguen direcciones curvas, como si estuvieran guiadas por un flujo invisible.
Color
Generalmente usa una paleta limitada (pocos colores), lo que hace que el patrón sea más claro y elegante.
Ritmo
Se genera un ritmo visual por la repetición de líneas, pero con pequeñas variaciones en dirección.
Repetición y variación
Las líneas se repiten, pero nunca son iguales. Cada una cambia ligeramente su trayectoria.

Obra 2: Fidenza


<img width="1565" height="900" alt="image" src="https://github.com/user-attachments/assets/8ed9278e-6399-428d-b110-757c15ed0890" />


Composición
Está organizada en bloques o estructuras, pero con formas curvas que rompen la rigidez.
Densidad
Algunas zonas son muy compactas y otras más abiertas, generando contraste.
Dirección del movimiento
Las formas parecen fluir en diferentes direcciones, como si fueran caminos o circuitos.
Color
Usa combinaciones de colores armónicas, a veces suaves, a veces contrastantes.
Ritmo
Hay repetición de formas, pero con cambios en tamaño y orientación.
Repetición y variación
Ninguna figura es igual, pero todas siguen una “familia” visual.


Creo que la pieza está construida a partir de un sistema basado en campos de flujo (flow fields), donde cada elemento visual (líneas o formas) sigue direcciones definidas por un campo generado con ruido como Perlin noise.

Este sistema probablemente funciona así:

Se genera un campo de vectores donde cada punto del espacio tiene una dirección.
Muchas “partículas” o líneas se mueven siguiendo esas direcciones.
Cada partícula tiene pequeñas variaciones en velocidad, longitud o curvatura para evitar que todas sean iguales.
Se utilizan reglas de repetición con variación para crear patrones complejos.

Además, el sistema puede incluir:

Cambios de color basados en posición o tiempo
Límites espaciales que definen la composición
Control de densidad para que algunas zonas tengan más elementos que otras

## Bitácora de aplicación 

### Actividad 2
### ¿Qué es un agente autónomo?

Un agente autónomo es una entidad que puede moverse y tomar decisiones por sí misma dentro de un sistema. No sigue un movimiento predefinido, sino que responde a su entorno a partir de ciertas reglas.
En lugar de controlar directamente su posición, se le asignan comportamientos. Por ejemplo, puede seguir un objetivo, evitar obstáculos o reaccionar a la presencia del mouse.

En este sentido, el agente no ejecuta una animación fija, sino que actúa en función de lo que percibe.

### ¿Qué es una steering force?

Una steering force es una fuerza que se utiliza para guiar el movimiento de un agente hacia un comportamiento específico.
A diferencia de una fuerza física simple, una steering force está asociada a una intención, como acercarse a un punto, alejarse de algo o moverse de forma alineada con otros agentes.
Estas fuerzas permiten construir comportamientos más complejos a partir de reglas simples de movimiento.

Diferencia entre una steering force y fuerzas como la gravedad
Las fuerzas físicas como la gravedad, el viento o la fricción son fuerzas externas que afectan a todos los objetos de manera uniforme y constante.

### Por ejemplo:

-La gravedad siempre actúa hacia abajo.
-El viento empuja en una dirección determinada.
-La fricción reduce la velocidad.

Estas fuerzas no dependen del contexto ni del objetivo del objeto.

En cambio, una steering force depende del comportamiento que se quiere lograr. Puede cambiar constantemente según la situación del agente y su entorno.

### Por ejemplo:

Una fuerza de tipo steering puede hacer que una partícula siga el mouse.
Otra puede hacer que huya si está demasiado cerca.
¿Por qué estas ideas son útiles para diseñar comportamiento visual?

Estas ideas permiten diseñar sistemas en los que el comportamiento emerge a partir de reglas, en lugar de definir cada movimiento de manera manual.

### Esto es útil porque:

Permite crear animaciones más naturales y orgánicas.
Hace posible que múltiples elementos interactúen entre sí de forma coherente.
Facilita la generación de sistemas complejos a partir de reglas simples.

En lugar de animar directamente cada elemento, se diseñan las condiciones bajo las cuales se mueven. Esto hace que el resultado sea más dinámico, impredecible y adaptable.


## Bitácora de reflexión
