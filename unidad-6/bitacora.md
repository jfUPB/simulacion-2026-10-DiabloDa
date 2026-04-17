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

Enlace: https://editor.p5js.org/DiabloDa/sketches/5WTCozAeR

```java
let audio, fft, amp;
let roses = [];
let petals = [];
let flowfield;

let started = false;
let beat = false;
let lastBeatTime = 0;

let smoothBass = 0;
let smoothMid = 0;
let smoothTreble = 0;
let smoothLevel = 0;

let paletteIndex = 0;

let modeClimax = false;
let modeSilence = false;

const MAX_PETALS = 800;

const PALETTES = [
  { stem: [330, 70, 80], petal: [350, 85, 95], center: [15, 90, 100] },
  { stem: [270, 60, 75], petal: [290, 80, 100], center: [330, 90, 100] },
  { stem: [180, 60, 70], petal: [200, 80, 90], center: [160, 85, 95] },
];

function preload() {
  soundFormats('mp3', 'ogg');
  audio = loadSound('rosa.mp3');
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  colorMode(HSB, 360, 100, 100, 255);
  background(0);
  fft = new p5.FFT(0.8, 1024);
  amp = new p5.Amplitude();
  flowfield = new FlowField(20);
}

function draw() {
  if (!started) {
    background(0);
    fill(0, 0, 100);
    textAlign(CENTER, CENTER);
    textSize(28);
    text('Click para comenzar', width / 2, height / 2);
    return;
  }

  let level = amp.getLevel();
  let bass = fft.getEnergy("bass") / 255;
  let mid = fft.getEnergy("mid") / 255;
  let treble = fft.getEnergy("treble") / 255;

  smoothBass = lerp(smoothBass, bass, 0.08);
  smoothMid = lerp(smoothMid, mid, 0.08);
  smoothTreble = lerp(smoothTreble, treble, 0.08);
  smoothLevel = lerp(smoothLevel, level, 0.08);

  let now = millis();
  beat = smoothBass > 0.6 && (now - lastBeatTime) > 300;
  if (beat) lastBeatTime = now;

  let bgAlpha;
  if (modeSilence) bgAlpha = 5;
  else if (modeClimax) bgAlpha = 60;
  else bgAlpha = map(smoothLevel, 0, 0.3, 10, 45);

  background(0, bgAlpha);

  flowfield.update(smoothLevel + smoothBass);

  if (modeClimax) {
    for (let r of roses) {
      r.bloomAngle += 0.05 + smoothBass * 0.05;
      r.rotation += 0.02 + smoothLevel * 0.05;
      if (random() < 0.2 + smoothTreble * 0.3 && petals.length < MAX_PETALS) {
        petals.push(new FreePetal(r.pos.x, r.pos.y));
      }
    }
  } else if (modeSilence) {
    if (random() < 0.01) {
      roses.push(new Rose(random(width), height + 10));
    }
  } else {
    if (beat) {
      for (let i = 0; i < floor(map(smoothBass, 0, 1, 1, 3)); i++) {
        roses.push(new Rose(random(width), height));
      }
    } else if (random() < 0.02 + smoothLevel * 0.3) {
      roses.push(new Rose(random(width), height));
    }
  }

  let speedMult = modeSilence ? 0.3 : modeClimax ? 1.8 : 1.0;

  for (let i = roses.length - 1; i >= 0; i--) {
    roses[i].update(smoothLevel * speedMult, beat, smoothBass, smoothMid, smoothTreble);
    roses[i].show(smoothLevel);
    if (roses[i].dead) roses.splice(i, 1);
  }

  for (let i = petals.length - 1; i >= 0; i--) {
    petals[i].update();
    petals[i].show();
    if (petals[i].alpha <= 0 || petals[i].pos.y > height + 50) {
      petals.splice(i, 1);
    }
  }

  if (modeClimax && frameCount % 90 === 0) modeClimax = false;
}

function mousePressed() {
  if (!started) {
    audio.loop();
    started = true;
    noCursor();
    fullscreen(true);
  } else {
    for (let i = 0; i < 80; i++) {
      if (petals.length < MAX_PETALS) {
        petals.push(new FreePetal(random(width), random(height)));
      }
    }
  }
}

function keyPressed() {
  if (key === 'f' || key === 'F') fullscreen(!fullscreen());
  if (key === 'r' || key === 'R') { roses = []; petals = []; background(0); }
  if (key === 'c' || key === 'C') paletteIndex = (paletteIndex + 1) % PALETTES.length;

  if (key === ' ') {
    modeClimax = true;
    modeSilence = false;
  }

  if (key === 's' || key === 'S') {
    modeSilence = !modeSilence;
    modeClimax = false;
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}

class FlowField {
  constructor(res) {
    this.res = res;
    this.cols = floor(width / res);
    this.rows = floor(height / res);
    this.field = [];
    this.zoff = 0;
  }

  update(level) {
    this.zoff += 0.003 + level * 0.01;
    for (let x = 0; x < this.cols; x++) {
      this.field[x] = [];
      for (let y = 0; y < this.rows; y++) {
        let angle = noise(x * 0.1, y * 0.1, this.zoff) * TWO_PI * 2;
        this.field[x][y] = p5.Vector.fromAngle(angle);
      }
    }
  }

  lookup(pos) {
    let col = floor(constrain(pos.x / this.res, 0, this.cols - 1));
    let row = floor(constrain(pos.y / this.res, 0, this.rows - 1));
    return this.field[col][row].copy();
  }
}

class Rose {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = createVector(random(-0.3, 0.3), random(-2.5, -3.5));
    this.path = [createVector(x, y)];
    this.stemLife = floor(random(120, 200));
    this.bloomAngle = 0;
    this.blooming = false;
    this.dead = false;
    this.age = 0;
    this.numPetals = floor(random(6, 9));
    this.petalSize = random(22, 38);
    this.rotation = random(TWO_PI);
    this.glitters = [];
  }

  update(level, beat, bass, mid, treble) {
    this.age++;

    if (!this.blooming) {
      let force = flowfield.lookup(this.pos);
      force.mult(0.3);
      this.vel.add(force);
      this.vel.limit(2 + level * 3 + bass * 3);
      this.pos.add(this.vel);
      this.path.push(this.pos.copy());

      if (beat) this.vel.add(p5.Vector.random2D().mult(1 + bass * 2));
      if (this.age > this.stemLife) this.blooming = true;

    } else {
      let target = map(mid, 0, 1, 0.3, 1);
      this.bloomAngle = lerp(this.bloomAngle, target, 0.03 + level * 0.06);
      this.rotation += 0.005 + bass * 0.05;

      if (random() < 0.06 + treble * 0.4 && petals.length < MAX_PETALS) {
        petals.push(new FreePetal(this.pos.x, this.pos.y));
      }

      if (beat) {
        for (let i = 0; i < 6; i++) {
          this.glitters.push(new Glitter(this.pos.x, this.pos.y, this.petalSize));
        }
      }

      for (let i = this.glitters.length - 1; i >= 0; i--) {
        this.glitters[i].update();
        if (this.glitters[i].dead) this.glitters.splice(i, 1);
      }

      if (this.age > this.stemLife + 400) this.dead = true;
    }

    if (this.pos.y < -150 || this.pos.y > height + 20) this.dead = true;
  }

  show(level) {
    let pal = PALETTES[paletteIndex];

    noFill();
    for (let i = 1; i < this.path.length; i++) {
      let w = map(i, 0, this.path.length, 2.5, 0.8);
      stroke(pal.stem[0], pal.stem[1], pal.stem[2] - 20, 160);
      strokeWeight(w);
      line(
        this.path[i - 1].x, this.path[i - 1].y,
        this.path[i].x, this.path[i].y
      );
    }

    if (this.blooming) {
      for (let g of this.glitters) g.show();
      this.drawRose(level, pal);
    }
  }

  drawRose(level, pal) {
    push();
    translate(this.pos.x, this.pos.y);
    scale(beat ? 1.2 : 1.0);
    rotate(this.rotation);

    let open = this.bloomAngle;
    let baseSize = this.petalSize * (0.9 + level * 1.5);

    let layers = [
      { n: this.numPetals, size: baseSize * 1.0, sat: pal.petal[1] - 25, bri: pal.petal[2] - 10, spread: open * baseSize * 0.55, alpha: 170 },
      { n: this.numPetals, size: baseSize * 0.72, sat: pal.petal[1] - 10, bri: pal.petal[2] - 5, spread: open * baseSize * 0.28, alpha: 200 },
      { n: this.numPetals - 1, size: baseSize * 0.42, sat: pal.petal[1], bri: pal.petal[2], spread: open * baseSize * 0.08, alpha: 230 },
    ];

    for (let layer of layers) {
      for (let i = 0; i < layer.n; i++) {
        let angle = (TWO_PI / layer.n) * i;
        push();
        rotate(angle);
        translate(layer.spread, 0);
        rotate(PI / 2 + open * 0.4);
        fill(pal.petal[0], layer.sat, layer.bri, layer.alpha);
        noStroke();
        this.drawPetal(layer.size);
        pop();
      }
    }

    noStroke();
    fill(pal.center[0], pal.center[1] - 20, pal.center[2], 80);
    ellipse(0, 0, baseSize * 0.22 * 2.5, baseSize * 0.22 * 2.5);
    fill(pal.center[0], pal.center[1], pal.center[2], 240);
    ellipse(0, 0, baseSize * 0.22, baseSize * 0.22);

    pop();
  }

  drawPetal(s) {
    let w = s * 0.38;
    let h = s * 0.85;
    beginShape();
    vertex(0, 0);
    bezierVertex(-w * 0.9, -h * 0.2, -w, -h * 0.65, 0, -h);
    bezierVertex(w, -h * 0.65, w * 0.9, -h * 0.2, 0, 0);
    endShape(CLOSE);
  }
}

class FreePetal {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = createVector(random(-0.6, 0.6), random(-0.5, 0.3));
    this.rot = random(TWO_PI);
    this.rotVel = random(-0.015, 0.015);
    this.size = random(6, 14);
    this.alpha = random(160, 220);
    this.fadeSpeed = random(0.3, 0.7);
  }

  update() {
    this.vel.y += 0.012;
    this.vel.x += sin(frameCount * 0.02 + this.rot) * 0.015;
    this.vel.mult(0.995);
    this.pos.add(this.vel);
    this.rot += this.rotVel;
    this.alpha -= this.fadeSpeed;
  }

  show() {
    if (this.alpha <= 0) return;
    let pal = PALETTES[paletteIndex];
    push();
    translate(this.pos.x, this.pos.y);
    rotate(this.rot);
    fill(pal.petal[0], pal.petal[1] - 10, pal.petal[2], this.alpha);
    noStroke();
    let s = this.size;
    beginShape();
    vertex(0, 0);
    bezierVertex(-s * 0.4, -s * 0.2, -s * 0.45, -s * 0.65, 0, -s);
    bezierVertex(s * 0.45, -s * 0.65, s * 0.4, -s * 0.2, 0, 0);
    endShape(CLOSE);
    pop();
  }
}

class Glitter {
  constructor(x, y, roseSize) {
    let angle = random(TWO_PI);
    let dist = random(roseSize * 0.3, roseSize * 1.2);
    this.pos = createVector(x + cos(angle) * dist, y + sin(angle) * dist);
    this.size = random(1.5, 4);
    this.alpha = random(180, 255);
    this.dead = false;
  }

  update() {
    this.alpha -= 6;
    this.size *= 0.95;
    if (this.alpha <= 0) this.dead = true;
  }

  show() {
    let pal = PALETTES[paletteIndex];
    noStroke();
    fill(pal.center[0], pal.center[1] - 30, 100, this.alpha);
    rectMode(CENTER);
    rect(this.pos.x, this.pos.y, this.size * 0.6, this.size * 3);
    rect(this.pos.x, this.pos.y, this.size * 3, this.size * 0.6);
    rectMode(CORNER);
  }
}
```



Capturas:

<img width="1919" height="1199" alt="image" src="https://github.com/user-attachments/assets/5b3202aa-2789-414a-8e6b-5200f6cfcebe" />

<img width="940" height="958" alt="image" src="https://github.com/user-attachments/assets/4763ebbe-cbdc-4027-b50c-121c21be1048" />


<img width="1608" height="957" alt="image" src="https://github.com/user-attachments/assets/ef529e35-03c4-4c44-a184-bc0fbfbe91a0" />

