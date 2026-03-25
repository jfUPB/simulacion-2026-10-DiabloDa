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

velocity += acceleration
position += velocity

Además:
-se aplica una fuerza (gravedad)
-se reduce el lifespan
-se reinicia la aceleración

- Capa de estructura

Las partículas se crean aquí:

particles.push(new Particle(width / 2, 20));

Esto ocurre en cada frame, o sea, constantemente se están generando nuevas partículas.

Las partículas se eliminan en:

if (particle.isDead()) {
  particles.splice(i, 1);
}

El sistema decide eliminarlas cuando su vida termina.

El array se recorre en reversa:

for (let i = particles.length - 1; i >= 0; i--)

Esto se hace porque al eliminar elementos (splice), el array cambia de tamaño.
Si se recorriera hacia adelante, se podrían saltar partículas o generar errores.

Si no eliminamos partículas:

el array crecería infinitamente
consumiría más memoria
bajaría el rendimiento (FPS)
## Bitácora de aplicación 


## Bitácora de reflexión
