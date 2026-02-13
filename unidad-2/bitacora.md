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

-¿Para qué sirve el método mag()? Nota que hay otro método llamado magSq(). ¿Cuál es la diferencia entre ambos? ¿Cuál es más eficiente?

mag (Desde el origen hasta su punta) lo que hace es darnos la magnitud del vector, sin embargom, la diferencia entre magSq y mag es que Sq no saca el valor con la raíz cuadrada, que puede llegar a ser un poco inpresiso, pero si se busca una aproximado y poder ahorrar recursos, magSq es mejor opción, por otro lado, para más precisión se busca usar mag().

-¿Para qué sirve el método normalize()?

Convierte un vector en unitario, mantiene su dirección pero su tamaño cambia a 1, es decir, apunta al mismo sitio, pero su tamaño es uno.

-Te encuentras con un periodista en la calle y te pregunta ¿Para qué sirve el método dot()? ¿Qué le responderías en un frase?

Con el método dot() hacemos referencia al producto punto entre vectores, y con este podemos saber que tan aliniados están dos vectores.

-El método dot() tiene una versión estática y una de instancia. ¿Cuál es la diferencia entre ambas?

A la hora de la verdad, no  cambia mucho. Por instancia, un vector llama al otro y hace el calculo (v1.dot(v2)), mientras que por estático, se llama a la clase y hace la operación, es más por comodidad pero ambos dan el mismo resultado.

-Ahora el mismo periodista curioso de antes te pregunta si le puedes dar una intuición geométrica acerca del producto cruz. Entonces te pregunta ¿Cuál es la interpretación geométrica del producto cruz de dos vectores? Tu respuesta debe incluir qué pasa con la orientación y la magnitud del vector resultante.

El producto cruz nos permite crear otro vector perpendicular a los otros dos que ya estén creados. donde su magnitud es el area de estos dos vectores y su dirección se puede calcular por la regla de la mano derecha

-¿Para que te puede servir el método dist()?

Está función nos permite calcular la distancia entre dos vectores

-¿Para qué sirven los métodos normalize() y limit()?

limit(), lo que hace es decirle al vector que no se pase de cierta magnitud, es decir, le damos un valor que sea el límite de su magnitud, mientras que normalice es que su tamaño será 1. 

### Actividad 6

## Bitácora de reflexión


