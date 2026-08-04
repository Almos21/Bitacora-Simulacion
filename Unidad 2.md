## Unidad 2
### Conceptualización:
Quiero explorar la tensión entre la propagación y la voracidad
Esta idea de tensión me surgió inspirándome en las deidades del juego Honkai Star Rail, llamadas Eones, estas representan cada una un concepto y hay dos opuestas llamadas Voracidad y Propagación. La propagación busca nunca estar sola y se multiplica de manera inmensa y descontrolada, y la voracidad nunca deja de tener hambre por lo que devora insaciablemente la plaga de la propagación, quien intenta sobrevivir y propagarse constantemente y por su parte la Voracidad nunca está satisfecha del todo, lo que es su objetivo final. Con esta simulación entonces busco no solo representar estos eones sino también una dinámica poblacional que se puede relacionar con otros seres.

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/56ccfa60-6244-4f77-81c6-54de189d376a" />

<img width="512" height="512" alt="image" src="https://github.com/user-attachments/assets/5706f2fa-5cd1-4ba9-8394-58c595bde20d" />

### Definiciones:
#### Tipos de partículas:
- ##### Vida:
Existen para alimentar la propagación y definir sus movimientos, no hacen nada y solo aparecen de a poco, atraen a la propagación hacia ella y se mueve lentamente sin destino. Esta se crea con la intención de ayudar a condicionar el movimiento de la propagación y que no este por estar, tiene que ver con el concepto porque representa los seres que la propagación también cazaba en el universo su búsqueda de vivir y reproducirse.
-  ##### Propagación:
-   - Nómada: Esta existe para representar la expansión constante que no busca formar sociedades o agrupaciones, se reproduce de manera más constante y busca comida, es más rápida para buscar y huir y no le gusta mucho acercarse a otras partículas.
    - Social: Esta representa a una propagación más organizada, cuando encuentren comida atraen a las cercanas como comunicándose, y si se encuentran con la voracidad se juntan para protegerse, se reproducen menos pero sobreviven más que las nómadas debido a no estar aisladas.
- ##### Voracidad:
Son los cazadores, su velocidad de movimiento depende de las poblaciones de Propagación y de su energía, entre menos hayan tiene menos hambre y se mueve más lento pero entre más hayan más rápido lo hacen, esta decisión se toma para mostrar la tensión de los conceptos, mientras más uno quiera reproducirse más hambre el otro va a tener evitándole permitirle llegar a propagarse lo mucho que quiere pero nunca estando satisfecho por completo.

#### Cantidades Iniciales:
Vida: 300 Debe ser la partícula más abundante para evitar que el sistema colapse rápidamente por falta de alimento. Su distribución amplia obliga a las especies a explorar el escenario.
Voracidad: 15 Deben ser pocos al inicio. Si hubiera demasiados, eliminarían la Propagación antes de que esta se expanda. Al ser pocos, primero observamos el crecimiento de las colonias y luego el inicio de la depredación.
Propagación Nómada: 90 Al ser la variante exploradora y con mayor reproducción, necesita comenzar con una población relativamente alta para colonizar rápidamente el mapa y encontrar nuevas fuentes de Vida.
Propagación Social: 60 Empieza con menos individuos porque su ventaja no está en el número sino en la cooperación. Al agruparse sobreviven más tiempo frente a la Voracidad. 

#### Matriz de atracción, repulsión o indiferencia:
| | Vida| Prop. Nómada | Prop. Social | Prop. Social|
|----------|:-------:|:---------:|:---------:|-----------|
| Vida | — | atrae | atrae | indiferente |
| Prop. Nómada| consume | ligera atracción | indiferencia | fuerte repulsión |
| Prop. Social| consume | ligera atracción |fuerte atracción | fuerte repulsión |
| Voracidad | indiferencia | fuerte atracción |fuerte atracción | ligera repulsión |

#### Intensidad y alcance de cada relación:
Manejándolo como una escala de 0 a 1
- Vida → Propagación
Atracción 0.8 radio 80 px
- Propagación Social → Propagación Social
Atracción 0.7 radio 60 px
- Voracidad → Propagación
Atracción 1.0 radio 140 px
- Propagación → Voracidad
Repulsión 1 radio 130 px

#### Distancias de interacción:
- Detección
150 px
Lo suficiente para ver gran cantidad de distancia cerca y que no se pierdan
- Influencia
80 px
Empieza a afectar de verdad
- Contacto
8 px
Lo suficiente para detectar y actuar respecto a esto

#### Fricción y velocidad máxima
- Vida
Fricción: 0.97
Velocidad máxima: 0.2

- Voracidad
Fricción: 0.86
Velocidad máxima: 3.4

- Prop. Nómada, deben sentirse nerviosas
Fricción: 0.82
Velocidad máxima: 4.0

- Prop. Social, deben verse coordinadas
Fricción: 0.89
Velocidad máxima: 2.1

#### Distribución inicial:
Vida, toda la pantalla.

Nómadas, cinco colonias pequeñas.

Sociales, tres colonias grandes.

Voracidad, dos individuos aislados.

Estas decisiones permiten que haya un tiempo para que el enjambre se genere sin ser devorados aún.

#### Parámetros constantes
Masa
Radio
Velocidad máxima
Fuerza máxima de giro
Fricción
Alcance visual
Radio de colisión

#### Parámetros variables

##### Hambre
Hace crecer
velocidad de búsqueda y velocidad de persecución 
radio de detección

##### Energía
Al comer energía aumenta mientras que al moverse la energía disminuye.

##### Reproducción
Depende de la energía, comida y la cantidad de partículas de propagación

##### Miedo
Si Voracidad está cerca la huida aumenta.

##### Densidad del enjambre
Si hay muchas partículas sociales su cohesión aumenta y si hay pocas su alienación disminuye, esto lo seleccioné porque de esta manera el grupo empieza a romperse.

#### Apariencia e interacción:
- Vida: puntos verdes que pulsan lentamente para indicar regeneración.
- Propagación: amarillo (sociales) o cian brillante (nómadas); cuando están listas para dividirse emiten un halo que aumenta de intensidad.
- Voracidad: rojo o púrpura; su tamaño o brillo crece con el nivel de hambre y dejan una estela al perseguir

- Vida + Propagación: la partícula de Vida desaparece y la de Propagación aumenta ligeramente de tamaño antes de volver a su tamaño normal.
- Voracidad + Propagación: la Propagación es consumida y la Voracidad incrementa temporalmente su brillo y velocidad.

### Registro de pruebas
En base al sistema ya planteado usaré el agente de IA Claude para la programación, explicándole todo el sistema.

### Autoevaluación:
(aun no aplica es solo que pegué la que hice en el anterior para tener el formato)
| Criterio | Cumplo | No cumplo | Evidencia |
|----------|:-------:|:---------:|-----------|
| Encargo completo: interpreto los cinco momentos dentro de un mismo sistema visual. | ◼ | ☐ | [Evidencia](#1)|
| Simulación con intención: utilizo al menos tres conceptos de la unidad para comunicar las ideas del encargo. | ◼ | ☐ | [Evidencia](#1) |
| Interacción significativa: la interacción modifica el comportamiento o las probabilidades del sistema, que también funciona sin intervención. | ◼ | ☐ |[Evidencia](#1) |
| Prototipo funcional: la experiencia puede ejecutarse y recorrerse completa sin errores que impidan comprenderla. | ◼ | ☐ |[Evidencia](#2) |
| Proceso documentado: la bitácora evidencia avances, decisiones, dificultades, soluciones, uso de IA y enlace al prototipo. | ◼ | ☐ |[Evidencia](#3) |
