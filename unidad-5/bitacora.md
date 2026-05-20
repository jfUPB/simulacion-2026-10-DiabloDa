# Unidad 5
## Bitácora de proceso de aprendizaje

### Actividad 1

-Capa de comportamiento: 
Cada particula cuenta dos estados:
 -Estado físico con 3 propiedades: 
     position → posición en pantalla
     velocity → velocidad
     acceleration → aceleración

 -Estado vital con una propiedad:
     lifespan → tiempo de vida de la partícula

Y la muerte de la particula esta dada cuando lifespan sea menor a 0.

La actualización en cada frame sigue el patrón Motion 101:

```java
velocity += acceleration
position += velocity
```

Además:
-se aplica una fuerza (gravedad)
-se reduce el lifespan
-se reinicia la aceleración

- Capa de estructura

Las partículas se crean aquí:


```java
particles.push(new Particle(width / 2, 20));
```

Esto ocurre en cada frame, o sea, constantemente se están generando nuevas partículas.

Las partículas se eliminan en:

```java
if (particle.isDead()) {
  particles.splice(i, 1);
}
```

El sistema decide eliminarlas cuando su vida termina.

El array se recorre en reversa:

```java
for (let i = particles.length - 1; i >= 0; i--)
```

Esto se hace porque al eliminar elementos (splice), el array cambia de tamaño.
Si se recorriera hacia adelante, se podrían saltar partículas o generar errores.

Si no eliminamos partículas:

el array crecería infinitamente
consumiría más memoria
bajaría el rendimiento (FPS)

-Capa de visualización
Cada partícula se representa como:

```java
circle(...)
```

con:

borde (stroke)
relleno (fill)
transparencia ligada al lifespan

El lifespan afecta directamente la apariencia:

```java
stroke(0, this.lifespan);
fill(127, this.lifespan);
```

A medida que la vida baja, la partícula se vuelve más transparente.

Si quisiera cambiar la representación visual:

Cambiaría:

el método show() (por ejemplo usar line() o rect())

No cambiaría:

update()
applyForce()
lógica de vida (lifespan)

### Actividad 2:

Antes (en el ejemplo anterior), en draw() se hacía todo:

crear partículas
actualizarlas
eliminarlas

Ahora esas responsabilidades están dentro de la clase Emitter:

addParticle() → crea partículas
run() → actualiza y elimina partículas

Es decir, la lógica del sistema de partículas ya no está en draw(), está encapsulada en el emitter.

- Ventaja de encapsular en una clase

La ventaja principal es la organización:

cada emitter maneja sus propias partículas
el código es más limpio
se pueden tener muchos sistemas al mismo tiempo
es más fácil reutilizar y modificar

En vez de un sistema global, ahora hay múltiples sistemas independientes.

Antes (en el ejemplo anterior), en draw() se hacía todo:

crear partículas
actualizarlas
eliminarlas

Ahora esas responsabilidades están dentro de la clase Emitter:

addParticle() → crea partículas
run() → actualiza y elimina partículas

- Ventaja de encapsular en una clase

La ventaja principal es la organización:

cada emitter maneja sus propias partículas
el código es más limpio
se pueden tener muchos sistemas al mismo tiempo
es más fácil reutilizar y modificar

En vez de un sistema global, ahora hay múltiples sistemas independientes.

- Transferencia conceptual (sin hablar de código)

Este sistema consiste en una colección de emisores, donde cada emisor genera múltiples entidades. Cada entidad tiene un estado definido por su posición, velocidad y tiempo de vida.

En cada ciclo, los emisores crean nuevas entidades y actualizan las existentes. Las entidades evolucionan en el tiempo bajo la influencia de fuerzas, modificando su estado en cada iteración.

Cada entidad posee un ciclo de vida limitado, y cuando este termina, la entidad es eliminada del sistema. Los emisores funcionan como organizadores que gestionan la creación, actualización y eliminación de estas entidades dentro de una colección dinámica.

### Actividad 3

- ¿Qué tienen en común y qué tienen de diferente?

En común:

Tienen las mismas propiedades base:
   posición, velocidad, aceleración, lifespan

Usan el mismo comportamiento:
   run(), update(), applyForce()

Todas pueden:
  moverse
  morir (isDead())

Porque Confetti hereda de Particle.

Diferente:

La forma en que se dibujan (show())
circle(...)   // Particle
square(...)   // Confetti

Una es un círculo y la otra un cuadrado rotando.

-¿Por qué el Emitter no necesita saber el tipo?

Porque todas las partículas comparten la misma interfaz:

p.run();
p.isDead();

El emitter trata a todas igual, sin importar si son:

Particle
Confetti

Esto es polimorfismo.

¿Y Si quisiera agregar otro tipo de partícula?

-Tendría que crear:

una nueva clase, por ejemplo:
class FireParticle extends Particle

-Cambiar (opcional):

addParticle() para incluirla

-NO tendría que modificar:

run() del emitter
isDead()
lógica de movimiento
estructura del sistema

-Comparación con Example 4.2

¿Cambió la lógica del Emitter?
No

Sigue:
recorriendo partículas
actualizando
eliminando

¿Cambió la lógica de muerte?
No

Sigue siendo:
lifespan < 0

-¿Qué cambió entonces?

Cambió la capa de visualización:

ahora hay diferentes representaciones visuales
cada tipo de partícula se dibuja distinto

Se agregó heterogeneidad:

ya no todas las partículas son iguales
hay variedad dentro del sistema

### Actividad 4:

#### Example 4.6
La gravedad se define en draw():

let gravity = createVector(0, 0.1);
El emitter la aplica:
emitter.applyForce(gravity);

Es una fuerza global, porque:

es la misma para todas las partículas
no depende de cada partícula individual

#### Example 4.7

La gravedad sigue siendo global
El repeller es diferente:

El repeller es una fuerza local, porque:

depende de la posición de cada partícula
cambia según la distancia

¿Dónde “vive” cada fuerza?

Gravedad → en el draw() (externa al sistema)
Repeller → en su propia clase (Repeller)


- ¿Qué principio físico se modela?

La fórmula:

strength = (-power) / (distance * distance)

Es similar a:

gravedad o fuerzas eléctricas

O sea: fuerza inversamente proporcional al cuadrado de la distancia.

¿Cambió la clase Particle?

No cambió casi nada

Esto significa que:

las partículas no saben nada de las fuerzas
solo reciben fuerzas


#### Modificación

Cambié solo la apariencia

Antes:

circle(this.position.x, this.position.y, 8);

Ahora (ejemplo):

rect(this.position.x, this.position.y, 8, 8);

¿Qué líneas toqué?

Solo el método show() en Particle

¿Qué clases modifiqué?

Solo Particle

¿Qué NO modifiqué?

Emitter
Repeller
fuerzas
lógica de muerte
estructura del sistema

## Bitácora de aplicación 

#### El amor es una sensación que todos hemos vivido con un ser especial, esos momentos y ese recuerdo que nos queda de ese ser. Con esta obra busco retratar como el amor es algo corto en la vida, pero que sin embargo, se puede quedar siemrpe ese recuerdo del amor que una vez vivimos en nuestras cabezas, simbolizando que no se acaba, sino que se transforma.

#### Cada decisión de lo planteo se tuvo en cuenta, que color agarrarían las particulas y como primero no sienten nada, luego se les acerca un ser querido y toman el color rosado y lo siguen con un poco de fuerza, luego al alejarse o al morir repentinametne, este deseo se vuelve azul llenandose de tristeza hasta que se aleja y queda como un bello recuerdo de un ser querido.



Código: https://editor.p5js.org/DiabloDa/sketches/hbxblekTJ

```java
let particles = [];

function setup() {
  createCanvas(800, 500);
}

function draw() {
  background(10, 10, 20, 40);

  // crear nuevas partículas (nacen en el centro)
  if (frameCount % 15 == 0) {
    particles.push(new LoveParticle(width / 2, height / 2));
  }

  // recorrer partículas
  for (let i = particles.length - 1; i >= 0; i--) {
    let p = particles[i];

    // fuerza suave hacia abajo (gravedad)
    let gravity = createVector(0, 0.03);
    p.applyForce(gravity);

    p.update();
    p.show();

    // cuando "muere", se transforma en recuerdo
    if (p.isDead()) {
      particles.splice(i, 1);

      // crear recuerdo
      particles.push(new MemoryParticle(p.pos.x, p.pos.y));
    }
  }
}

// interacción: aceptar la pérdida
function mousePressed() {
  for (let p of particles) {
    if (p instanceof LoveParticle) {
      p.acceptLoss();
    }
  }
}

// ---------------- CLASE BASE

class Particle {
  constructor(x, y) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.acc = createVector();
    this.lifespan = 255;
  }

  applyForce(force) {
    this.acc.add(force);
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  isDead() {
    return this.lifespan <= 0;
  }
}

// ---------------- AMOR (ciclo principal)

class LoveParticle extends Particle {
  constructor(x, y) {
    super(x, y);
    this.state = 0; // 0 gris, 1 amor, 2 duelo
    this.size = 5;
  }

  update() {
    super.update();

    let mouse = createVector(mouseX, mouseY);
    let d = p5.Vector.dist(mouse, this.pos);

    // ---------------- ETAPA 0 → inicio
    if (this.state == 0) {
      this.size += 0.05;

      // si el mouse se acerca → pasa a amor
      if (d < 100) {
        this.state = 1;
      }
    }

    // ---------------- ETAPA 1 → amor
    else if (this.state == 1) {
      this.size += 0.2;

      // atracción al mouse
      let dir = p5.Vector.sub(mouse, this.pos);
      dir.setMag(0.05);
      this.applyForce(dir);

      // si el mouse se aleja → duelo
      if (d > 150) {
        this.state = 2;
      }
    }

    // ---------------- ETAPA 2 → duelo
    else if (this.state == 2) {
      this.size -= 0.1;
      this.lifespan -= 3;
    }
  }

  acceptLoss() {
    if (this.state == 1) {
      this.state = 2;
    }
  }

  show() {
    noStroke();

    if (this.state == 0) {
      fill(150, this.lifespan); // gris
    } else if (this.state == 1) {
      fill(255, 100, 150, this.lifespan); // rosado
    } else if (this.state == 2) {
      fill(100, 150, 255, this.lifespan); // azul
    }

    circle(this.pos.x, this.pos.y, this.size);
  }
}

// ---------------- RECUERDO (segunda partícula)

class MemoryParticle extends Particle {
  constructor(x, y) {
    super(x, y);
    this.size = 6;
    this.lifespan = 200;
  }

  update() {
    super.update();

    // movimiento suave (como flotando)
    let noiseForce = p5.Vector.random2D();
    noiseForce.mult(0.02);
    this.applyForce(noiseForce);

    this.lifespan -= 0.5;
  }

  show() {
    noStroke();
    fill(255, 220, 100, this.lifespan); // amarillo recuerdo
    circle(this.pos.x, this.pos.y, this.size);
  }
}
```

<img width="944" height="760" alt="image" src="https://github.com/user-attachments/assets/ed1fbe0f-a16b-4a3a-a94e-667271e4e862" />


<img width="962" height="704" alt="image" src="https://github.com/user-attachments/assets/dccc253d-6ae0-4053-9b6d-e970a37f9958" />



## Bitácora de reflexión
