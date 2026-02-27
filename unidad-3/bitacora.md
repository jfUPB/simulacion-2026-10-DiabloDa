# Unidad 3

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 

### Activida 2

En esta actividad entendí que la aceleración ya no se “inventa” directamente, sino que ahora es el resultado de las fuerzas que actúan sobre el objeto.

Antes yo escribía un algoritmo para mover el objeto. Ahora aplico fuerzas como viento o gravedad, y la aceleración se calcula como la suma de esas fuerzas. Esto tiene relación con la segunda ley de Newton: la fuerza produce aceleración.

También entendí por qué es importante hacer:

this.acceleration.mult(0);

al final de update().
Esto es necesario porque la aceleración solo debe durar un frame. Si no la reinicio, las fuerzas se acumulan y el objeto se movería cada vez más rápido sin control.

Otra cosa importante fue entender el paso por referencia. Cuando usamos force.div(masa) estamos modificando el vector original. Eso puede causar errores si usamos esa misma fuerza en otro objeto. Por eso es mejor hacer una copia del vector antes de dividirlo.

En conclusión, ahora el movimiento se siente más realista porque depende de fuerzas y no solo de valores inventados.

### Actividad 3

-Código con fricción:

```java
let mover;

function setup() {
  createCanvas(640, 240);
  mover = new Mover();
}

function draw() {
  background(255);

  mover.applyFriction(0.05);
  mover.update();
  mover.show();
}

class Mover {
  constructor() {
    this.pos = createVector(50, height / 2);
    this.vel = createVector(5, -2);
    this.acc = createVector();
  }

  applyFriction(coeff) {
    let friction = this.vel.copy();
    friction.mult(-1);
    friction.normalize();
    friction.mult(coeff);

    this.applyForce(friction);
  }

  applyForce(f) {
    this.acc.add(f);
  }

  update(){
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  show(){
    fill(0);
    circle(this.pos.x, this.pos.y, 24);
  }
}
```

-Código Resistencia al aire:
```java
let mover;

function setup() {
  createCanvas(640, 240);
  mover = new Mover();
}

function draw() {
  background(255);

  mover.applyDrag(0.02); 
  mover.update();
  mover.show();
}

class Mover {
  constructor() {
    this.pos = createVector(width/2, 0);
    this.vel = createVector(0, 0);
    this.acc = createVector();
  }

  applyDrag(c) {
    let speed = this.vel.mag();
    let dragMag = c * speed * speed;
    let drag = this.vel.copy().mult(-1).normalize().mult(dragMag);

    this.applyForce(drag);
  }

  applyForce(f) {
    this.acc.add(f);
  }

  update(){
    // gravity
    this.applyForce(createVector(0, 0.2));

    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  show(){
    fill(0);
    circle(this.pos.x, this.pos.y, 24);
  }
}
```

-Código de Atracción gravitacional: 

```java
let planets = [];
let sun;

function setup() {
  createCanvas(640, 240);
  sun = new Body(width/2, height/2, 50);

  for(let i=0; i<6; i++){
    planets.push(new Body(random(width), random(height), random(6,20)));
  }
}

function draw() {
  background(0);

  sun.show();

  for(let p of planets){
    let force = sun.attract(p);
    p.applyForce(force);

    p.update();
    p.show();
  }
}

class Body {
  constructor(x,y,m){
    this.pos = createVector(x,y);
    this.vel = createVector();
    this.acc = createVector();
    this.mass = m;
  }

  attract(other){
    let dir = p5.Vector.sub(this.pos, other.pos);
    let distance = constrain(dir.mag(), 5, 25);
    dir.normalize();
    let G = 1;
    let strength = (G * this.mass * other.mass) / (distance * distance);
    return dir.mult(strength);
  }

  applyForce(f){
    let f2 = f.copy().div(this.mass);
    this.acc.add(f2);
  }

  update(){
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  show(){
    noStroke();
    fill(255,200,0);
    circle(this.pos.x, this.pos.y, this.mass);
  }
}
```

### Actividad 4:

# Historia
Esta obra habla de cómo a veces intentamos alejarnos de algo, pero siempre terminamos volviendo.

En el centro hay una especie de “recuerdo” o energía que no se ve como algo literal, pero se siente. Las partículas alrededor son como pensamientos. Se mueven libres, cambian de dirección, parecen escapar… pero poco a poco vuelven hacia el centro.

Cuando el usuario presiona el mouse, puede intervenir en ese equilibrio. Puede ayudar a que se acerquen más o empujarlos lejos. Es como influir en una emoción.

Código: 
```java
let particles = [];
let center;

function setup(){
  createCanvas(800,500);
  center = new Attractor(width/2,height/2,40);

  for(let i=0;i<80;i++){
    particles.push(new Particle(random(width),random(height)));
  }
}

function draw(){
  background(10,15,30,40);

  center.show();

  for(let p of particles){

    // gravedad hacia el recuerdo
    let gravity = center.attract(p);
    p.applyForce(gravity);

    // fricción (duda)
    p.applyFriction(0.02);

    // impulso interno (intento de escapar)
    p.wander();

    // interacción con el usuario
    if(mouseIsPressed){
      let mouse = createVector(mouseX,mouseY);
      let dir = p5.Vector.sub(mouse,p.pos);
      dir.setMag(0.5);
      p.applyForce(dir);
    }

    p.update();
    p.show();
  }
}

// ---------------- PARTICLE

class Particle{
  constructor(x,y){
    this.pos = createVector(x,y);
    this.vel = p5.Vector.random2D();
    this.acc = createVector();
    this.mass = random(0.5,2);
  }

  applyForce(force){
    let f = p5.Vector.div(force,this.mass);
    this.acc.add(f);
  }

  applyFriction(c){
    let friction = this.vel.copy();
    friction.mult(-1);
    friction.normalize();
    friction.mult(c);
    this.applyForce(friction);
  }

  wander(){
    let randomForce = p5.Vector.random2D();
    randomForce.mult(0.1);
    this.applyForce(randomForce);
  }

  update(){
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  show(){
    noStroke();
    fill(180,200,255,120);
    circle(this.pos.x,this.pos.y,6);
  }
}

// ---------------- ATTRACTOR

class Attractor{
  constructor(x,y,m){
    this.pos = createVector(x,y);
    this.mass = m;
  }

  attract(p){
    let force = p5.Vector.sub(this.pos,p.pos);
    let distance = constrain(force.mag(),10,200);
    force.normalize();

    let G = 2;
    let strength = (G * this.mass * p.mass) / (distance * distance);
    force.mult(strength);
    return force;
  }

  show(){
    noStroke();
    fill(255,120,150);
    circle(this.pos.x,this.pos.y,this.mass);
  }
}

```

Código: https://editor.p5js.org/DiabloDa/sketches/R6FZ2hmuD


<img width="947" height="656" alt="image" src="https://github.com/user-attachments/assets/d41ba8fd-a5a2-4f70-99f7-ee1026d9179d" />


## Bitácora de reflexión



