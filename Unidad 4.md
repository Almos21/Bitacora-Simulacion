# Unidad 4
<a name="6"></a>
## Instrumento funcional
[Link a instrumento](https://almos21.github.io/kuramoto-calaveras/)

## Idea
Para este proyecto mi idea fue hacer un escenario con una chica en el medio que fuera cantando, y los demás agentes fueran calaveras alrededor siendo picoteadas por cuervos, el oscilador interno de estos es lo que indica cada cuanto picotean y el kuramoto se ve aplicado ya que cada grito de calavera va haciendo que los cuervos cambien su ritmo interno y se vayan sincronizando, además de esto queria que la chica llevara la batuta del tiempo así que su influencia es mayor al de los cuervos (esto modificando el kuramoto).
<img width="3840" height="2160" alt="IMG_0253" src="https://github.com/user-attachments/assets/8b0a52ef-8c34-4d4f-b535-7844fa443348" />


## Implementación del modelo obligatorio
Se implementó el modelo con un cambio y fue la adición de `w_ij` esta es una variable que se multiplica en la sumatoria y deja la ecuación así: `dθ_i/dt = ω_i + (K/(N-1)) Σ_j w_ij · sin(θ_j - θ_i)` su intención es permitir que el valor dependa de quien canta y que tan cerca está, para así que la cantante lleve el ritmo base y las calaveras se alteren más de las cercanas que de las lejanas. En la aplicación la oscilación se representa con cada picoteo seguido de un sonido por la calavera y su frecuencia se evidencia con el aumento y disminución de cada cuanto esto pasa, la oscilación se ve alterada por el click que asusta a el cuervo y descuadra su reloj interno

## Requisitos mínimos
### 8 agentes simultáneos y 4 personalidades audiovisuales diferentes minimas.
Son 8 agentes distintos en apariencia y sonido, además de diferentes parámetros de oscilación. Cada uno tiene un sonido distinto que esta editado para sonar en una nota específica, originalmente pensé en que fueran notas que armonizaran, pero al hacer los primeros sonidos me encantó lo chistoso que sonaban y como quedaba de bien con la imagen de las calaveras.
### El usuario deberá poder modificar en tiempo real al menos 2 variables relacionadas con el modelo, siendo obligatorio poder intervenir (K).
El usuario puede usar el click para alterar el reloj interno y que a su vez disminuye por un tiempo k, para que demore un rato en que se sincronicen de nuevo. Además de esto con las flechas del teclado puede subir o bajar ω de la cantante, para así modificar la velocidad y ritmo general de la composición.



### Autoevaluación:
| Criterio | Peso | Valoración | Aporte | Evidencia|
|----------|:-------:|:---------:|:---------:|-----------|
| Trazabilidad y comprensión del sistema | 25% | 100 | 25 | [Comprendí el modelo del sistema, donde se debían ubicar las fuerzas y como se integraba todo](#2)|
| Verificación del algoritmo de fuerzas | 25% | 100 | 25 | [Comprendí las fuerzas implicadas, en que parte del código se almacenaban y como agregar unas nuevas, dirigiendo así a la IA sin estar a lo ciego de que se hacía](#1) |
| Diseño de fuerzas e intención | 20% | 100 | 20 | [Modifique las fuerzas para poder dar las reacciones que buscaba con una intención de diseño detrás](#3) |
| Instrumento, score e interpretación | 15% | 100 | 15 | [Score final](#4) |
| Experimentación y criterio frente a la IA | 10% | 100 | 10 | [Revisé y aislé lo que la IA me entregó y realicé cambios según mi juicio](#5) |
|Entrega técnica y documentación | 5 | 100% | 5 | [Entrega URL](#6) |

Total: 5

