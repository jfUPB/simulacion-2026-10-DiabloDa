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

Código:

```java
// Nature of Code
// Daniel Shiffman
// Modificado: dos resortes en serie

class Spring {
  constructor(x, y, length) {
    this.anchor = createVector(x, y);
    this.restLength = length;
    this.k = 0.2;
  }

  connect(bob) {
    let force = p5.Vector.sub(bob.position, this.anchor);
    let currentLength = force.mag();

    let stretch = currentLength - this.restLength;

    force.setMag(-1 * this.k * stretch);

    bob.applyForce(force);
  }

  constrainLength(bob, minlen, maxlen) {
    let direction = p5.Vector.sub(bob.position, this.anchor);
    let length = direction.mag();

    if (length < minlen) {
      direction.setMag(minlen);
      bob.position = p5.Vector.add(this.anchor, direction);
      bob.velocity.mult(0);
    } 
    else if (length > maxlen) {
      direction.setMag(maxlen);
      bob.position = p5.Vector.add(this.anchor, direction);
      bob.velocity.mult(0);
    }
  }

  show() {
    fill(127);
    circle(this.anchor.x, this.anchor.y, 10);
  }

  showLine(bob) {
    stroke(0);
    line(bob.position.x, bob.position.y, this.anchor.x, this.anchor.y);
  }
}

// ----------------------
// Bob class

class Bob {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = createVector();
    this.acceleration = createVector();
    this.mass = 24;

    this.dragging = false;
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  handleClick(mx, my) {
    let d = dist(mx, my, this.position.x, this.position.y);
    if (d < this.mass) {
      this.dragging = true;
    }
  }

  stopDragging() {
    this.dragging = false;
  }

  handleDrag(mx, my) {
    if (this.dragging) {
      this.position.x = mx;
      this.position.y = my;
    }
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(175);
    circle(this.position.x, this.position.y, this.mass * 2);
  }
}

// ----------------------

let bob1;
let bob2;

let spring1;
let spring2;

function setup() {
  createCanvas(640, 240);

  spring1 = new Spring(width / 2, 10, 100);

  bob1 = new Bob(width / 2, 100);

  spring2 = new Spring(width / 2, 100, 80);

  bob2 = new Bob(width / 2, 180);
}

function draw() {
  background(255);

  let gravity = createVector(0, 2);

  bob1.applyForce(gravity);
  bob2.applyForce(gravity);

  bob1.update();
  bob2.update();

  bob1.handleDrag(mouseX, mouseY);
  bob2.handleDrag(mouseX, mouseY);

  // primer resorte
  spring1.connect(bob1);

  // segundo resorte conectado al bob1
  spring2.anchor = bob1.position;
  spring2.connect(bob2);

  spring1.constrainLength(bob1, 30, 200);
  spring2.constrainLength(bob2, 30, 200);

  spring1.showLine(bob1);
  spring2.showLine(bob2);

  bob1.show();
  bob2.show();

  spring1.show();
}

function mousePressed() {
  bob1.handleClick(mouseX, mouseY);
  bob2.handleClick(mouseX, mouseY);
}

function mouseReleased() {
  bob1.stopDragging();
  bob2.stopDragging();
}
```

Para modificar la simulación creé un sistema de dos resortes conectados en serie. En el código original solo había un resorte conectado a un objeto bob. Para lograr el nuevo sistema agregué un segundo objeto bob y un segundo resorte.

El primer resorte conecta el punto de anclaje con el primer bob. Luego, el segundo resorte conecta el primer bob con el segundo bob. De esta forma, cuando uno de los objetos se mueve, el movimiento se transmite al otro a través del resorte, generando una interacción entre ambos.

### Actividad 10

## Bitácora de reflexión


