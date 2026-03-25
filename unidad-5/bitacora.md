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

## Bitácora de aplicación 


## Bitácora de reflexión
