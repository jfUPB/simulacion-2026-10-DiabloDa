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

### Actividad 3: 

#### ¿Cómo está construido el campo de flujo?

El campo de flujo está construido como una grilla (cuadrícula) que divide el espacio en celdas.
En cada celda se almacena un vector que indica una dirección.

#### ¿Qué representa cada celda o vector del campo?

Cada celda representa una “instrucción de dirección”.
El vector almacenado en esa celda indica hacia dónde debería moverse un agente si se encuentra en esa posición del espacio.

-Es decir:

  No mueve directamente al agente
  Le da una guía de dirección

#### ¿Cómo usa un agente su posición para consultar el campo?

El agente toma su posición (x, y) y la traduce a la celda correspondiente dentro de la grilla.
Por ejemplo:

Divide su posición por el tamaño de cada celda (resolución)
Obtiene un índice dentro del arreglo del campo

De esta forma, sabe qué vector le corresponde según dónde está ubicado.

#### ¿Cómo se convierte el vector consultado en una decisión de movimiento?

El vector obtenido del campo se usa como una steering force.
El proceso es:

El agente obtiene el vector del campo
Ese vector se ajusta (por ejemplo, se multiplica por una magnitud)
Se aplica como fuerza al agente
Se suma a su aceleración
Esto modifica su velocidad y finalmente su posición

Así, el agente no se mueve directamente, sino que es influenciado por el campo.

#### Parámetros importantes del sistema:

-Resolución:
  -Define el tamaño de cada celda del campo.
  -Alta resolución (celdas pequeñas): movimiento más detallado y complejo.
  -Baja resolución (celdas grandes): movimiento más simple y uniforme.
  
-maxspeed:
  -Limita la velocidad máxima del agente.
  .Valores altos: movimiento más rápido y caótico.
  -Valores bajos: movimiento más suave.
  
-maxforce:
  -Limita la intensidad de la fuerza aplicada.
  -Valores altos: cambios de dirección bruscos.
  -Valores bajos: movimiento más fluido.
  
-Cantidad de agentes:
  -Define cuántos elementos interactúan con el campo.
  -Muchos agentes: mayor densidad visual.
  -Pocos agentes: composición más limpia.

#### Modificación realizada y efecto visual

Modificación: disminuí el valor de maxforce.

-Efecto:
El movimiento se volvió más suave y continuo. Los agentes tardan más en cambiar de dirección, lo que genera trayectorias más fluidas y menos abruptas.
Visualmente, el sistema se siente más orgánico, como si fuera un flujo natural (similar al agua o al viento).

#### ¿Qué tipo de movimiento produce este algoritmo?

Produce un movimiento continuo, fluido y direccional.
Los agentes parecen seguir corrientes invisibles, generando trayectorias curvas en lugar de líneas rectas o movimientos bruscos.

#### ¿Qué sensaciones visuales sugiere?

-Fluidez
-Organicidad
-Calma o suavidad (dependiendo de los parámetros)
-Complejidad emergente

También puede sugerir fenómenos naturales como:

-corrientes de agua
-viento
-humo

#### ¿En qué tipo de pieza musical podría funcionar bien?

Este tipo de sistema funcionaría bien con música que tenga continuidad y ritmo suave, por ejemplo:

música ambiental
electrónica suave
piezas instrumentales lentas

También podría adaptarse a música más intensa si se aumentan parámetros como velocidad y fuerza, generando un movimiento más caótico y energético.

### Actividad 4:

#### Reglas básicas del flocking

El sistema de flocking se basa en tres reglas simples que cada agente sigue de manera local:

#### Separación

La separación hace que un agente se aleje de los vecinos que están demasiado cerca.
Evita que los agentes se amontonen o colisionen.
Funciona como una fuerza de repulsión a corta distancia.

#### Alineación

La alineación hace que un agente ajuste su dirección para coincidir con la de sus vecinos cercanos.
Esto genera movimiento coordinado, donde muchos agentes parecen moverse como un grupo.

#### Cohesión

La cohesión hace que un agente se acerque al centro del grupo de vecinos.
Es una fuerza de atracción que mantiene unido al conjunto.

#### Parámetros que controlan estas reglas

Cada regla tiene parámetros que afectan su comportamiento:

-Peso de separación:
  Controla qué tan fuerte un agente evita a los demás.

-Peso de alineación:
  Define cuánto intenta coincidir con la dirección de sus vecinos.

Peso de cohesión:
  Determina qué tan fuerte es la atracción hacia el grupo.


#### Comportamiento emergente observado

El sistema presenta un comportamiento:

-Moderadamente disperso
-Relativamente estable
-Con momentos de fluidez en el movimiento grupal

Cuando los parámetros están equilibrados, el flocking se ve organizado, pero con suficiente variación para no ser rígido.

Si se exageran los valores, puede volverse:

-nervioso (cambios bruscos)
-caótico (pérdida de estructura grupal)

#### ¿Qué atmósfera visual produce el flocking?

El flocking genera una atmósfera de movimiento colectivo, similar a:

bandadas de aves
bancos de peces
multitudes en movimiento

Visualmente transmite:

coordinación
comportamiento grupal
sensación de “vida” en el sistema
¿En qué relación con una canción podría funcionar mejor?

Este algoritmo funciona bien con música que tenga:

ritmo constante
estructura progresiva
capas que se repiten con variaciones

Por ejemplo:

música electrónica
música instrumental con crescendos
piezas donde el ritmo guía el movimiento

También puede adaptarse a cambios musicales:

partes suaves → flocking más cohesivo y lento
partes intensas → movimiento más rápido y disperso

#### Actividad 5: 

#### Tipo de movimiento que producen

-Flow Fields:
  Producen un movimiento continuo y fluido. Los agentes siguen trayectorias suaves y curvas, como si fueran arrastrados por una corriente invisible.

-Flocking:
  Genera un movimiento colectivo basado en interacción. Los agentes se agrupan, se separan y se reorganizan constantemente, simulando comportamientos de grupo.

#### Nivel de control visual:

-Flow Fields:
  Alto nivel de control.
  El diseñador define directamente el campo de vectores, lo que permite controlar la dirección global del movimiento.

-Flocking:
  Menor control directo.
  El comportamiento emerge de la interacción entre agentes, por lo que es más difícil predecir exactamente el resultado.

#### Nivel de emergencia

-Flow Fields
Nivel medio de emergencia.
Aunque hay variación, el comportamiento general está guiado por el campo.

-Flocking
Alto nivel de emergencia.
El comportamiento colectivo no está predefinido, sino que surge de reglas locales simples.

#### Tipo de atmósfera o sensación

Flow Fields:

Fluidez
Calma
Organicidad
Sensación de corriente o flujo natural

Flocking:

Vida colectiva
Dinamismo
Coordinación grupal
Tensión o energía (dependiendo de parámetros)
Relación posible con una pieza musical

Flow Fields
Funciona bien con música:

ambiental
lenta
continua

Se adapta a sonidos suaves y progresivos.

Flocking
Funciona bien con música:

rítmica
estructurada
con cambios de intensidad

Se adapta a beats y variaciones dinámicas.

#### Ventajas y limitaciones

-Flow Fields

Ventajas:

Fácil de controlar visualmente
Movimiento suave y predecible
Ideal para composiciones limpias

Limitaciones:

Puede volverse repetitivo
Menor interacción entre agentes

-Flocking

Ventajas:

Alto nivel de complejidad emergente
Movimiento más “vivo”
Interacción rica entre agentes

Limitaciones:

Difícil de controlar con precisión
Puede volverse caótico si no se ajustan bien los parámetros.


#### Cierre
Uso según tipo de canción:

-Contemplativa
Usaría Flow Fields, porque genera movimiento suave, continuo y relajante, que acompaña bien sonidos lentos y atmósferas tranquilas.

-Agresiva
Usaría Flocking, aumentando velocidad y fuerzas. Esto genera movimiento caótico, tensión y energía, que coincide con música intensa.

-Melancólica
Usaría Flow Fields, con baja velocidad y variaciones suaves. Esto crea una sensación de fluidez lenta y emocional.

-Eufórica
Usaría Flocking, con parámetros que generen cohesión y dinamismo. El movimiento grupal rápido transmite energía y emoción colectiva.

## Bitácora de reflexión

#### Concepto visual:

Con esta obra, se busca generar el sentimiento de cariño hacia alguien, atraves de un campo de rosas generativas, petalos y siguiendo la melodia de la respectiva canción. Simbolizando de esta manera como se construyen, se intensifican y se expresan los sentimientos.

#### ¿Cuál es la relación entre lo visual y la canción?

La relación está estrechamente pensada, se busco generar un campo de rosas y cada parte se generara según algúna parte del a melodía, por ejemplo:
-Graves (bass): controlan el nacimiento de nuevas rosas y los impulsos fuertes del sistema
-Medios (mid): afectan la apertura de las rosas (floración)
-Agudos (treble): generan pétalos y detalles visuales
-Amplitud general: controla velocidad, energía y persistencia visual

Generando así una armonia visual con la música, en algunas partes aparecen más rosas, crecen más rápido y así.

La pantalla completa también fue de gran importancia para una mayor inmersión.

#### Moodboard
Algunas de estás imagenes se pensaron para la idea

<img width="692" height="1230" alt="image" src="https://github.com/user-attachments/assets/1c494352-4263-45c9-bb84-725da2d423d8" />

<img width="1152" height="2048" alt="image" src="https://github.com/user-attachments/assets/3d84fe4f-dc16-4cb9-93cb-55a03a75ba13" />

<img width="720" height="1083" alt="image" src="https://github.com/user-attachments/assets/f479f24f-f3e3-4a4d-8d12-290599b92f2e" />

<img width="736" height="1308" alt="image" src="https://github.com/user-attachments/assets/c4214b82-26cf-4b30-ae0a-2369d9ed1549" />

#### Mapa de Decisiones

Varios factores estéticos fueron pensados para una mayor inmersión, se escogio un fondo negro buscando una atmosfera más íntima, de ese sentimiento de cariño que es algo muy personal. El crecimiento vertical simboliza a su vez como este sentimiento va creciendo, los petalos es ese desborde emocional por el aprecio hacia esa persona.

#### Mapa de interpretación

Mouse: genera pétalos 
Espacio: activa clímax visual
S: reduce energía 
C: Cambia el color de los petalos y las rosas
Audio: controla dinámica general del sistema

#### Algoritmo elegido

En este caso para esta obra, se utilizó flow field en lugar de flocking. Esta decisión se tomo respecto a verios factores:

-permitir un movimiento continuo y orgánico
-generar varias trayectorias naturales similares al crecimiento de plantas
-no depender del comportamiento grupal, sino de un “campo invisible”

Y con estos factores cruciales, fue que se tomo la decisión de poder hacer una obra tan natural como esta.

#### Relación audio-visual

En la obra, como se mencionó antes, se busco una sinergia con la melodia, entonces, la energía se basa en la velocidad y cantidad, lso graves en el nacimiento de las rosas, lso medios en su forma y por último, los agudos en los detalles como los pétalos y destellos.

#### Uso de la IA

Aparte de generar el código únicamente, se busco mejorar el rendimiendo, usando IA's como Claude, ChatGPT y Gemini, para pulir el código en sus respectivas y ver algunos errores qeu salían, por ejemplo "Las rosas no se ven en la pantalla", o "Están saliendose de la pantalla, y no están tomando un buen tamaño, deberíamos intentar esto para intensificar el sentimiento" y prompts por el estilo.

#### Código:




