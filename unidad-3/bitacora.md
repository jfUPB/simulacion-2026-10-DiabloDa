# Unidad 3

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 


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



## Bitácora de reflexión


