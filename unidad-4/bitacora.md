# Unidad 4

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 

### Actividad 2
-Simulación de ángulos:
En la simulación se observa una figura que rota constantemente alrededor del centro de la pantalla. El programa cambia el ángulo de rotación en cada frame, lo que hace que los elementos gráficos giren.

El origen del sistema de coordenadas se traslada al centro del canvas porque las rotaciones en p5.js ocurren alrededor del origen. Si no se hiciera esto, los objetos rotarían alrededor de la esquina superior izquierda.

La función rotate() rota el sistema de coordenadas, no el objeto directamente. Por eso primero se mueve el origen con translate() y luego se aplica la rotación.

Los elementos se dibujan alrededor de (0,0) porque ese punto es el centro del sistema de coordenadas después de la traslación. Aunque en cada frame se dibuja lo mismo, el sistema de coordenadas ya está rotado, por lo que los objetos parecen girar.

-Simulación de dirección del movimiento:
En esta simulación se usa el marco Motion 101, donde cada objeto tiene posición, velocidad y aceleración. En cada frame se actualiza la velocidad y la posición del objeto.
La función heading() obtiene el ángulo del vector de velocidad, es decir, la dirección en la que se está moviendo el objeto.
Las funciones push() y pop() sirven para guardar y restaurar el sistema de coordenadas, de modo que las transformaciones como translate() y rotate() solo afecten al objeto que se está dibujando.
La función rectMode(CENTER) hace que el rectángulo se dibuje desde su centro y no desde una esquina, lo que facilita que la rotación ocurra alrededor del centro del objeto.

El ángulo de rotación se obtiene del vector de velocidad, por lo que el objeto siempre apunta en la misma dirección en la que se está moviendo.

### Actividad 3

```java
let car;

function setup(){
  createCanvas(800,500);
  car = new Vehicle(width/2,height/2);
}

function draw(){
  background(240);

  car.update();
  car.edges();
  car.show();
}

function keyPressed(){

  if(keyCode === LEFT_ARROW){
    let force = createVector(-0.3,0);
    car.applyForce(force);
  }

  if(keyCode === RIGHT_ARROW){
    let force = createVector(0.3,0);
    car.applyForce(force);
  }

}

class Vehicle{

  constructor(x,y){
    this.pos = createVector(x,y);
    this.vel = createVector();
    this.acc = createVector();
    this.topSpeed = 5;
  }

  applyForce(force){
    this.acc.add(force);
  }

  update(){
    this.vel.add(this.acc);
    this.vel.limit(this.topSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  edges(){
    if(this.pos.x > width) this.pos.x = 0;
    if(this.pos.x < 0) this.pos.x = width;
  }

  show(){

    let angle = this.vel.heading();

    push();
    translate(this.pos.x,this.pos.y);
    rotate(angle);

    fill(100,150,255);
    stroke(0);

    triangle(-15,10,-15,-10,20,0);

    pop();
  }

}

```

### Actividad 4:

El marco Motion 101 consiste en que un objeto tiene posición, velocidad y aceleración. En cada frame la aceleración modifica la velocidad y la velocidad modifica la posición. Cuando se agregan fuerzas, la aceleración se calcula como la suma de todas las fuerzas que actúan sobre el objeto usando una función como applyForce(). Al final de cada frame se reinicia la aceleración con acceleration.mult(0) para que las fuerzas se vuelvan a calcular en el siguiente frame.

El Attractor es el objeto que atrae a las partículas con una fuerza. Normalmente aparece como un círculo en el centro del canvas. Para cambiar su color se puede modificar el fill() en la función donde se dibuja el attractor.

Los atributos dragging y rollover permitirían interactuar con el attractor. rollover se activaría cuando el mouse esté sobre el objeto (calculando la distancia entre el mouse y el attractor), y dragging cuando el usuario haga clic y arrastre el objeto. Esto se podría implementar usando funciones de p5.js como mousePressed(), mouseReleased() y usando mouseX y mouseY para actualizar la posición mientras se arrastra.

### Actividad 5:

Pon algo así en la bitácora, sencillo:

En las coordenadas polares la posición de un punto se define con r y theta.
r representa la distancia desde el centro y theta el ángulo. Para convertir estas coordenadas a coordenadas cartesianas se usan las fórmulas:

- X = r⋅cos(theta)

- Y = r⋅sin(theta)

Esto permite calcular la posición del punto en el plano a partir de un ángulo y una distancia. En la simulación el punto rota alrededor del centro porque el valor de theta aumenta en cada frame.

Cuando se modifica el código usando p5.Vector.fromAngle(theta), se crea un vector que solo tiene dirección basada en el ángulo, pero su magnitud es 1. Por eso el punto queda muy cerca del centro y el radio del movimiento prácticamente desaparece.

En la última modificación p5.Vector.fromAngle(theta, r), el vector se crea con un ángulo y también con una magnitud r. Esto hace que el vector tenga la misma distancia que antes, por lo que el punto vuelve a moverse en un círculo alrededor del centro con ese radio.

### Actividad 6:

En la simulación se observa cómo un punto se mueve siguiendo una función sinusoide. El movimiento ocurre porque la posición del punto se calcula con sin(), que genera valores que oscilan entre -1 y 1, produciendo un movimiento repetitivo hacia arriba y hacia abajo.

La amplitud controla qué tan grande es la oscilación del movimiento. Cuando la amplitud aumenta, el punto se mueve más lejos del centro. La frecuencia controla qué tan rápido se repite la onda, por lo que valores mayores hacen que el movimiento sea más rápido.

La velocidad angular es la cantidad que aumenta el ángulo en cada frame y determina la velocidad de la animación. El periodo corresponde al tiempo que tarda la onda en completar un ciclo completo. Finalmente, la fase desplaza la onda horizontalmente, cambiando el punto donde empieza el movimiento sin modificar su forma.

### Activdad 7:

Código: 

```java
class Oscillator {
  constructor() {
    this.angle = createVector();
    this.angleVelocity = createVector(0.02, 0.03);
    this.amplitude = createVector(
      random(20, width / 2),
      random(20, height / 2)
    );

    this.acceleration = createVector();
    this.t = random(1000); // para noise
  }

  applyForce(force){
    this.acceleration.add(force);
  }

  update() {

    // fuerza que cambia con noise (unidad 1)
    let n = noise(this.t);
    let force = createVector(map(n,0,1,-0.01,0.01), map(n,0,1,-0.01,0.01));

    this.applyForce(force);

    // motion 101 con fuerzas (unidad 3)
    this.angleVelocity.add(this.acceleration);
    this.angle.add(this.angleVelocity);

    this.acceleration.mult(0);
    this.t += 0.01;
  }

  show() {
    let x = sin(this.angle.x) * this.amplitude.x;
    let y = sin(this.angle.y) * this.amplitude.y;

    push();
    translate(width / 2, height / 2);
    stroke(0);
    strokeWeight(2);
    fill(127);
    line(0, 0, x, y);
    circle(x, y, 32);
    pop();
  }
}

let oscillators = [];

function setup() {
  createCanvas(640, 240);

  for (let i = 0; i < 10; i++) {
    oscillators.push(new Oscillator());
  }
}

function draw() {
  background(255);

  for (let i = 0; i < oscillators.length; i++) {
    oscillators[i].update();
    oscillators[i].show();
  }
}
```

Para incluir un concepto de la unidad 1, agregué noise() para modificar ligeramente la velocidad del ángulo. Esto introduce variaciones más suaves y orgánicas en el movimiento, diferentes a random().

Luego añadí un concepto de la unidad 3, incorporando fuerzas que afectan el movimiento. Se crea un vector de fuerza que modifica la velocidad angular del oscilador, haciendo que el movimiento cambie dinámicamente.

### Actividad 8: 

```java
let startAngle = 0;
let angleVelocity = 0.2;
let amplitude = 100;

function setup() {
  createCanvas(640, 240);
}

function draw() {
  background(255);

  stroke(0);
  strokeWeight(2);
  fill(127,127);

  let angle = startAngle;

  for (let x = 0; x <= width; x += 24) {

    let y = amplitude * sin(angle);

    circle(x, y + height/2, 48);

    angle += angleVelocity;
  }

  startAngle += 0.05;
}
```

En el código original la onda se dibuja solo una vez dentro de setup(), por lo que queda estática. Para que la onda se mueva como una ola, moví el código al draw() para que se dibuje en cada frame.

Además agregué una variable llamada startAngle que cambia ligeramente en cada frame. Esto hace que el cálculo de la función seno empiece desde un ángulo distinto cada vez, produciendo el efecto de que la onda se desplaza horizontalmente.

### Actividad 9:



## Bitácora de reflexión

