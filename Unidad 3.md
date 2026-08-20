# Unidad 3

Instrumento funcional

Mapa del sistema

## Ficha de fuerzas

La primera fuerza que decidí probar fue aplicar ondas que me ayudaran a simular el beat y un movimiento oscilante que va dandole vida a las partículas, la ecuación que ordena esta fuerza es: $$F_{onda} = \hat{r} \cdot A \cdot \sin(k \cdot d - \omega \cdot t) \cdot L$$

Donde: $\hat{r}$ (Dirección): Vector normalizado desde la partícula hacia el cursor. 

$A$ (Magnitud/Amplitud): La fuerza del empuje/atracción. 

$k$ (Frecuencia): Qué tan juntas están las crestas de las ondas respecto a la distancia ($d$).

$\omega$ (Velocidad): Qué tan rápido se desplaza la onda en el tiempo ($t$).

$L$ (Límite): Un multiplicador binario (1 o 0) que anula la fuerza si la distancia supera el radio máximo estipulado.

| Prueba | Fuerzas activas | Condición inicial | Predicción |
|---|---|---|---|
| Inercia | ninguna | velocidad ≠ 0 | movimiento sin aceleración deliberada |
| +X | viento | velocidad = 0 | `v.x` crece positiva |
| Atracción | radial + | velocidad = 0 | aceleración hacia atractor |
| Repulsión | radial - | velocidad = 0 | aceleración alejándose |
| Vórtice | radial suave + tangencial | velocidad = 0 | aparece giro, no solo caída radial |

La segunda fuerza es una de repusliín

## Registro de pruebas
### Ondas
El resultado esperado para las ondas es que generen una sensación de beat o "latido" en las partículas mientras a la vez forma un patrón base que se alterará después, el primer intento con la IA dio este resultado:

<img width="501" height="429" alt="image" src="https://github.com/user-attachments/assets/20ec6de1-9213-494f-b420-29af82866ec1" />

cumple con lo que se buscaba, y al modificar en el lab editor puedo modificar los parámetros para que alcance la velocidad que busco, pero esto no es suficiente para mi, la canción esta en un bmp determinado, y verlo a ojo es difícil, por esto decidí que cambiaría la velocidad por bmp, al hacer este cambio es más acorde a la canción y más fácil de modificar

### Disparos
Para esta fuerza decidí hacer una repulsión focalizada y muy fuerte, para hacer estelas de colores a lo largo del campo, el resultado esperado eran lineas en el aire rápidas, pero este fue el primer resultado:

<img width="1436" height="968" alt="image" src="https://github.com/user-attachments/assets/73db9b2f-af46-44e1-8d02-3ef0ba0f306d" />

una repulsión inicial masiva que terminaba en un caos completo a resolver

en el segundo intento resultó como se buscaba, también puedo modificar su grosor y fuerza para que sea como lo busco: 

<img width="927" height="888" alt="image" src="https://github.com/user-attachments/assets/6d8450e6-2787-4456-bbd9-6a772d5f085c" />

### Ruido
<img width="1131" height="804" alt="image" src="https://github.com/user-attachments/assets/be14c466-522d-47fc-afa4-8a49af8e6d67" />



Score visual

Bitácora de IA

Autoevaluación ponderada

### Autoevaluación:
| Criterio | Peso | Valoración | Aporte | Evidencia|
|----------|:-------:|:---------:|:---------:|-----------|
| La intención es clara y perceptible en el comportamiento. | 20% | 100% | 20 | [Se puede ver en las evidencias como la intención es clara, se evidencia la dinámica de la propagación y sus distintos tipos ante la caza de la voracidad](#1)|
| Los tipos, cantidades, matriz y parámetros están justificados desde la intención. | 25% | 90% | 22.5 | [Justifiqué el porqué de la mayoría de los parámetros, algunos están sin explicar porque estaban bien así, sin embargo son pocos](#2) |
| Comprendo y puedo modificar el funcionamiento técnico del sistema. | 20% | 80% | 16 | [Evidencia](#3) |
| El sistema produce variaciones con una identidad reconocible. | 15% | 100% | 15 | [Evidencia](#3) |
| Experimenté, comparé, seleccioné y descarté con criterios claros. | 10% | 90% | 9 | [Se pudo ver como cambié entre versiones, tenia claro que fallaba y sabia por donde podía ir para arreglarlo ayudándome de la IA](#4) |
| Puedo distinguir y sustentar lo diseñado y lo emergente. | 10% | 100% | 10 | [Evidencia](#3) |

Total: 

