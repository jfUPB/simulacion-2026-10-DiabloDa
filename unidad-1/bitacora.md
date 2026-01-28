# Unidad 1

## Bitácora de proceso de aprendizaje

### Actividad 1:
R//= Unir la programación con la creatividad humana, permitiendo hacer arte con una perfecta armonia entre máquina y mente humana.

### Actividad 2: 

- Modificación de ka función step:
```java
step() {
    const choice = floor(random(6));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else if (choice == 3) {
      this.y--;
    } else if (choice == 4) {
      this.x++;
      this.y++;
    } else if (choice == 5){
      this.x--;
      this.y--;
    }
```
- ¿Qué se espera? 
R//= Con la modificación se espera que en dos ocasiones se mueva de forma diagonal tanto para arriba como para abajo

Resultado:

<img width="824" height="423" alt="image" src="https://github.com/user-attachments/assets/714de657-c5a1-42f1-944d-6999ea71d562" />

Como se pudo observar se cumplió lo esperado,  debido a que cuando el random sacaba un valor de 4 o 5, se le sumaba o restaba a ambos ejes al mismo tiempo, generando así como cuando en un juego pulsamos la tecla D + W al mismo tiempo para subir de forma horizontal.

### Actividad 3
-"En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.": 
Una distribución uniforme es una distribución en la que todos los números tienen exactamente la misma probabilidad de salir, es como un dado, cualquiera de los seis números en una tirada tiene la misma probabilidad de salir. Mientras, que por otro lado, una distribución no uniforme, es todo lo contrario, valores con más probabilidad para salir, por ejemplo, la probabilidad en que las personas caminan, no todos caminan al mismo ritmo, unos van mucho más rápido y otro mucho más despacio, y así.

Para nosotros generar un programa en el cual no sea uniforme, hay que cambiar las posibilidades, es por eso que se decidio hacer esto:

```java
step() {
  let r = random(1);

  if (r < 0.4) {
    // 40% → derecha
    this.x++;
  } else if (r < 0.7) {
    // 30% → izquierda
    this.x--;
  } else if (r < 0.8) {
    // 10% → abajo
    this.y++;
  } else {
    // 20% → arriba
    this.y--;
  }
}
```

- ¿Qué se espera? 
R//= Como se observa en la imagen, se dibuja más hacía la derecha, esto debido a uqe estamos agarrando más valores a la derecha (O sea, de 0.4 hacía abajo)

<img width="824" height="419" alt="image" src="https://github.com/user-attachments/assets/8152ebcb-4890-4ec2-9f8c-0d93d5648d57" />

### Actividad 4
-Código: 
```java
let values = [];

function setup() {
  createCanvas(640, 240);
  background(255);
}

function draw() {
  // Genera un nuevo número gaussiano
  let x = randomGaussian(width/2, 60);
  values.push(x);

  // Dibuja histograma
  background(255);
  noStroke();
  fill(0, 100);
  for (let i = 0; i < values.length; i++) {
    let xPos = values[i];
    let yPos = height;
    rect(xPos, yPos, 5, -10); // pequeñas barras
  }
}
```

Enlace: https://editor.p5js.org/DiabloDa/sketches/UGfN9gpON

Imagen:

<img width="1688" height="676" alt="image" src="https://github.com/user-attachments/assets/1e34bb1c-ace6-4eaa-a6d3-7d954609a021" />

### Actividad 5:

#### Distribución personalizada: Levy flight
Este tipo de distribución básicamente es un tipo especial de la distribución de los pasos, y muchas de sus caracteristicas son varios pasos cercas, y otros alejados. 

Entonces basandome en esto, busque modificar el primer ejemplo que nos dieron del walk, ya que por lo que se investigo, esto era lo más sencillo basado en una caminata.

-Código: 
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
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0, 50);
    point(this.x, this.y);
  }

  step() {
    let stepSize = levyStep();
    let angle = random(TWO_PI);
    this.x += cos(angle) * stepSize;
    this.y += sin(angle) * stepSize;

    this.x = constrain(this.x, 0, width);
    this.y = constrain(this.y, 0, height);
  }
}

function levyStep() {
  let u = random();
  return pow(u, -1.5); 
}

```

Enlace: https://editor.p5js.org/DiabloDa/sketches/OeSiINBWZ

### Actividad 6:


## Bitácora de aplicación 

### Actividad 7:

¿Cuál es el concepto del arte? 
R//= La idea de este proyecto, su concepto artístico fue retratar desde una curva la variación de colores y además que tan suavizada podría estar esta línea. Para esto se uso el ruido de Perlin, para lograr suavizar la curva con noise, además de que hacer que suba y baje generando una aleatoriedad en su movimiento y que no sea predecible se puede hacer gracías a la función gaussiana, permiento que los valores se apróximen a un valor mayor, y que no sea predecible. Para el cambio de color también se uso una distribución más uniforme, donde cada color podía salir, y el espectador puede ver varios colores junto, generando una curva con colores armónicos y probar muchas combinaciones, esto también se permite gracias a que cada curva se almacena y dura un breve periodo de tiempo, entonces si al pulsar repetidamente el click para cambiar los colores de forma aleatoria, se podría alcanzar a distinguir esto.

-Código: 
```java

let t = 0; //Tiempo
let chaos = 0;              //Suavidad de la línea
let lines = []; //Vector de líneas
let currentColor; //Color

function setup() {
  createCanvas(360, 240);
  background(0);
  currentColor = color(255); //Se inicia el color
}

function draw() {
  background(0);

  // Dibujar líneas anteriores
  for (let l of lines) {
    stroke(l.col); //Definir color de la línea
    noFill(); //Sin grosor
    beginShape(); //empezar a calcular la línea para dibujarla, abre el buffer para mandarle las indicaciones
    for (let p of l.points) {
      vertex(p.x, p.y);  //Manda las coordenadas a p5
    }
    endShape(); //Une todos los puntos y la dibuja
  }

  // Línea nueva
  let points = []; //Array de puntos
  let xoff = t; //Guarda el tiempo en el offset del eje x para su variación

  for (let x = 0; x < width; x++) { //Array que genera la posición de X
    // Curva base suave (Perlin)
    let base = noise(xoff) * height; //Se suaviza la base con el noise dando valores de 1 y 0 y se multiplica por la altura

    // Perturbación gaussiana (controlada)
    let offset = randomGaussian() * chaos; //Aquí se calcula la distorción

    let y = base + offset; //El eje y define su distorción
    points.push({ x, y }); //Se guardan los puntos

    xoff += 0.01; 
  }

  lines.push({
    points: points,
    col: currentColor
  });

  if (lines.length > 70) {
    lines.shift();
  }

  t += 0.01;
}

// Mouse
function mousePressed() {
  // Nuevo color SOLO para lo nuevo
  if (mouseButton === LEFT) {
    currentColor = color(random(255), random(255), random(255));
  }

  // Más caos
  if (mouseButton === RIGHT) {
    chaos += 10;
  }
}

// Teclado
function keyPressed() {
  if (key === 'w') {
    chaos -= 15;
  }

  if (key === 's') {
    chaos += 15;
  }
  // Suavizar
  if (key === 'p') {
    chaos = 0;
  }
}

```

Imagenes:

<img width="551" height="453" alt="image" src="https://github.com/user-attachments/assets/b8b25361-d365-476e-b3c0-ef137c71f71f" />

<img width="682" height="420" alt="image" src="https://github.com/user-attachments/assets/0245d706-f590-4084-887d-2f4258703394" />

<img width="656" height="391" alt="image" src="https://github.com/user-attachments/assets/9344faab-b901-4511-9d3d-697392c0339a" />

Enlace del Sketch: https://editor.p5js.org/DiabloDa/sketches/N1nGSF_A5

## Bitácora de reflexión







