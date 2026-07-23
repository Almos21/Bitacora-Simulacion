## Unidad 1
### Idea base
Mi idea de diseño para un festival de ciencia y creatividad relacionado con la aletoriedad es enfocar la temática y el diseño respecto a los fractales. Los fractales se relacionan con este tema debido a su relación con la incertidumbre y la aletoriedad, como se ha visto diferentes formas de aletoriedad finalizan en resultados distintos, pero aunque es imposible saber exactamente cada resultado individual es esperable la forma general final influida por las reglas establecidas (como la campana de gauss, el ejemplo de la distribución normal, el ruido perlin, etc.) lo mismo ocurre con los fractales aleatorios, inicialmente se desconoce cuales son los resultados que componen su figura final, pero la imagen global que se produce se define por las reglas establecidas dentro de su propia aletoriedad.

Esta es la relación con la idea principal que se debia mostrar en la experiencia interactiva, mi relación con el festival es la relación que hay entre la matemática y el arte a través de los fractales, algunos artistas generativos o incluso tradicionales se basan en las figuras que las ecuaciones de los fractales revelan, en corrientes como el arte psicodelico se relacionan con el humano con el cosmos a través de estas figuras, no es solo por replicar alucinaciones sino que buscan encontrar una sensasión de orden cósmico incluso dentro de la infinidad y caos interior, y esto ultimo se relaciona con la idea que la pantalla interactiva a demostrar.

### ¿Como traduzco esto a un sistema?
Un primer ejemplo que quiero tomar como inspiración es el juego del caos, que se realiza facilmente poniendo un punto en cualquier lado de un triangulo (por dentro o afuera) y aleatoriamente eligiendo un punto al cual se mueve 1/2 de la distancia, al final a pesar de ser algo aleaotrio termina con una imagen general.

<img width="529" height="459" alt="image" src="https://github.com/user-attachments/assets/f92c7d7f-41f2-4397-8d7a-9d52240d423a" />


Esta idea me gusta mucho, el problema es que este ejemplo solo cumple con el primer momento *Posibilidad* pero no con los demás, a partir de elegir el punto de partida no hay mucho margen de alteración, si se altera el movimiento y las reglas de este sistema el resultado final no será el esperado, asi que es necesario pensar en como adaptarlo, o que tomar de el. 

Investigando más sobre el mismo juego encontre que si se hace con otras figuras como un cuadrado hay que definir más reglas para poder general diferentes imagenes, esto debido a que al poner este tipo de reglas los puntos empiezan a tener unas partes por la que pasan por más frecuencia u otras por las que definitivamente no lo hacen, con esto puedo cumplir con el momento de *Tendencia* y *Normalidad* pero seguimos sin la excepción y muchisimo menos con la interactividad, ya que a pesar de todo este sistema es demasiado automatizado y sin abertura hacia la intervención sin derrumbarse. Además de otro problema conceptual y es que buscamos demostrar que la aletoriedad puede dar a muchas posibilidades pero aqui a diferencia de patrones como el walker que sabemos como puede verse pero no de manera exacta en este sabemos la figura final.

Ante este problema decidí recurrir a un modelo de IA para investigar sobre otros fractales aleatorios que si tuvieran espacio para la interactividad, preguntando a gemini dandole lo que estaba investigando y como necesitaba que fuera algo interactivo y con excepciones me dio un concepto muy util que podria utilizar: el DLA
<img width="746" height="756" alt="image" src="https://github.com/user-attachments/assets/3150955d-38a9-4b63-ab81-d79b92b3d522" />

Con la idea danda por gemini tengo un terreno muy solido sobre el cual actuar y podria directamente pedirle esto mismo, pero senti que queria ver que más podria aprovechar de este concepto ya que igual este no complia con Tendencia (si con normalidad al estas acomularse cerca de los puntos deseados). Para esto entendi bien el funcionamiento del DLA: Se sueltan partículas invisibles para el espectador desde algun emisor y desde alli realizan algun tipo de caminata definida por algun patrón y al chocar con la semilla o alguna particula conectada a esta o a la estructura general se detienen y se vuelven visibles al espectador, esto termina generando el patron mostrado:
<img width="250" height="223" alt="image" src="https://github.com/user-attachments/assets/661251fd-5ac6-4346-a1dd-edd2137c657c" />

Ahora, para hacerlo más interesante y cumplir con los momentos realizaré varias modificaciones con ayuda también de lo propuesto por gemini: 
#### Primer momento:
La probabilidad ya esta simulación desde un inicio, pero la aplicare también en el emisor, será aleatorio de donde surgen las partículas pero moviendose siempre por el borde de la pantalla.
#### Segundo momento:
Ahora, la tendencia, ya hice que el emisor sea aleatorio pero quiero hacer que las partículas tiendan hacia algún punto, lo que haré es que la posición del emisor tienda hacia el cursor (desde aqui ya entrando un poco en la última etapa).
#### Tercer momento: 
La normalidad ya se ve en la naturaleza de la simulación, la figura se normaliza solo desde el centro hacia las ramas no existe por fuera de esto.
#### Cuarto momento: 
La excepción: Existirá una probabilidad determinada de que en cierto punto una partícula toque la estructura pero inmediatamente salte hacia un punto lejano del cuadro, pero aun considerandose parte de la estructura y por ende una nueva semilla, esto causará un nuevo punto desde el cual puedan crecer las ramas.
#### Quinto momento: 
El usuario ya influye por el segundo momento la tendencia de la generación de las partículas, pero también podrá crear con un clic nuevos núcleos con los que puedan colisionar las partículas, esto con un máximo de 3 núcleos en totál coexistiendo para no saturar la simulación, al alcanzar el máximo y crear uno nuevo se borrará el más antiguo soltando sus partículas como nuevos walkers, esto puede que resulte dañando las formas pero solo lo sabré al probarlo.

### Ahora si nos fuimos
Ahora es el momento de pasar esta idea a P5js, para programarlo usaré el apoyo de la IA


