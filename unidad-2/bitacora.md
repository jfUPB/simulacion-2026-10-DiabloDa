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

Código:

```java
let t = 0;
let speed = 0.01;
let dir = 1;

function setup() {
    createCanvas(200, 200);
}

function draw() {
    background(200);

    let origin = createVector(100, 100);

    let v1 = createVector(70, 0);
    let v2 = createVector(0, 70);

    let v3 = p5.Vector.lerp(v1, v2, t);

    // flechas principales
    drawArrow(origin, v1, color(255,0,0));
    drawArrow(origin, v2, color(0,0,255));
    drawArrow(origin, v3, color(150,0,200));

   
    let between = p5.Vector.sub(v2, v1);
    let redTip = p5.Vector.add(origin, v1);
    drawArrow(redTip, between, color(0,150,0));

    // animación
    t += speed * dir;
    if (t > 1 || t < 0) dir *= -1;
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);

    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);

    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize/2, 0, -arrowSize/2, arrowSize, 0);
    pop();
}
```
-¿Cómo funciona lerp() y lerpColor().
R//= Lerp() nos da un valor intermedio entre dos valores que nos deny este varía según un parametro que va de 0 a 1, mientras que lerpcolor() busca hacer lo mismo, pero esta vez con colores, no hacer un cambio brusco entre colores, sino un cambio suave.

-¿Cómo se dibuja una flecha usando drawArrow()?
R//=Primero se define una base, una posición en la cual se va a iniciar, la cual por defecto es 0,0. Luego con la función line se dibuja la línea, desde el punto 0,0 hasta el vector que se le dio, después se rota para que la flecha apunte a donde esta el vector y luego se evita que se pase la punta de la flecha del vector con su magnitud y restandole el tamaño, además de luego dibujar la punta.

### Actividad 7
-Cuál es el concepto del marco motion 101 y cómo se interpreta geométricamente.
R//= Es un modelo básico 


## Bitácora de reflexión



