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

## Bitácora de reflexión
