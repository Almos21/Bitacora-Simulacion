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
Ahora es el momento de pasar esta idea a P5js, para programarlo usaré el apoyo de la IA Gemini, el promnt inicial que utilicé fue este: 
```
Imagina que eres alguien encargado para la construcción de una simulación en P5js utilizando el concepto de la aletoriedad y los fractales, para esto tengo este diseño:
Un DLA, pero con las siguientes condiciones: el emisor esta constantemente apareciendo en posiciones aleatorias del borde de la pantalla, la probabilidad de aparición por cada punto de la pantalla tiende hacia donde se encuentre el cursor más cerca,
preferiblemente usando una función de gauss o algo por el estilo, Existirá una probabilidad determinada de que en cierto punto una partícula toque la estructura pero inmediatamente salte hacia un punto lejano del cuadro, pero aun considerandose parte
de la estructura y por ende una nueva semilla, esto causará un nuevo punto desde el cual puedan crecer las ramas, el usuario también podrá crear con un clic nuevos núcleos con los que puedan colisionar las partículas,esto con un máximo de 3 núcleos en
totál coexistiendo para no saturar la simulación, al alcanzar el máximo y crear uno nuevo se borrará el más antiguo soltando sus partículas como nuevos walkers. Has que tenga todo un gradiente de color de azules morados y amarillos dependiendo de su
cercania con la semilla. Entregame esto como código para p5.js con Formato 9:16, full screen y ejecución interactiva en tiempo real, la semilla primera será definida por el usuario, pero si se demora 5 segundos o más desde la ejecución del programa
en elegir entonces lo hará en algun punto cercano al centro de la pantalla. Si crees que puede haber algun conflicto con las mecánicas o por ejemplo la parte de las ramas desapareciendo y soltando walkers puede dañar las figuras fractales me avisas.
```
Primer Intento:
``` js
let tree = [];
let walkers = [];
let userCores = []; // Guarda los núcleos generados por el usuario
const MAX_USER_CORES = 3;
const NUM_WALKERS = 200; // Cantidad de walkers simultáneos
const STICK_DISTANCE = 8;
const JUMP_PROBABILITY = 0.0005; // Probabilidad de saltar y crear una nueva semilla flotante

let initialSeedCreated = false;
let startTime;
let primarySeedPos = null;

function setup() {
  // Ajuste para pantalla completa manteniendo proporción 9:16
  let h = windowHeight;
  let w = h * (9 / 16);
  if (w > windowWidth) {
    w = windowWidth;
    h = w * (16 / 9);
  }
  createCanvas(w, h);
  colorMode(HSB, 360, 255, 255, 255);

  startTime = millis();

  // Inicializar walkers
  for (let i = 0; i < NUM_WALKERS; i++) {
    walkers.push(new Walker());
  }
}

function draw() {
  background(10, 20, 15); // Fondo oscuro para resaltar el gradiente

  // Revisa el temporizador de 5 segundos para la semilla inicial
  if (!initialSeedCreated && millis() - startTime > 5000) {
    createInitialSeed(width / 2 + random(-30, 30), height / 2 + random(-30, 30));
  }

  // Dibujar núcleos adicionales colocados por el usuario
  fill(50, 255, 255, 100);
  noStroke();
  for (let core of userCores) {
    ellipse(core.x, core.y, 16, 16);
  }

  // Dibujar la estructura DLA
  for (let p of tree) {
    drawParticle(p);
  }

  // Si aún no hay semilla, mostramos una pequeña guía visual
  if (!initialSeedCreated) {
    fill(0, 0, 255, 150 + sin(frameCount * 0.1) * 100);
    textAlign(CENTER, CENTER);
    textSize(14);
    text("Haz clic para colocar la semilla inicial\n(o espera 5s)", width / 2, height / 2);
    return;
  }

  // Actualizar e iterar Walkers
  for (let i = 0; i < walkers.length; i++) {
    // Múltiples pasos por frame para acelerar la simulación
    for (let step = 0; step < 4; step++) {
      walkers[i].walk();
      
      // Chequear colisión con el árbol o núcleos
      if (walkers[i].checkCollision()) {
        // ¿Ocurre un salto cuántico / nueva semilla distante?
        if (random(1) < JUMP_PROBABILITY) {
          let jumpPos = createVector(random(width * 0.15, width * 0.85), random(height * 0.15, height * 0.85));
          tree.push(new TreeParticle(jumpPos.x, jumpPos.y, getDistanceToPrimary(jumpPos)));
        } else {
          // Se une normalmente a la estructura
          tree.push(new TreeParticle(walkers[i].pos.x, walkers[i].pos.y, getDistanceToPrimary(walkers[i].pos)));
        }
        
        // Respawn del walker
        walkers[i] = new Walker();
        break;
      }
    }
    walkers[i].show();
  }
}

function getDistanceToPrimary(pos) {
  if (!primarySeedPos) return 0;
  return dist(pos.x, pos.y, primarySeedPos.x, primarySeedPos.y);
}

function createInitialSeed(x, y) {
  primarySeedPos = createVector(x, y);
  tree.push(new TreeParticle(x, y, 0));
  initialSeedCreated = true;
}

function mousePressed() {
  if (mouseX < 0 || mouseX > width || mouseY < 0 || mouseY > height) return;

  if (!initialSeedCreated) {
    createInitialSeed(mouseX, mouseY);
  } else {
    // Manejo del límite de 3 núcleos de usuario
    if (userCores.length >= MAX_USER_CORES) {
      let oldestCore = userCores.shift(); // Elimina el más antiguo
      releaseCoreAsWalkers(oldestCore);   // Libera sus partículas
    }
    
    let newCore = createVector(mouseX, mouseY);
    userCores.push(newCore);
    tree.push(new TreeParticle(newCore.x, newCore.y, getDistanceToPrimary(newCore)));
  }
}

// Libera las partículas cercanas al núcleo destruido convirtiéndolas en nuevos walkers
function releaseCoreAsWalkers(corePos) {
  for (let i = tree.length - 1; i >= 0; i--) {
    if (dist(tree[i].pos.x, tree[i].pos.y, corePos.x, corePos.y) < 30) {
      let released = tree.splice(i, 1)[0];
      // Reemplaza un walker existente con esta posición para dispersarse
      let w = new Walker();
      w.pos = released.pos.copy();
      walkers[Math.floor(random(walkers.length))] = w;
    }
  }
}

// --- CLASE WALKER ---
class Walker {
  constructor() {
    this.spawn();
  }

  spawn() {
    // Aparece en los bordes usando distribución Gaussiana hacia la posición del Mouse
    let side = floor(random(4));
    let x, y;

    // Generar un desplazamiento gaussiano respecto al cursor
    let gx = randomGaussian(mouseX, width * 0.25);
    let gy = randomGaussian(mouseY, height * 0.25);

    if (side === 0) { x = random(width); y = 0; }            // Arriba
    else if (side === 1) { x = width; y = random(height); }   // Derecha
    else if (side === 2) { x = random(width); y = height; }  // Abajo
    else { x = 0; y = random(height); }                      // Izquierda

    // Sesgar la posición del borde según el cursor/gauss
    if (side === 0 || side === 2) x = constrain(gx, 0, width);
    else y = constrain(gy, 0, height);

    this.pos = createVector(x, y);
  }

  walk() {
    // Movimiento aleatorio (Browniano)
    let vel = p5.Vector.random2D();
    this.pos.add(vel);

    // Mantener dentro del lienzo
    this.pos.x = constrain(this.pos.x, 0, width);
    this.pos.y = constrain(this.pos.y, 0, height);
  }

  checkCollision() {
    // Chequea distancia contra los nodos del árbol
    for (let i = 0; i < tree.length; i++) {
      let d = dist(this.pos.x, this.pos.y, tree[i].pos.x, tree[i].pos.y);
      if (d < STICK_DISTANCE) {
        return true;
      }
    }
    return false;
  }

  show() {
    stroke(255, 50);
    strokeWeight(1.5);
    point(this.pos.x, this.pos.y);
  }
}

// --- CLASE ESTRUCTURA FRACTAL ---
class TreeParticle {
  constructor(x, y, dFromSeed) {
    this.pos = createVector(x, y);
    this.dist = dFromSeed;
  }
}

function drawParticle(p) {
  // Paleta de gradiente: Azul (200) -> Morado (280) -> Amarillo (50)
  // Mapea la distancia desde la semilla principal
  let maxD = width * 0.7;
  let normD = constrain(p.dist / maxD, 0, 1);
  
  let hueVal;
  if (normD < 0.5) {
    // Mapea de Azul a Morado
    hueVal = map(normD, 0, 0.5, 200, 280);
  } else {
    // Mapea de Morado a Amarillo
    hueVal = map(normD, 0.5, 1, 280, 410) % 360; 
  }

  stroke(hueVal, 220, 255);
  fill(hueVal, 220, 255, 150);
  ellipse(p.pos.x, p.pos.y, 5, 5);
}

function windowResized() {
  let h = windowHeight;
  let w = h * (9 / 16);
  if (w > windowWidth) {
    w = windowWidth;
    h = w * (16 / 9);
  }
  resizeCanvas(w, h);
}
```
Este intento salio no tanto como esperaba, se demora bastante en llegar las partículas y son muy grandes, esto se corrige facil cambiando el tamaño de partículas y su velocidad, además de poner un slider.
<img width="416" height="772" alt="image" src="https://github.com/user-attachments/assets/8016b6f2-9005-43c9-a7e2-d1e60dccb650" />

##Versión Final
  ``` js
/* noprotect */

let tree = [];
let walkers = [];
let userCores = [];
const MAX_USER_CORES = 3;
const NUM_WALKERS = 180; 
const STICK_DISTANCE = 4.5; 

// Grilla espacial de optimización
const GRID_SIZE = 12; 
let grid = {};

let initialSeedCreated = false;
let startTime;
let primarySeedPos = null;

// UI
let speedSlider;
let resetButton;

function setup() {
  let h = windowHeight;
  let w = h * (9 / 16);
  if (w > windowWidth) {
    w = windowWidth;
    h = w * (16 / 9);
  }
  createCanvas(w, h);
  colorMode(HSB, 360, 255, 255, 255);

  // Slider de Velocidad
  speedSlider = createSlider(1, 30, 8, 1);
  speedSlider.position(15, 15);
  speedSlider.style('width', '90px');
  speedSlider.style('opacity', '0.8');

  // Botón de Reinicio Manual
  resetButton = createButton('Reiniciar');
  resetButton.position(120, 15);
  resetButton.style('opacity', '0.8');
  resetButton.style('background-color', '#1a1a2e');
  resetButton.style('color', '#ffffff');
  resetButton.style('border', '1px solid #4a4e69');
  resetButton.style('border-radius', '4px');
  resetButton.style('padding', '2px 8px');
  resetButton.style('cursor', 'pointer');
  resetButton.mousePressed(resetSimulation);

  resetSimulation();
}

function resetSimulation() {
  tree = [];
  walkers = [];
  userCores = [];
  grid = {};
  initialSeedCreated = false;
  primarySeedPos = null;
  startTime = millis();

  for (let i = 0; i < NUM_WALKERS; i++) {
    walkers.push(new Walker());
  }
}

function getGridKey(x, y) {
  let gx = Math.floor(x / GRID_SIZE);
  let gy = Math.floor(y / GRID_SIZE);
  return gx + "," + gy;
}

function addToGrid(particle) {
  let key = getGridKey(particle.pos.x, particle.pos.y);
  if (!grid[key]) grid[key] = [];
  grid[key].push(particle);
}

function addTreeParticle(x, y) {
  let p = new TreeParticle(x, y, getDistanceToPrimary(createVector(x, y)));
  tree.push(p);
  addToGrid(p);
  return p;
}

function draw() {
  background(10, 20, 15);

  drawUI();

  if (!initialSeedCreated && millis() - startTime > 5000) {
    createInitialSeed(width / 2 + random(-20, 20), height / 2 + random(-20, 20));
  }

  // Dibujar núcleos adicionales
  fill(50, 255, 255, 120);
  noStroke();
  for (let core of userCores) {
    ellipse(core.x, core.y, 10, 10);
  }

  // Dibujar estructura fractal
  for (let p of tree) {
    drawParticle(p);
  }

  if (!initialSeedCreated) {
    fill(0, 0, 255, 150 + sin(frameCount * 0.1) * 100);
    textAlign(CENTER, CENTER);
    textSize(13);
    text("Haz clic para colocar la semilla inicial\n(o espera 5s)", width / 2, height / 2);
    return;
  }

  // Control de velocidad por tiempo seguro
  let stepsPerFrame = speedSlider.value();
  let maxTimeMs = 12; 
  let frameStart = millis();

  for (let step = 0; step < stepsPerFrame; step++) {
    for (let i = 0; i < walkers.length; i++) {
      walkers[i].walk();
      
      if (walkers[i].checkCollision()) {
        addTreeParticle(walkers[i].pos.x, walkers[i].pos.y);
        walkers[i] = new Walker();
      }
    }
    
    if (millis() - frameStart > maxTimeMs) {
      break;
    }
  }

  // Dibujar walkers
  for (let w of walkers) {
    w.show();
  }
}

function drawUI() {
  push();
  fill(0, 0, 255, 200);
  noStroke();
  textSize(11);
  textAlign(LEFT, TOP);
  text("Velocidad: " + speedSlider.value() + "x", 15, 33);
  pop();
}

function getDistanceToPrimary(pos) {
  if (!primarySeedPos) return 0;
  return dist(pos.x, pos.y, primarySeedPos.x, primarySeedPos.y);
}

function createInitialSeed(x, y) {
  primarySeedPos = createVector(x, y);
  addTreeParticle(x, y);
  initialSeedCreated = true;
}

function mousePressed() {
  // Ignorar clics sobre la UI (Slider y Botón)
  if (mouseX >= 10 && mouseX <= 200 && mouseY >= 10 && mouseY <= 55) return;
  if (mouseX < 0 || mouseX > width || mouseY < 0 || mouseY > height) return;

  if (!initialSeedCreated) {
    createInitialSeed(mouseX, mouseY);
  } else {
    if (userCores.length >= MAX_USER_CORES) {
      let oldestCore = userCores.shift();
      releaseCoreAsWalkers(oldestCore);
    }
    
    let newCore = createVector(mouseX, mouseY);
    userCores.push(newCore);
    addTreeParticle(newCore.x, newCore.y);
  }
}

function releaseCoreAsWalkers(corePos) {
  for (let i = tree.length - 1; i >= 0; i--) {
    if (dist(tree[i].pos.x, tree[i].pos.y, corePos.x, corePos.y) < 20) {
      tree.splice(i, 1);
    }
  }
  grid = {};
  for (let p of tree) addToGrid(p);
}

// --- CLASE WALKER CON LÉVY FLIGHT ---
class Walker {
  constructor() {
    this.spawn();
  }

  spawn() {
    let side = floor(random(4));
    let x, y;

    let gx = randomGaussian(mouseX, width * 0.2);
    let gy = randomGaussian(mouseY, height * 0.2);

    if (side === 0) { x = random(width); y = 0; }
    else if (side === 1) { x = width; y = random(height); }
    else if (side === 2) { x = random(width); y = height; }
    else { x = 0; y = random(height); }

    if (side === 0 || side === 2) x = constrain(gx, 0, width);
    else y = constrain(gy, 0, height);

    this.pos = createVector(x, y);
  }

  // Generación del salto con distribución de ley de potencia
  levyStep() {
    // Probabilidad de Ley de Potencia (Lévy Flight)
    let r = random(1);
    // Exponente de Lévy: Pasos mayoritariamente cortos, pero saltos gigantes muy probables
    let stepSize = pow(1 - r, -0.4) * 1.5; 
    
    // Limitar longitud máxima para estabilidad
    stepSize = min(stepSize, width * 0.4);

    let step = p5.Vector.random2D();
    step.mult(stepSize);
    return step;
  }

  walk() {
    let step = this.levyStep();
    this.pos.add(step);

    this.pos.x = constrain(this.pos.x, 0, width);
    this.pos.y = constrain(this.pos.y, 0, height);
  }

  checkCollision() {
    let gx = Math.floor(this.pos.x / GRID_SIZE);
    let gy = Math.floor(this.pos.y / GRID_SIZE);

    for (let x = -1; x <= 1; x++) {
      for (let y = -1; y <= 1; y++) {
        let key = (gx + x) + "," + (gy + y);
        let neighbors = grid[key];
        
        if (neighbors) {
          for (let i = 0; i < neighbors.length; i++) {
            let d = dist(this.pos.x, this.pos.y, neighbors[i].pos.x, neighbors[i].pos.y);
            if (d < STICK_DISTANCE) {
              return true;
            }
          }
        }
      }
    }
    return false;
  }

  show() {
    stroke(255, 40);
    strokeWeight(1);
    point(this.pos.x, this.pos.y);
  }
}

// --- CLASE ESTRUCTURA Y DIBUJO ---
class TreeParticle {
  constructor(x, y, dFromSeed) {
    this.pos = createVector(x, y);
    this.dist = dFromSeed;
  }
}

function drawParticle(p) {
  let maxD = width * 0.65;
  let normD = constrain(p.dist / maxD, 0, 1);
  
  let hueVal;
  if (normD < 0.5) {
    hueVal = map(normD, 0, 0.5, 200, 280); 
  } else {
    hueVal = map(normD, 0.5, 1, 280, 410) % 360; 
  }

  stroke(hueVal, 220, 255, 200);
  fill(hueVal, 220, 255, 180);
  ellipse(p.pos.x, p.pos.y, 3, 3);
}

function windowResized() {
  let h = windowHeight;
  let w = h * (9 / 16);
  if (w > windowWidth) {
    w = windowWidth;
    h = w * (16 / 9);
  }
  resizeCanvas(w, h);
  speedSlider.position(15, 15);
  resetButton.position(120, 15);
}
  ``` 
