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



## Bitácora de aplicación 



## Bitácora de reflexión


