# Unidad 4
<a name="6"></a>
## Instrumento funcional
[Link a instrumento](https://almos21.github.io/kuramoto-calaveras/)

## Idea
Para este proyecto mi idea fue hacer un escenario con una chica en el medio que fuera cantando, y los demás agentes fueran calaveras alrededor siendo picoteadas por cuervos, el oscilador interno de estos es lo que indica cada cuanto picotean y el kuramoto se ve aplicado ya que cada grito de calavera va haciendo que los cuervos cambien su ritmo interno y se vayan sincronizando, además de esto queria que la chica llevara la batuta del tiempo así que su influencia es mayor al de los cuervos (esto modificando el kuramoto).
<img width="3840" height="2160" alt="IMG_0253" src="https://github.com/user-attachments/assets/8b0a52ef-8c34-4d4f-b535-7844fa443348" />

<a name="1"></a>
## Implementación del modelo obligatorio
Se implementó el modelo con un cambio y fue la adición de `w_ij` esta es una variable que se multiplica en la sumatoria y deja la ecuación así: `dθ_i/dt = ω_i + (K/(N-1)) Σ_j w_ij · sin(θ_j - θ_i)` su intención es permitir que el valor dependa de quien canta y que tan cerca está, para así que la cantante lleve el ritmo base y las calaveras se alteren más de las cercanas que de las lejanas. En la aplicación la oscilación se representa con cada picoteo seguido de un sonido por la calavera y su frecuencia se evidencia con el aumento y disminución de cada cuanto esto pasa, la oscilación se ve alterada por el click que asusta a el cuervo y descuadra su reloj interno
<a name="2"></a>
## Requisitos mínimos
### 8 agentes simultáneos y 4 personalidades audiovisuales diferentes minimas.
Son 8 agentes distintos en apariencia y sonido, además de diferentes parámetros de oscilación. Cada uno tiene un sonido distinto que esta editado para sonar en una nota específica, originalmente pensé en que fueran notas que armonizaran, pero al hacer los primeros sonidos me encantó lo chistoso que sonaban y como quedaba de bien con la imagen de las calaveras.
### El usuario deberá poder modificar en tiempo real al menos 2 variables relacionadas con el modelo, siendo obligatorio poder intervenir (K).
El usuario puede usar el click para alterar el reloj interno y que a su vez disminuye por un tiempo k, para que demore un rato en que se sincronicen de nuevo. Además de esto con las flechas del teclado puede subir o bajar ω de la cantante, para así modificar la velocidad y ritmo general de la composición.
### La experiencia deberá permitir reconocer al menos 3 estados colectivos: desorden, organización parcial y organización estable
Esto es notorio a partir de el comportamiento de las calaveras, al inicio sus cantos son muy disparejos y de a poco van acoplándose. 

## Códigos
### Sketch
``` js
/*
  sketch.js
  ---------
  Simulación de sincronización basada en el modelo de Kuramoto:

      dθ_i/dt = ω_i + (K/N) * Σ_j w_ij * sin(θ_j - θ_i)

  Cada oscilador (la cantante + 7 calaveras) tiene una fase θ que avanza
  con el tiempo. Cuando la fase de un oscilador completa una vuelta
  (θ pasa por un múltiplo de 2π), eso ES el "picoteo": dispara la
  animación y el audio de ese personaje. Como en el modelo clásico de
  luciérnagas sincronizándose, θ es literalmente el reloj interno de
  cada personaje.

  w_ij (peso del acoplamiento) NO es uniforme:
    - Si la fuente j es la cantante, su influencia se multiplica por
      CONFIG.kuramoto.singerWeightMult -> "ella rige el tiempo".
    - Para cualquier par, el peso decae con la distancia real entre sus
      posiciones lógicas -> las calaveras cercanas se sincronizan más
      rápido entre sí que las lejanas.

  Un clic en una calavera no la sincroniza: espanta al ave (sin sprite,
  solo audio "ave") y perturba su fase de vuelta al caos, deshaciendo el
  progreso de sincronización que llevaba.
*/

let img = { skulls: [] };
let snd = { skulls: [] };

let singer;      // estado del oscilador de la cantante
let skulls = []; // estado de los 7 osciladores de calaveras

let showDebug = false;
let assetsOk = true;

// K dinámico: cuánto se le resta al K base ahora mismo. Sube de golpe con
// cada susto y decae solo con el tiempo (ver stepKuramoto).
let kDeficit = 0;

// Colliders "vivos" durante el modo de calibración (coordenadas de canvas,
// se inicializan desde config.js y se editan con el mouse). Se convierten
// de vuelta a coordenadas de 4K solo al exportar (tecla P).
let working = null;
let drag = null; // { target: 'singer'|skullId, mode: 'move'|'resize', ... }
const HANDLE = 16; // tamaño del cuadrito de redimensionar, en px de canvas

function preload() {
  // Si algún archivo no existe, p5 avisará en consola pero no debe romper
  // la simulación entera: seguimos igual, solo no se verá ese sprite.

  img.background = loadImage(CONFIG.background.image, () => {}, onAssetError);

  img.singerQuieta   = loadImage(CONFIG.singer.images.quieta,   () => {}, onAssetError);
  img.singerCantando = loadImage(CONFIG.singer.images.cantando, () => {}, onAssetError);
  snd.singer          = loadSound(CONFIG.singer.audio, () => {}, onAssetError);

  for (const s of CONFIG.skulls) {
    img.skulls[s.id] = {
      normal: loadImage(s.images.normal, () => {}, onAssetError),
      peck:   loadImage(s.images.peck,   () => {}, onAssetError),
      scream: loadImage(s.images.scream, () => {}, onAssetError),
    };
    snd.skulls[s.id] = loadSound(s.audio, () => {}, onAssetError);
  }

  snd.ave = loadSound(CONFIG.ave.audio, () => {}, onAssetError);
}

function onAssetError(err) {
  assetsOk = false;
  console.warn('No se pudo cargar un asset (revisa las rutas en config.js):', err);
}

// Convierte coordenadas escritas en config.js (resolución de 4K de tus
// sprites) al tamaño real del canvas, según CONFIG.canvas.scale.
function scaledPoint(p) {
  const S = CONFIG.canvas.scale;
  return { x: p.x * S, y: p.y * S };
}

function scaledRect(r) {
  const S = CONFIG.canvas.scale;
  return { x: r.x * S, y: r.y * S, w: r.w * S, h: r.h * S };
}

// Inversa de scaledRect: de coordenadas de canvas de vuelta a las
// coordenadas de 4K que se escriben en config.js.
function unscaledRect(r) {
  const S = CONFIG.canvas.scale;
  return { x: round(r.x / S), y: round(r.y / S), w: round(r.w / S), h: round(r.h / S) };
}

function getWorkingRect(target) {
  return target === 'singer' ? working.singer : working.skulls[target];
}

function setup() {
  const S = CONFIG.canvas.scale;
  createCanvas(CONFIG.canvas.sourceW * S, CONFIG.canvas.sourceH * S);
  angleMode(RADIANS);

  singer = {
    theta: random(TWO_PI),
    omega: CONFIG.singer.omegaBase,
    phase: 'quieta',      // 'quieta' | 'cantando'
    lapCount: 0,
  };

  skulls = CONFIG.skulls.map((s) => ({
    id: s.id,
    theta: random(TWO_PI),
    omega: s.omegaBase + random(-0.3, 0.3), // jitter ampliado — arranca más disperso, más caos inicial
    phase: 'normal',       // 'normal' | 'peck' | 'scream'
    timer: 0,
    lapCount: 0,
  }));

  // Copia editable de los colliders para el modo de calibración
  working = {
    singer: scaledRect(CONFIG.singer.collider),
    skulls: CONFIG.skulls.map(s => scaledRect(s.collider)),
  };
}

function draw() {
  background(8, 6, 14);

  const dt = min(deltaTime / 1000, 0.05); // clamp por si hay un frame lento
  stepKuramoto(dt);
  updateStateMachines(dt);

  drawBackground();
  drawSinger();
  drawSkulls();

  if (showDebug) drawDebug();
  if (!assetsOk) drawAssetWarning();
}

// ---------------------------------------------------------------------
// MODELO DE KURAMOTO
// ---------------------------------------------------------------------

function couplingWeight(sourceIsSinger, dist) {
  const base = sourceIsSinger ? CONFIG.kuramoto.singerWeightMult : 1.0;
  const falloff = exp(-dist / CONFIG.kuramoto.distanceFalloff);
  return base * falloff;
}

// K_efectivo(t) = max(scareKMin, K_base - kDeficit). kDeficit se alimenta
// en scareSkull() y decae solo cada frame (ver el final de stepKuramoto).
function currentK() {
  return max(CONFIG.kuramoto.scareKMin, CONFIG.kuramoto.K - kDeficit);
}

function stepKuramoto(dt) {
  // Armamos un arreglo homogéneo: índice 0 = cantante, 1..7 = calaveras
  const n = 1 + skulls.length;
  const theta = [singer.theta, ...skulls.map(s => s.theta)];
  const omega = [singer.omega, ...skulls.map(s => s.omega)];
  const pos = [scaledPoint(CONFIG.singer.pos), ...CONFIG.skulls.map(s => scaledPoint(s.pos))];
  const K = currentK();

  const dtheta = new Array(n).fill(0);

  for (let i = 0; i < n; i++) {
    let sum = 0;
    for (let j = 0; j < n; j++) {
      if (j === i) continue;
      const d = dist(pos[i].x, pos[i].y, pos[j].x, pos[j].y);
      const w = couplingWeight(j === 0 /* fuente es la cantante */, d);
      sum += w * sin(theta[j] - theta[i]);
    }
    dtheta[i] = omega[i] + (K / (n - 1)) * sum;
  }

  // Aplicamos y detectamos "vueltas" (laps) completas -> disparan eventos
  const prevSingerTheta = singer.theta;
  singer.theta += dtheta[0] * dt;
  if (floor(singer.theta / TWO_PI) > floor(prevSingerTheta / TWO_PI)) {
    onSingerLap();
  }

  skulls.forEach((s, idx) => {
    const prev = s.theta;
    s.theta += dtheta[idx + 1] * dt;
    if (floor(s.theta / TWO_PI) > floor(prev / TWO_PI)) {
      onSkullLap(s);
    }
  });

  // kDeficit decae exponencialmente hacia 0 -> K se va recuperando solo
  kDeficit *= exp(-dt / CONFIG.kuramoto.scareKRecoveryTau);
}

// ---------------------------------------------------------------------
// EVENTOS DE "VUELTA COMPLETA" (equivalen al picoteo / canto)
// ---------------------------------------------------------------------

function onSingerLap() {
  if (singer.phase !== 'quieta') return; // ya está cantando, no se re-dispara
  singer.phase = 'cantando';
  singer.lapCount++;
  if (snd.singer && snd.singer.isLoaded()) snd.singer.play();
}

function onSkullLap(s) {
  if (s.phase !== 'normal') return; // ya está en su ciclo de picoteo/grito
  s.phase = 'peck';
  s.timer = 0;
  s.lapCount++;
}

// ---------------------------------------------------------------------
// MÁQUINAS DE ESTADO (sprites + audio)
// ---------------------------------------------------------------------

function updateStateMachines(dt) {
  // Cantante: cuando termina su audio, vuelve a 'quieta'
  if (singer.phase === 'cantando') {
    if (snd.singer && snd.singer.isLoaded() && !snd.singer.isPlaying()) {
      singer.phase = 'quieta';
    }
  }

  for (const s of skulls) {
    if (s.phase === 'peck') {
      s.timer += dt;
      if (s.timer >= CONFIG.timing.peckDuration) {
        s.phase = 'scream';
        const sound = snd.skulls[s.id];
        if (sound && sound.isLoaded()) sound.play();
      }
    } else if (s.phase === 'scream') {
      const sound = snd.skulls[s.id];
      if (sound && sound.isLoaded() && !sound.isPlaying()) {
        s.phase = 'normal';
      }
    }
  }
}

// ---------------------------------------------------------------------
// INTERACCIÓN: teclado (velocidad de la cantante) y clic (espantar ave)
// ---------------------------------------------------------------------

function keyPressed() {
  if (key === 'd' || key === 'D') {
    showDebug = !showDebug;
    return;
  }
  if (showDebug && (key === 'p' || key === 'P')) {
    printCalibration();
    return;
  }
  if (keyCode === UP_ARROW) {
    singer.omega = constrain(singer.omega + CONFIG.singer.omegaStep, CONFIG.singer.omegaMin, CONFIG.singer.omegaMax);
  } else if (keyCode === DOWN_ARROW) {
    singer.omega = constrain(singer.omega - CONFIG.singer.omegaStep, CONFIG.singer.omegaMin, CONFIG.singer.omegaMax);
  }
}

// Imprime en la consola del navegador (F12) los valores de collider
// actuales, ya en coordenadas de 4K, listos para pegar en config.js.
function printCalibration() {
  const lines = [];
  lines.push('--- Valores de collider (pega esto en config.js) ---');
  const sc = unscaledRect(working.singer);
  lines.push(`singer.collider: { x: ${sc.x}, y: ${sc.y}, w: ${sc.w}, h: ${sc.h} }`);
  working.skulls.forEach((r, i) => {
    const c = unscaledRect(r);
    lines.push(`skulls[${i}].collider: { x: ${c.x}, y: ${c.y}, w: ${c.w}, h: ${c.h} }`);
  });
  console.log(lines.join('\n'));
}

function mousePressed() {
  if (showDebug) {
    startCalibrationDrag();
    return;
  }
  for (const s of skulls) {
    const c = scaledRect(CONFIG.skulls[s.id].collider);
    if (mouseX >= c.x && mouseX <= c.x + c.w && mouseY >= c.y && mouseY <= c.y + c.h) {
      scareSkull(s);
      return; // solo una calavera por clic
    }
  }
}

function startCalibrationDrag() {
  const targets = ['singer', ...skulls.map(s => s.id)];
  for (const target of targets) {
    const r = getWorkingRect(target);
    // Zona de la esquina inferior derecha -> redimensionar
    const hx = r.x + r.w, hy = r.y + r.h;
    if (mouseX >= hx - HANDLE && mouseX <= hx + HANDLE / 2 && mouseY >= hy - HANDLE && mouseY <= hy + HANDLE / 2) {
      drag = { target, mode: 'resize', startW: r.w, startH: r.h, startMouseX: mouseX, startMouseY: mouseY };
      return;
    }
    // Cuerpo del rectángulo -> mover
    if (mouseX >= r.x && mouseX <= r.x + r.w && mouseY >= r.y && mouseY <= r.y + r.h) {
      drag = { target, mode: 'move', offsetX: mouseX - r.x, offsetY: mouseY - r.y };
      return;
    }
  }
}

function mouseDragged() {
  if (!showDebug || !drag) return;
  const r = getWorkingRect(drag.target);
  if (drag.mode === 'move') {
    r.x = mouseX - drag.offsetX;
    r.y = mouseY - drag.offsetY;
  } else if (drag.mode === 'resize') {
    r.w = max(10, drag.startW + (mouseX - drag.startMouseX));
    r.h = max(10, drag.startH + (mouseY - drag.startMouseY));
  }
}

function mouseReleased() {
  drag = null;
}

function scareSkull(s) {
  // Cancela cualquier animación/audio en curso y vuelve a sprite normal
  const sound = snd.skulls[s.id];
  if (sound && sound.isPlaying()) sound.stop();
  s.phase = 'normal';
  s.timer = 0;

  // Suena el audio predeterminado del ave asustada
  if (snd.ave && snd.ave.isLoaded()) {
    if (snd.ave.isPlaying()) snd.ave.stop();
    snd.ave.play();
  }

  // Perturba su fase -> la empuja de vuelta a un estado caótico,
  // deshaciendo el progreso de sincronización que tenía con sus vecinas.
  const sign = random() < 0.5 ? -1 : 1;
  s.theta += sign * random(CONFIG.kuramoto.scarePerturbMin, CONFIG.kuramoto.scarePerturbMax);

  // Además, el susto le resta al K GLOBAL del sistema (no solo a esta
  // calavera): todo el sistema se sincroniza menos por un rato, y se va
  // recuperando solo (ver el decaimiento de kDeficit en stepKuramoto).
  const maxDeficit = CONFIG.kuramoto.K - CONFIG.kuramoto.scareKMin;
  kDeficit = min(kDeficit + CONFIG.kuramoto.scareKDrop, maxDeficit);
}

// ---------------------------------------------------------------------
// DIBUJO
// ---------------------------------------------------------------------

function drawBackground() {
  if (img.background) {
    image(img.background, 0, 0, width, height);
  }
}

function drawSinger() {
  const im = singer.phase === 'cantando' ? img.singerCantando : img.singerQuieta;
  if (im) image(im, 0, 0, width, height);
}

function drawSkulls() {
  for (const s of skulls) {
    const set = img.skulls[s.id];
    if (!set) continue;
    const im = set[s.phase]; // 'normal' | 'peck' | 'scream'
    if (im) image(im, 0, 0, width, height);
  }
}

function drawDebug() {
  textSize(13);

  fill(255, 220, 80);
  noStroke();
  text(`K_efectivo = ${currentK().toFixed(2)}  (base ${CONFIG.kuramoto.K.toFixed(2)}, déficit ${kDeficit.toFixed(2)})`, 12, 20);

  drawCalibBox(working.singer, [0, 200, 255], 'cantante');
  skulls.forEach((s, i) => {
    drawCalibBox(working.skulls[i], [255, 80, 80], `#${s.id}`);
  });

  fill(255);
  noStroke();
  textSize(13);
  text('Modo calibración: arrastra el cuerpo para mover, la esquina inferior-derecha para redimensionar. P = imprimir valores en consola.', 12, height - 16);
}

function drawCalibBox(r, col, label) {
  noFill();
  stroke(col[0], col[1], col[2]);
  strokeWeight(2);
  rect(r.x, r.y, r.w, r.h);

  // Handle de redimensionar (esquina inferior derecha)
  fill(col[0], col[1], col[2]);
  noStroke();
  rect(r.x + r.w - HANDLE / 2, r.y + r.h - HANDLE / 2, HANDLE, HANDLE);

  // Valores en coordenadas de 4K (las que van en config.js)
  const c = unscaledRect(r);
  fill(col[0], col[1], col[2]);
  noStroke();
  text(`${label}  x:${c.x} y:${c.y} w:${c.w} h:${c.h}`, r.x, r.y - 6);
}

function drawAssetWarning() {
  fill(255, 60, 60);
  noStroke();
  textSize(14);
  text('Faltan uno o más archivos en assets/ — revisa la consola y las rutas en config.js', 12, height - 16);
}
```
## Index
``` html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Kuramoto Calaveras</title>
  <style>
    html, body { margin: 0; padding: 0; background: #000; overflow: hidden; }
    canvas { display: block; margin: 0 auto; }
  </style>
</head>
<body>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.4/p5.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.4/addons/p5.sound.min.js"></script>
  <script src="config.js"></script>
  <script src="sketch.js"></script>
</body>
</html>
```
## Config
``` js
/*
  CONFIG.js
  ---------
  Todo lo que necesitas editar para calzar tus sprites está aquí.
  No toques sketch.js a menos que quieras cambiar la lógica del modelo.

  IMPORTANTE sobre los sprites:
  Como cada imagen es del tamaño completo de la ventana (con transparencia
  alrededor del personaje dibujado), cada sprite se dibuja SIEMPRE en
  (0,0) cubriendo todo el canvas — nunca se recorta ni se reposiciona.
  Lo único que cambia entre personajes es el "collider" (la caja/círculo
  invisible que usamos para detectar el mouse) y la posición lógica
  "pos" que se usa solo para calcular distancias en el acoplamiento
  de Kuramoto (qué tan cerca están un cráneo de otro / de la cantante).

  Presiona la tecla "D" en la simulación para ver los colliders dibujados
  encima y calibrarlos visualmente.

  SOBRE RESOLUCIÓN Y ESCALA:
  Tus sprites están hechos en 3840x2160 (4K). Dibujarlos así de grandes en
  el navegador es innecesariamente pesado, así que el canvas real se
  calcula como sourceW*scale x sourceH*scale (con scale=0.5 -> 1920x1080).
  TODAS las posiciones y colliders de abajo se escriben en las coordenadas
  ORIGINALES de 4K (las mismas que ves en tu editor de imagen/Photoshop) —
  el código las reescala automáticamente, no tienes que hacer la cuenta tú.
  Si quieres un canvas aún más liviano, baja "scale" (ej. 0.35).
  Nota: escalar aquí reduce el tamaño de RENDER, no el peso de descarga de
  los PNG — si el peso de la página (tiempo de carga) te importa, exporta
  también versiones más livianas de los PNG/MP3 del lado de tu editor.
*/

const CONFIG = {

  canvas: {
    sourceW: 3840,   // ancho con el que exportaste tus sprites
    sourceH: 2160,   // alto con el que exportaste tus sprites
    scale: 0.5,      // factor de escala para el canvas real (0.5 -> 1920x1080)
  },

  background: {
    image: 'assets/background.PNG', // se dibuja primero, detrás de la cantante y las calaveras
  },

  // ---------- MODELO DE KURAMOTO ----------
  kuramoto: {
    K: 1.6,                // fuerza de acoplamiento global BASE — bajado de 1.6 para que tarde más en sincronizar
    singerWeightMult: 3,  // cuánto más pesa el valor de la cantante θ_j cuando aparece en la ecuación de OTROS — bajado de 4.0
    distanceFalloff: 1500,   // px (en el canvas ya escalado). Bajado de 700: el acoplamiento llega a menos distancia,
                             // así que el contagio entre calaveras lejanas es más lento.
    scarePerturbMin: Math.PI * 0.9,  // al asustar un cráneo (clic), cuánto se perturba su fase como mínimo
    scarePerturbMax: Math.PI * 2.0,  // y como máximo (empuja al cráneo de vuelta a un estado caótico)

    // K dinámico: cada susto resta de golpe al K global (no solo perturba
    // la fase de esa calavera), y se recupera solo con el tiempo.
    // K_efectivo(t) = max(scareKMin, K - kDeficit(t)), donde kDeficit decae
    // exponencialmente: kDeficit(t+dt) = kDeficit(t) * e^(-dt/scareKRecoveryTau)
    scareKDrop: 0.6,          // cuánto le resta a K cada vez que asustas una calavera
    scareKRecoveryTau: 3.0,   // segundos que tarda en recuperarse (más alto = recuperación más lenta)
    scareKMin: 0.2,           // piso mínimo, K nunca cae más abajo de esto
  },

  // ---------- CANTANTE (rige el tiempo) ----------
  singer: {
    omegaBase: 1.0,     // frecuencia natural (rad/s) inicial
    omegaStep: 0.15,    // cuánto cambia con cada pulsación de flecha ↑ / ↓
    omegaMin: 0.15,
    omegaMax: 4.0,
    pos: { x: 1920, y: 1080 }, // posición lógica (para distancias), EN COORDENADAS DE 4K
    collider: { x: 1680, y: 510, w: 758, h: 1264 }, // EDITA esto para calzar tu sprite, EN COORDENADAS DE 4K
    images: {
      quieta:   'assets/singer_quieta.PNG',
      cantando: 'assets/singer_cantando.PNG',
    },
    audio: 'assets/singer.mp3',
  },

  // ---------- LAS 7 CALAVERAS ----------
  // "pos" = posición lógica aproximada del cráneo en el frame, usada SOLO
  // para calcular distancias (acoplamiento más fuerte entre vecinos cercanos).
  // "collider" = caja de detección de clic, EDITA x/y/w/h para calzar tu arte.
  // Todos los valores están en coordenadas de 4K (3840x2160), igual que tus sprites.
  skulls: [
    { id: 0, pos: { x: 360, y: 900 }, collider: { x: 2726, y: 46, w: 402, h: 408 },
      omegaBase: 0.55,
      images: { normal: 'assets/skull0_normal.PNG', peck: 'assets/skull0_peck.PNG', scream: 'assets/skull0_scream.PNG' },
      audio: 'assets/skull0.mp3' },

    { id: 1, pos: { x: 810, y: 1260 }, collider: { x: 3366, y: 528, w: 440, h: 496 },
      omegaBase: 1.35,
      images: { normal: 'assets/skull1_normal.PNG', peck: 'assets/skull1_peck.PNG', scream: 'assets/skull1_scream.PNG' },
      audio: 'assets/skull1.mp3' },

    { id: 2, pos: { x: 1260, y: 1560 }, collider: { x: 2028, y: 18, w: 494, h: 422 } ,
      omegaBase: 0.45,
      images: { normal: 'assets/skull2_normal.PNG', peck: 'assets/skull2_peck.PNG', scream: 'assets/skull2_scream.PNG' },
      audio: 'assets/skull2.mp3' },

    { id: 3, pos: { x: 2580, y: 1560 }, collider: { x: 2944, y: 1454, w: 752, h: 434 } ,
      omegaBase: 1.55,
      images: { normal: 'assets/skull3_normal.PNG', peck: 'assets/skull3_peck.PNG', scream: 'assets/skull3_scream.PNG' },
      audio: 'assets/skull3.mp3' },

    { id: 4, pos: { x: 3030, y: 1260 }, collider: { x: 742, y: 1088, w: 372, h: 450 },
      omegaBase: 0.65,
      images: { normal: 'assets/skull4_normal.PNG', peck: 'assets/skull4_peck.PNG', scream: 'assets/skull4_scream.PNG' },
      audio: 'assets/skull4.mp3' },

    { id: 5, pos: { x: 3480, y: 900 }, collider: { x: 344, y: 690, w: 386, h: 400 },
      omegaBase: 1.45,
      images: { normal: 'assets/skull5_normal.PNG', peck: 'assets/skull5_peck.PNG', scream: 'assets/skull5_scream.PNG' },
      audio: 'assets/skull5.mp3' },

    { id: 6, pos: { x: 1920, y: 1860 }, collider: { x: 948, y: 12, w: 816, h: 428 },
      omegaBase: 1.75,
      images: { normal: 'assets/skull6_normal.PNG', peck: 'assets/skull6_peck.PNG', scream: 'assets/skull6_scream.PNG' },
      audio: 'assets/skull6.mp3' },
  ],

  // Sonido fijo del "ave asustada" al hacer clic en cualquier cráneo
  ave: { audio: 'assets/ave.mp3' },

  timing: {
    peckDuration: 0.35, // segundos que se ve el sprite "ave picoteando" antes de pasar al grito + audio
  },
};
```

### Autoevaluación:
| Criterio | Puntos | Evidencia|
|----------|:-------:|-----------|
| Leí y verifiqué que mi proyecto cumple con los requisitos mínimos de la unidad | 25 | [Evidencia](#2)|
| Puedo explicar claramente qué representa cada variable del modelo de Kuramoto en mi proyecto | 25 | [Evidencia](#1) |
| Puedo explicar claramente cómo las variables del modelo producen el comportamiento observado en mi proyecto | 25 | [Evidencia](#1)  |
| Puedo demostrar que mi proyecto cumple con los objetivos establecidos en la unidad | 25 | [Evidencia](#2) |

Total: 100
Nota: 5

