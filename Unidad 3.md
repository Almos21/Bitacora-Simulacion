# Unidad 3
<a name="6"></a>
## Instrumento funcional
[Link a instrumento](https://almos21.github.io/test-sim/)

## Mapa del sistema
<a name="2"></a>
## Ficha de fuerzas
<a name="1"></a>
### Ondas
La primera fuerza que decidí probar fue aplicar ondas que me ayudaran a simular el beat y un movimiento oscilante que va dándole vida a las partículas, la ecuación que ordena esta fuerza es: 

$$F_{onda} = \hat{r} \cdot A \cdot \sin(k \cdot d - \omega \cdot t) \cdot L$$

Donde: $\hat{r}$ (Dirección): Vector normalizado desde la partícula hacia el cursor. 

$A$ (Magnitud/Amplitud): La fuerza del empuje/atracción. 

$k$ (Frecuencia): Qué tan juntas están las crestas de las ondas respecto a la distancia ($d$).

$\omega$ (Velocidad): Qué tan rápido se desplaza la onda en el tiempo ($t$).

$L$ (Límite): Un multiplicador binario (1 o 0) que anula la fuerza si la distancia supera el radio máximo estipulado.

### Disparo
Para este me base en la repulsión base que de por si tiene particle life, pero enfocandolo desde el mouse, queda así:

$$v_{nueva} = v_{actual} + (\text{Fuerza} \times \text{Dirección} \times \Delta t)$$

la intención con esta fuerza fue crear líneas interesantes en medio de la simulación, pero no solo lineas finas, sino con la posibilidad de aumentar su grosor para hacer otras visuales y movimientos notorios, esto lo acompañe de un mayor rango de color en la velocidad de la partícula

### Gravedad Doble
Para esta fuerza tenia pensado hacer que partículas subieran y otras bajara y de vez en cuando al encontrarse chocaran y formaran explosiones, esta ultima parte llevaba a un caos gigantesco así que decidí solo utilizar la gravedad doble y dejar las repulsiones como un recurso extra, para estas la lógica fue una ecuación que detecta la distancia entre partículas y si esta baja de un umbral y además se cumple que un random es menor a una probabilidad editable entonces las partículas usan la ecuación de repulsión pero a una magnitud exagerada.

| Prueba | Fuerzas activas | Condición inicial | Predicción |
|---|---|---|---|
| Ondas | $$F_{onda}$$ | velocidad = 0 | las partículas empiezan a oscilar y a generar un patrón de onda |
| Disparo | $$F_{repulsión}$$ | velocidad = 0 | salen partículas volando desde el cursor hasta la dirección que tenía |
| Gravedad Doble | Gravedad | velocidad = 0 | caen o se alzan dependiendo de cual dirección se les asignó |

## Registro de pruebas
<a name="3"></a>
### Ondas
El resultado esperado para las ondas es que generen una sensación de beat o "latido" en las partículas mientras a la vez forma un patrón base que se alterará después, el primer intento con la IA dio este resultado:

<img width="501" height="429" alt="image" src="https://github.com/user-attachments/assets/20ec6de1-9213-494f-b420-29af82866ec1" />

cumple con lo que se buscaba, y al modificar en el lab editor puedo modificar los parámetros para que alcance la velocidad que busco, pero esto no es suficiente para mi, la canción esta en un bmp determinado, y verlo a ojo es difícil, por esto decidí que cambiaría la velocidad por bmp, al hacer este cambio es más acorde a la canción y más fácil de modificar, esto no lo puedo mostrar aqui porque el patrón es tecnicamente el mismo, cambió su velocidad

### Disparos
Para esta fuerza decidí hacer una repulsión focalizada y muy fuerte, para hacer estelas de colores a lo largo del campo, el resultado esperado eran lineas en el aire rápidas, pero este fue el primer resultado:

<img width="718" height="484" alt="image" src="https://github.com/user-attachments/assets/73db9b2f-af46-44e1-8d02-3ef0ba0f306d" />

una repulsión inicial masiva que terminaba en un caos completo a resolver asi que expliqué mejor a la IA como funcionaba la fuerza y la dirección buscada, en el segundo intento resultó como se buscaba, también puedo modificar su grosor y fuerza para que sea como lo desee.

<img width="463" height="444" alt="image" src="https://github.com/user-attachments/assets/6d8450e6-2787-4456-bbd9-6a772d5f085c" />

### Caida y subida
Mi idea original con esta fuerza era que las partículas subieran una mitad y bajaron la otra, y que al encontrarse chocaran y crearan explosiones interesantes

<img width="576" height="603" alt="image" src="https://github.com/user-attachments/assets/25ad7909-0723-41ac-add0-84c1390e9285" />

Pero no lo pensé bien, primero que nada es obvio que al todas chocar se crea un caos absoluto así que decidí regularlo con un chance modificable de que pasara, pero aunque al inicio creaba una imagen interesante se volvía siempre al final un caos

<img width="622" height="593" alt="image" src="https://github.com/user-attachments/assets/cad1f02b-ce24-49c6-a2df-f47d69242397" />

Pero decidí no desecharlo todo, porque me interesó mucho los interesantes patrones formados por algunas partículas subiendo y otras bajando y al momento de juntarla con otras fuerzas daba patrones y resultados que se sentian interesantes.

<img width="501" height="350" alt="image" src="https://github.com/user-attachments/assets/ca583b9a-0425-4607-afdc-be5f4e565ef9" />
<img width="390" height="451" alt="image" src="https://github.com/user-attachments/assets/5eb2a7d6-a5dd-493c-912f-75fd91e2ea91" />
<img width="838" height="600" alt="image" src="https://github.com/user-attachments/assets/87c2bee0-b883-4293-b690-5e7a7dc156f1" />

El ultimo paso fue poder relacionar todo con teclas para poder interpretar las visuales en vivo, para esto decidí asignar a cada fuerza un número, al apretarlo se apagan o prenden y de paso si dejo presionada alguna letra desde la "q" hacia la derecha y las flechas del teclado modifica los parámetros de la ultima fuerza elegida, entonces por ejemplo si presiono 4 selecciono la de ondas y si dejo apretada la q puedo aumentar o rebajar su fuerza con las flechas del teclado. Mantuve fuerzas del proyecto original por su potencial al juntarlas con las elegidas.

Algunas pruebas con varias fuerzas aplicadas a la vez:

<img width="922" height="657" alt="image" src="https://github.com/user-attachments/assets/12903e5f-ef84-4a7b-b7ff-3fc4e86c891c" />

<img width="957" height="471" alt="image" src="https://github.com/user-attachments/assets/4976bb44-eca7-44cc-8a7a-4b0819ebd124" />

<img width="684" height="463" alt="image" src="https://github.com/user-attachments/assets/db53831a-f492-40f5-a6ca-36dc36de702f" />


Score visual
<a name="4"></a>
## Bitácora de IA
Lo primero que hice fue explicarle el contexto completo del proyecto a la ia, con esto me refiero a los archivos y los códigos para que tuviera una visión sobre la cual trabajar, además de marcarle partes de la estructura relevantes e importantes que tenían que permanecer. 
<a name="5"></a>
<img width="496" height="274" alt="image" src="https://github.com/user-attachments/assets/6a2d5503-d4a8-40d5-a69c-6ec9494bc527" />

De aquí explique las fuerzas que quería implementar una a una aislándolas y asegurándome que por si mismas fueran lo que buscaba, si sabia que era lo que quería pero no estaba seguro de la ecuación que lo regía también le preguntaba y le explicaba donde implementarlo. Los cambios o decisiones relevantes fueron: Primero hubo una fuerza que quise implementar pero descarté por completo que fue el ruido, no lograba el resultado que buscaba y al final consideré que solo era algo que no se relacionaba mucho por donde yo me dirigía. Lo segundo fue fue lo de gravedad doble, las partículas eran más caóticas de lo buscado pero gracias a que incluyó la posibilidad de mover los parámetros pude ver el potencial en la gravedad doble por si sola, y en las colisiones para efectos mínimos. (todas pruebas en la sección de pruebas arriba)

### Autoevaluación:
| Criterio | Peso | Valoración | Aporte | Evidencia|
|----------|:-------:|:---------:|:---------:|-----------|
| Trazabilidad y comprensión del sistema | 25% | 0 | 25 | [Comprendí el modelo del sistema, donde se debían ubicar las fuerzas y como se integraba todo](#2)|
| Verificación del algoritmo de fuerzas | 25% | 100 | 25 | [Comprendí las fuerzas implicadas, en que parte del código se almacenaban y como agregar unas nuevas, dirigiendo así a la IA sin estar a lo ciego de que se hacía](#1) |
| Diseño de fuerzas e intención | 20% | 100 | 20 | [Modifique las fuerzas para poder dar las reacciones que buscaba con una intención de diseño detrás](#3) |
| Instrumento, score e interpretación | 15% | 0 | 15 | [Score final](#4) |
| Experimentación y criterio frente a la IA | 10% | 100 | 9 | [Revisé y aislé lo que la IA me entregó y realicé cambios según mi juicio](#5) |
|Entrega técnica y documentación | 5 | 100% | 5 | [Entrega URL](#6) |

Total: 

