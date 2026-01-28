# Unidad 1

## Bitácora de proceso de aprendizaje

### Actividad 1:


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
    let yPos = height - 10;
    rect(xPos, yPos, 5, -10); // pequeñas barras
  }
}
```

Enlace: https://editor.p5js.org/DiabloDa/sketches/UGfN9gpON

## Bitácora de aplicación 



## Bitácora de reflexión



