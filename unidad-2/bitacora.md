# Unidad 2

## Bitácora de proceso de aprendizaje



## Bitácora de aplicación 

### Actividad 2:
-¿Cómo funciona la suma dos vectores en p5.js?
R// Aquí los vectores se suman por medio de la función add, la cual hace referencia a la suma. En el ejemplo se suma el vector posición con el de velocidad, por medio de "position.add(velocity)".

-¿Por qué esta línea position = position + velocity; no funciona?
R//= Porque la suma de dos vectores no funciona así en programación. Cuando se trata de vectores el programa los detecta como objetos, por ende ahí se esta intentando sumar dos objetos, lo cual no funciona así y para el lenguaje no tiene mucho sentido. Es por eso que se creo la función "add", la cual se encarga de esto, sumarlos.

### Actividad 3:
Código:
```java
let walker;

function setup() {
  createCanvas(640, 240);
  background(255);
  walker = new Walker();
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {

  constructor() {
    this.position = createVector(width/2, height/2);
  }

  show() {
    stroke(0, 40);
    point(this.position.x, this.position.y);
  }

  step() {

    // Crear desplazamiento aleatorio (vector)
    let step = createVector(random(-1,1), random(-1,1));

    // Suma vectorial (movimiento real)
    this.position.add(step);

    // Limitar al canvas
    this.position.x = constrain(this.position.x, 0, width);
    this.position.y = constrain(this.position.y, 0, height);
  }
}

```

Lo que se hizo fue crear dos vectores, con position y step. primero a position dandole el centro de la pantalla, para que siempre iniice ahí, y con el step, se busca crear un vector con valores random de - 1 a 1 tanto en x como en y para que su movimiento sea completamente aleatorio. y de ahí se le suman lso vectores position y step y luego se le límita, es decir, que no se vaya a pasar del canvas.

### Actividad 4

-¿Qué resultado esperas obtener en el programa anterior?
R//= Por lo que puedo interpretar, espero que se crea un vector, luego se pasa a string para escribirlo en consola, entonces que se escriba con su valor anterior para luego, llamar a esa otra función y cambiarle el valor de sus parametros para volver a escribirlo.

-¿Qué resultado obtuviste?
R//= El resultado que esperaba salió tal cual, además de un texto que se me olvido mencionar pero sí, se escribe el vector con sus valores iniciales, y luego se vuelve a escribir con los nuevos valores que se le asignan en la función nueva donde se pasa el vector "position" como parametro de está función.

Paso por valor: 
Acá cuando un se le da un valor a otra función, se crea otra copia, es decir, se crea una copia de lo que se tenga sin afectar el original.

Paso por referencia: 
Acá cuando se le da el valor a la función, el parametro que se le da (un objeto en este caso), si cambia, no se mantiene igual.

En el ejemplo que vimos, eso paso por referencia porque se cambio el vector, sus valores de x y y se cambiaron al pasarle una referencia a otra función.

### Actividad 5

## Bitácora de reflexión

