## Unidad 1
### Idea base
Mi idea de diseño para un festival de ciencia y creatividad relacionado con la aletoriedad es enfocar la temática y el diseño respecto a los fractales. Los fractales se relacionan con este tema debido a su relación con la incertidumbre y la aletoriedad, como se ha visto diferentes formas de aletoriedad finalizan en resultados distintos, pero aunque es imposible saber exactamente cada resultado individual es esperable la forma general final influida por las reglas establecidas (como la campana de gauss, el ejemplo de la distribución normal, el ruido perlin, etc.) lo mismo ocurre con los fractales aleatorios, inicialmente se desconoce cuales son los resultados que componen su figura final, pero la imagen global que se produce se define por las reglas establecidas dentro de su propia aletoriedad.

Esta es la relación con la idea principal que se debia mostrar en la experiencia interactiva, mi relación con el festival es la relación que hay entre la matemática y el arte a través de los fractales, algunos artistas generativos o incluso tradicionales se basan en las figuras que las ecuaciones de los fractales revelan, en corrientes como el arte psicodelico se relacionan con el humano con el cosmos a través de estas figuras, no es solo por replicar alucinaciones sino que buscan encontrar una sensasión de orden cósmico incluso dentro de la infinidad y caos interior, y esto ultimo se relaciona con la idea que la pantalla interactiva a demostrar.

### ¿Como traduzco esto a un sistema?
Un primer ejemplo que quiero tomar como inspiración es el juego del caos, que se realiza facilmente poniendo un punto en cualquier lado de un triangulo (por dentro o afuera) y aleatoriamente eligiendo un punto al cual se mueve 1/2 de la distancia, al final a pesar de ser algo aleaotrio termina con una imagen general.

<img width="529" height="459" alt="image" src="https://github.com/user-attachments/assets/f92c7d7f-41f2-4397-8d7a-9d52240d423a" />


Esta idea me gusta mucho, el problema es que este ejemplo solo cumple con el primer momento *Posibilidad* pero no con los demás, a partir de elegir el punto de partida no hay mucho margen de alteración, si se altera el movimiento y las reglas de este sistema el resultado final no será el esperado, asi que es necesario pensar en como adaptarlo, o que tomar de el. 

Investigando más sobre el mismo juego encontre que si se hace con otras figuras como un cuadrado hay que definir más reglas para poder general diferentes imagenes, esto debido a que al poner este tipo de reglas los puntos empiezan a tener unas partes por la que pasan por más frecuencia u otras por las que definitivamente no lo hacen, con esto puedo cumplir con el momento de *Tendencia* y *Normalidad* pero seguimos sin la excepción y muchisimo menos con la interactividad, ya que a pesar de todo este sistema es demasiado automatizado y sin abertura hacia la intervención sin derrumbarse. Además de otro problema conceptual y es que buscamos demostrar que la aletoriedad puede dar a muchas posibilidades pero aqui a diferencia de patrones como el walker que sabemos como puede verse pero no de manera exacta en este sabemos la figura final.

Ante este problema decidí recurrir a un modelo de IA para investigar sobre otros fractales aleatorios que si tuvieran espacio para la interactividad, preguntando a gemini me dio un concepto muy util que podria utilizar: el DLA
<img width="746" height="756" alt="image" src="https://github.com/user-attachments/assets/3150955d-38a9-4b63-ab81-d79b92b3d522" />

