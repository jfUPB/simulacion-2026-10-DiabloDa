# Unidad 3

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 


### Actividad 3

-Código con fricción:

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

## Bitácora de reflexión
