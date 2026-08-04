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

En la primera prueba ocurrió lo siguiente, empezó con muchas pero siempre terminaban muy pocas, no llevaban a patrones o movimientos interesantes y terminaba en una simulación muy simple 

<img width="932" height="947" alt="image" src="https://github.com/user-attachments/assets/6ce4aa1e-b2de-4d0d-9a11-39fa924b19c3" />

Un segundo cambio donde se configuró la población de la voracidad, crecimiento de la población y cuadrar los patrones sociales, resultaba en esto donde se juntaban los sociales y los nómadas eran lo que terminaban formando cúmulos


<img width="878" height="818" alt="image" src="https://github.com/user-attachments/assets/f58c124b-cf45-408a-8ae9-bd5774040c23" />

Esta fue la versión final después de tener que hacer unos cambios, debido a que la voracidad comía sin control siempre terminaba ganando sobre la población, para esto se le puso varias reglas, ahora tiene una saciedad y si pasa un tiempo sin comer muere

<img width="874" height="808" alt="image" src="https://github.com/user-attachments/assets/a8a591f9-ea14-44a2-b82b-26be0d4d2827" />

### Diferentes manifestaciones:
50 nómadas y solo 2 Voracidad, pero con 5 de velocidad, en esta la propagación logró establecer mejor sus poblaciones

<img width="875" height="814" alt="image" src="https://github.com/user-attachments/assets/e9beff4a-a2b4-4049-bd47-89e8c2101377" />

200 nómadas y más velocidad, además 600 de comida inicial, los nómadas la devoran enseguida y dominan el lugar

<img width="873" height="811" alt="image" src="https://github.com/user-attachments/assets/2cf1ec5a-93f5-4d68-8b54-069d612084a4" />

Lo mismo pero con los sociales, forman notables colonias.

<img width="874" height="810" alt="image" src="https://github.com/user-attachments/assets/f25ebc50-21a4-4ac6-bf10-310650fdca71" />

``` html
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Voracidad &amp; Propagación — Equilibrio Cósmico</title>
<style>
  html,body{margin:0;padding:0;overflow:hidden;background:#040308;font-family:'Georgia',serif;}
  canvas{display:block;}
  #hud{
    position:fixed; top:14px; left:14px; z-index:10;
    background:rgba(10,8,20,0.65); backdrop-filter:blur(8px);
    border:1px solid rgba(200,170,255,0.25); border-radius:10px;
    padding:12px 16px; color:#e8dfff; font-size:12px; letter-spacing:0.4px;
    box-shadow:0 0 30px rgba(120,60,200,0.15); min-width:220px;
  }
  #hud h1{font-size:13px; margin:0 0 8px 0; font-weight:600; letter-spacing:1.5px;
    background:linear-gradient(90deg,#ffd97a,#ff6ad5,#7ad9ff);
    -webkit-background-clip:text; background-clip:text; color:transparent; text-transform:uppercase;}
  #hud .row{display:flex; justify-content:space-between; gap:14px; margin:3px 0; font-family:'Courier New',monospace;}
  #hud .dot{display:inline-block;width:8px;height:8px;border-radius:50%;margin-right:6px;}
  #hud .sub{opacity:0.6; font-size:10px; margin-top:8px; line-height:1.4; font-family:'Georgia',serif;}
  #controls{
    position:fixed; bottom:14px; left:14px; z-index:10; display:flex; gap:8px;
  }
  #controls button{
    background:rgba(20,14,34,0.75); border:1px solid rgba(200,170,255,0.3); color:#e8dfff;
    padding:7px 14px; border-radius:8px; font-size:11px; cursor:pointer; letter-spacing:0.5px;
    font-family:'Courier New',monospace; transition:all .15s ease;
  }
  #controls button:hover{background:rgba(120,60,200,0.35); border-color:#c9a6ff;}
</style>
</head>
<body>
<div id="hud">
  <h1>Equilibrio Cósmico</h1>
  <div class="row"><span><span class="dot" style="background:#7CFF9E;"></span>Vida</span><span id="cLife">0</span></div>
  <div class="row"><span><span class="dot" style="background:#7ad9ff;"></span>Nómada</span><span id="cNomad">0</span></div>
  <div class="row"><span><span class="dot" style="background:#ffe27a;"></span>Social</span><span id="cSocial">0</span></div>
  <div class="row"><span><span class="dot" style="background:#ff4d6d;"></span>Voracidad</span><span id="cVor">0</span></div>
  <div class="sub">Sistema Oscilatorio Balanceado:<br>Inercia de caza, saciedad y muerte por inanición.</div>
</div>
<div id="controls">
  <button id="btnPause">Pausar</button>
  <button id="btnReset">Reiniciar</button>
  <button id="btnSpeed">Vel. x1</button>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.4/p5.min.js"></script>
<script>
/* ============================================================
   VORACIDAD & PROPAGACIÓN — Balance Re-Engineered
   ============================================================ */

const CONFIG = {
  // Ajustes de Agilidad y Giro (Inercia)
  life:   { count: 320, cap: 450, friction: 0.96, maxSpeed: 0.25, maxForce: 0.01, r: 2.5 },
  nomad:  { count: 90,  cap: 220, friction: 0.84, maxSpeed: 4.2,  maxForce: 0.50, r: 3.2 },
  social: { count: 60,  cap: 180, friction: 0.89, maxSpeed: 2.3,  maxForce: 0.35, r: 3.6 },
  
  // Voracidad balanceada: Más rápida en recta pero con giro torpe (inercia alta)
  vor:    { count: 12,  cap: 28,  friction: 0.91, maxSpeed: 3.6,  maxForce: 0.22, r: 5.5 },

  DETECTION: 140,
  INFLUENCE: 80,
  CONTACT: 8,

  LIFE_TO_PROP_ATTR: 0.8,    LIFE_TO_PROP_R: 85,
  SOCIAL_COHESION_ATTR: 0.65,SOCIAL_COHESION_R: 65,
  SOCIAL_SEPARATION_R: 18,   SOCIAL_SEPARATION_W: 1.1,
  VOR_TO_PROP_ATTR: 0.9,     VOR_TO_PROP_R: 130,
  PROP_FLEE_VOR: 1.1,        PROP_FLEE_VOR_R: 120,

  NOMAD_SEPARATION_R: 32,
  NOMAD_SEPARATION_W: 0.85,
};

let grid;
let lifeArr = [], propArr = [], vorArr = [];
let paused = false;
let timeScale = 1;
let W, H;
let starfield = [];
let lifeSpawnTimer = 0;

function limitVec(v, max){ if (v.magSq() > max*max) v.setMag(max); return v; }

class Grid {
  constructor(cellSize){ this.cellSize = cellSize; this.map = new Map(); }
  key(cx,cy){ return cx + ',' + cy; }
  clear(){ this.map.clear(); }
  insert(p){
    const cx = Math.floor(p.pos.x / this.cellSize);
    const cy = Math.floor(p.pos.y / this.cellSize);
    const k = this.key(cx,cy);
    if (!this.map.has(k)) this.map.set(k, []);
    this.map.get(k).push(p);
  }
  query(x, y, r){
    const res = [];
    const minCx = Math.floor((x-r)/this.cellSize), maxCx = Math.floor((x+r)/this.cellSize);
    const minCy = Math.floor((y-r)/this.cellSize), maxCy = Math.floor((y+r)/this.cellSize);
    for (let cx=minCx; cx<=maxCx; cx++){
      for (let cy=minCy; cy<=maxCy; cy++){
        const arr = this.map.get(this.key(cx,cy));
        if (arr) for (const p of arr) res.push(p);
      }
    }
    return res;
  }
}

// ============================================================
// VIDA
// ============================================================
class Life {
  constructor(x,y){
    this.pos = createVector(x,y);
    this.vel = p5.Vector.random2D().mult(0.05);
    this.acc = createVector(0,0);
    this.kind = 'life';
    this.phase = random(TWO_PI);
    this.dead = false;
    this.wanderAngle = random(TWO_PI);
  }
  update(){
    this.wanderAngle += random(-0.2, 0.2);
    const wander = p5.Vector.fromAngle(this.wanderAngle).mult(0.005);
    this.acc.add(wander);

    this.vel.add(this.acc);
    this.vel.mult(CONFIG.life.friction);
    limitVec(this.vel, CONFIG.life.maxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0);
    bounce(this, CONFIG.life.r);
  }
  draw(){
    const pulse = 0.55 + 0.45*sin(frameCount*0.03 + this.phase);
    const s = CONFIG.life.r * (1 + pulse*0.4);
    noStroke();
    blendMode(ADD);
    fill(124, 255, 158, 55*pulse);
    circle(this.pos.x, this.pos.y, s*4.0);
    fill(180, 255, 200, 210);
    circle(this.pos.x, this.pos.y, s*1.5);
    blendMode(BLEND);
  }
}

// ============================================================
// PROPAGACIÓN
// ============================================================
class Propagation {
  constructor(x,y,type){
    this.pos = createVector(x,y);
    this.vel = p5.Vector.random2D().mult(0.5);
    this.acc = createVector(0,0);
    this.type = type;
    this.kind = type;
    this.cfg = CONFIG[type];
    this.energy = random(40, 60);
    this.sizeBoost = 0;
    this.dead = false;
    this.fear = 0;
    this.panicTimer = 0; // Estado de evasión rápida al ver caer a un compañero
  }
  update(neighborsLife, neighborsSame, neighborsVor, neighborsProp){
    const cfg = this.cfg;

    let nearestVorDist = Infinity;
    for (const v of neighborsVor){
      const d = p5.Vector.dist(this.pos, v.pos);
      if (d < nearestVorDist) nearestVorDist = d;
    }
    this.fear = constrain(map(nearestVorDist, CONFIG.PROP_FLEE_VOR_R, 0, 0, 1), 0, 1);
    if (this.panicTimer > 0) this.panicTimer--;

    // 1. Vida (Búsqueda de comida)
    let seekLife = createVector(0,0);
    let nearestLife = null, nearestLifeD = Infinity;
    for (const l of neighborsLife){
      const d = p5.Vector.dist(this.pos, l.pos);
      if (d < CONFIG.LIFE_TO_PROP_R && d < nearestLifeD){ nearestLifeD = d; nearestLife = l; }
    }
    if (nearestLife){
      const desired = p5.Vector.sub(nearestLife.pos, this.pos);
      desired.setMag(cfg.maxSpeed);
      const steer = p5.Vector.sub(desired, this.vel);
      limitVec(steer, cfg.maxForce);
      seekLife.add(steer.mult(CONFIG.LIFE_TO_PROP_ATTR));
    }

    // 2. Huida / Esquiva de Voracidad (Aumentada agilidad de evasión)
    let flee = createVector(0,0);
    for (const v of neighborsVor){
      const d = p5.Vector.dist(this.pos, v.pos);
      if (d < CONFIG.PROP_FLEE_VOR_R && d > 0){
        let away = p5.Vector.sub(this.pos, v.pos);
        // Si la voracidad viene de frente, la propagación intenta esquivar en 90 grados
        const headingAngle = this.vel.angleBetween(away);
        if (abs(headingAngle) < HALF_PI) {
          away.rotate(this.pos.x % 2 === 0 ? HALF_PI * 0.5 : -HALF_PI * 0.5);
        }
        away.setMag(cfg.maxSpeed * 1.2);
        const steer = p5.Vector.sub(away, this.vel);
        limitVec(steer, cfg.maxForce * 1.5);
        const w = CONFIG.PROP_FLEE_VOR * map(d, 0, CONFIG.PROP_FLEE_VOR_R, 2.5, 0.3);
        flee.add(steer.mult(w));
      }
    }

    let social = createVector(0,0);
    let separation = createVector(0,0);

    if (this.type === 'social'){
      let center = createVector(0,0); 
      let pushForce = createVector(0,0);
      let count = 0, repCount = 0;

      for (const o of neighborsSame){
        if (o === this) continue;
        const d = p5.Vector.dist(this.pos, o.pos);
        if (d < CONFIG.SOCIAL_COHESION_R){ center.add(o.pos); count++; }
        if (d < CONFIG.SOCIAL_SEPARATION_R && d > 0){
          const away = p5.Vector.sub(this.pos, o.pos);
          away.div(d);
          pushForce.add(away);
          repCount++;
        }
      }

      // Si están en pánico por depredación cercana, rompen la cohesión temporalmente para dispersarse
      const cohesionMult = this.panicTimer > 0 ? 0.2 : 1.0;
      if (count > 0){
        center.div(count);
        const desired = p5.Vector.sub(center, this.pos);
        desired.setMag(cfg.maxSpeed);
        const steer = p5.Vector.sub(desired, this.vel);
        limitVec(steer, cfg.maxForce);
        social.add(steer.mult(CONFIG.SOCIAL_COHESION_ATTR * cohesionMult));
      }

      if (repCount > 0){
        pushForce.div(repCount);
        pushForce.setMag(cfg.maxSpeed);
        const steer = p5.Vector.sub(pushForce, this.vel);
        limitVec(steer, cfg.maxForce);
        separation.add(steer.mult(CONFIG.SOCIAL_SEPARATION_W));
      }

    } else {
      // Nómadas
      let push = createVector(0,0); let count=0;
      for (const o of neighborsProp){
        if (o === this) continue;
        const d = p5.Vector.dist(this.pos,o.pos);
        if (d < CONFIG.NOMAD_SEPARATION_R && d>0){
          const away = p5.Vector.sub(this.pos,o.pos);
          away.div(d*d);
          push.add(away);
          count++;
        }
      }
      if (count>0){
        push.div(count);
        push.setMag(cfg.maxSpeed);
        const steer = p5.Vector.sub(push, this.vel);
        limitVec(steer, cfg.maxForce);
        separation.add(steer.mult(CONFIG.NOMAD_SEPARATION_W));
      }
    }

    const fearSpeedMul = 1 + this.fear * 0.5 + (this.panicTimer > 0 ? 0.6 : 0);

    this.acc.add(seekLife);
    this.acc.add(flee.mult(1.3));
    this.acc.add(social);
    this.acc.add(separation);
    this.acc.add(p5.Vector.random2D().mult(this.type === 'nomad' ? 0.04 : 0.015));

    this.vel.add(this.acc);
    this.vel.mult(cfg.friction);
    limitVec(this.vel, cfg.maxSpeed * fearSpeedMul);
    this.pos.add(this.vel);
    this.acc.mult(0);
    bounce(this, cfg.r);

    // Metabolismo
    const moveCost = this.vel.mag() * 0.025;
    const metabolism = this.type === 'nomad' ? 0.025 : 0.015;
    this.energy -= moveCost + metabolism;
    if (this.sizeBoost > 0) this.sizeBoost *= 0.91;

    if (this.energy <= 0) this.dead = true;
  }

  tryEatLife(neighborsLife){
    for (const l of neighborsLife){
      if (l.dead) continue;
      const d = p5.Vector.dist(this.pos, l.pos);
      if (d < CONFIG.CONTACT){
        l.dead = true;
        this.energy = min(100, this.energy + 38);
        this.sizeBoost = 1.5;
        break;
      }
    }
  }

  triggerPanic(){ this.panicTimer = 90; }

  tryReproduce(currentCount){
    const cfg = this.cfg;
    const threshold = this.type === 'nomad' ? 62 : 72;
    if (this.energy < threshold) return null;
    if (currentCount >= cfg.cap) return null;
    const rate = this.type === 'nomad' ? 0.006 : 0.0025;
    if (random() < rate){
      this.energy *= 0.45;
      const child = new Propagation(
        this.pos.x + random(-6,6), this.pos.y + random(-6,6), this.type
      );
      child.energy = 30;
      return child;
    }
    return null;
  }

  draw(){
    const baseCol = this.type === 'nomad' ? [122,217,255] : [255,226,122];
    const threshold = this.type === 'nomad' ? 62 : 72;
    const readyGlow = constrain(map(this.energy, threshold*0.7, threshold, 0, 1), 0, 1);
    const s = this.cfg.r * (1 + this.sizeBoost*0.45);

    blendMode(ADD);
    if (readyGlow > 0){
      noStroke();
      fill(baseCol[0], baseCol[1], baseCol[2], 70*readyGlow);
      circle(this.pos.x, this.pos.y, s*6.5*(0.5+readyGlow));
    }
    if (this.fear > 0.1 || this.panicTimer > 0){
      noStroke();
      fill(255,80,100, 60*(this.fear || 0.8));
      circle(this.pos.x, this.pos.y, s*5.5);
    }
    noStroke();
    fill(baseCol[0], baseCol[1], baseCol[2], 230);
    circle(this.pos.x, this.pos.y, s*2.0);
    blendMode(BLEND);
  }
}

// ============================================================
// VORACIDAD
// ============================================================
class Voracity {
  constructor(x,y){
    this.pos = createVector(x,y);
    this.vel = p5.Vector.random2D().mult(0.5);
    this.acc = createVector(0,0);
    this.kind = 'vor';
    this.energy = 70;
    this.eatBoost = 0;
    this.satiatedTimer = 0; // Período de digestión (letargo)
    this.trail = [];
    this.dead = false;
  }
  update(neighborsProp, totalPropCount){
    if (this.satiatedTimer > 0) this.satiatedTimer--;

    // Factor de hambre moderado (No escala infinitamente)
    const hungerFactor = constrain(map(totalPropCount, 10, 180, 0.6, 1.15), 0.6, 1.15);
    const isSatiated = this.satiatedTimer > 0;
    
    // Si está saciada, reduce drásticamente su velocidad
    const effMaxSpeed = isSatiated ? 1.0 : (CONFIG.vor.maxSpeed * hungerFactor);
    const effDetection = isSatiated ? 60 : (CONFIG.DETECTION * hungerFactor);

    let nearest = null, nearestD = Infinity;
    if (!isSatiated) {
      for (const p of neighborsProp){
        const d = p5.Vector.dist(this.pos, p.pos);
        if (d < effDetection && d < nearestD){ nearestD = d; nearest = p; }
      }
    }

    if (nearest){
      const desired = p5.Vector.sub(nearest.pos, this.pos);
      desired.setMag(effMaxSpeed);
      const steer = p5.Vector.sub(desired, this.vel);
      // Inercia: maxForce bajo para dar giros lentos
      limitVec(steer, CONFIG.vor.maxForce);
      this.acc.add(steer.mult(CONFIG.VOR_TO_PROP_ATTR));
      
      if (frameCount % 2 === 0){
        this.trail.push(this.pos.copy());
        if (this.trail.length > 14) this.trail.shift();
      }
    } else {
      this.acc.add(p5.Vector.random2D().mult(0.03));
      if (this.trail.length > 0 && frameCount % 3 === 0) this.trail.shift();
    }

    this.vel.add(this.acc);
    this.vel.mult(CONFIG.vor.friction);
    limitVec(this.vel, effMaxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0);
    bounce(this, CONFIG.vor.r);

    // Muerte por inanición: si se queda sin comida, muere
    const baseMetabolism = 0.055;
    this.energy -= this.vel.mag()*0.02 + baseMetabolism;
    if (this.eatBoost > 0) this.eatBoost *= 0.92;

    if (this.energy <= 0) this.dead = true;
    this._isSatiated = isSatiated;
  }

  tryEat(neighborsProp){
    if (this.satiatedTimer > 0) return false;
    for (const p of neighborsProp){
      if (p.dead) continue;
      const d = p5.Vector.dist(this.pos, p.pos);
      if (d < CONFIG.CONTACT){
        p.dead = true;
        this.energy = min(100, this.energy + 40);
        this.eatBoost = 1.4;
        this.satiatedTimer = 110; // Digestión: 110 frames sin cazar intensamente
        
        // Asustar a las partículas cercanas (Alarma de enjambre)
        for (const other of neighborsProp){
          if (p5.Vector.dist(this.pos, other.pos) < 90 && other.triggerPanic){
            other.triggerPanic();
          }
        }
        return true;
      }
    }
    return false;
  }

  tryReproduce(currentCount){
    if (currentCount >= CONFIG.vor.cap) return null;
    if (this.energy < 92) return null;
    if (random() < 0.001){
      this.energy *= 0.48;
      const child = new Voracity(this.pos.x+random(-10,10), this.pos.y+random(-10,10));
      child.energy = 45;
      return child;
    }
    return null;
  }

  draw(){
    const s = CONFIG.vor.r * (1 + this.eatBoost*0.4);
    const col = this._isSatiated ? [140,70,180] : (this.eatBoost > 0.3 ? [255,90,120] : [210,40,70]);

    blendMode(ADD);
    noFill();
    for (let i=0; i<this.trail.length-1; i++){
      const a = map(i, 0, this.trail.length, 0, 80);
      stroke(col[0], col[1], col[2], a);
      strokeWeight(1.5);
      line(this.trail[i].x, this.trail[i].y, this.trail[i+1].x, this.trail[i+1].y);
    }
    noStroke();
    fill(col[0], col[1], col[2], this._isSatiated ? 25 : 50);
    circle(this.pos.x, this.pos.y, s*6.0);
    fill(255, 160, 180, 220);
    circle(this.pos.x, this.pos.y, s*2.1);
    blendMode(BLEND);
  }
}

function bounce(p, r){
  const margin = r*2;
  if (p.pos.x < margin){ p.pos.x = margin; p.vel.x *= -0.6; }
  if (p.pos.x > W-margin){ p.pos.x = W-margin; p.vel.x *= -0.6; }
  if (p.pos.y < margin){ p.pos.y = margin; p.vel.y *= -0.6; }
  if (p.pos.y > H-margin){ p.pos.y = H-margin; p.vel.y *= -0.6; }
}

// ============================================================
// SETUP & INICIALIZACIÓN
// ============================================================
function setup(){
  W = windowWidth; H = windowHeight;
  createCanvas(W,H);
  pixelDensity(1);
  initStarfield();
  initPopulations();

  document.getElementById('btnPause').onclick = () => {
    paused = !paused;
    document.getElementById('btnPause').textContent = paused ? 'Reanudar' : 'Pausar';
  };
  document.getElementById('btnReset').onclick = () => initPopulations();
  document.getElementById('btnSpeed').onclick = () => {
    timeScale = timeScale === 1 ? 2 : (timeScale === 2 ? 0.4 : 1);
    document.getElementById('btnSpeed').textContent = 'Vel. x' + timeScale;
  };
}

function windowResized(){
  W = windowWidth; H = windowHeight;
  resizeCanvas(W,H);
  initStarfield();
}

function initStarfield(){
  starfield = [];
  const n = floor((W*H)/8500);
  for (let i=0;i<n;i++){
    starfield.push({x:random(W), y:random(H), r:random(0.5,1.8), phase:random(TWO_PI), speed:random(0.01,0.03)});
  }
}

function initPopulations(){
  lifeArr = []; propArr = []; vorArr = [];
  grid = new Grid(CONFIG.DETECTION);

  for (let i=0; i<CONFIG.life.count; i++){
    lifeArr.push(new Life(random(W), random(H)));
  }

  const nomadColonies = 5;
  const perNomad = Math.floor(CONFIG.nomad.count / nomadColonies);
  for (let c=0; c<nomadColonies; c++){
    const cx = random(W*0.1, W*0.9), cy = random(H*0.1, H*0.9);
    for (let i=0; i<perNomad; i++){
      propArr.push(new Propagation(cx+random(-35,35), cy+random(-35,35), 'nomad'));
    }
  }

  const socialColonies = 3;
  const perSocial = Math.floor(CONFIG.social.count / socialColonies);
  for (let c=0; c<socialColonies; c++){
    const cx = random(W*0.15, W*0.85), cy = random(H*0.15, H*0.85);
    for (let i=0; i<perSocial; i++){
      propArr.push(new Propagation(cx+random(-45,45), cy+random(-45,45), 'social'));
    }
  }

  for (let i=0; i<CONFIG.vor.count; i++){
    let placed=false, tries=0, x, y;
    while(!placed && tries<50){
      x = random(W); y = random(H);
      let ok = true;
      for (const v of vorArr){ if (dist(x,y,v.pos.x,v.pos.y) < 180){ ok=false; break; } }
      if (ok) placed = true;
      tries++;
    }
    vorArr.push(new Voracity(x,y));
  }

  lifeSpawnTimer = 0;
}

// ============================================================
// SIMULACIÓN Y LOOP
// ============================================================
function draw(){
  drawBackground();

  if (!paused){
    for (let s=0; s<Math.max(1,Math.round(timeScale)); s++){
      if (timeScale < 1 && frameCount % 2 !== 0) break;
      stepSimulation();
    }
  }

  renderAll();
  updateHUD();
}

function stepSimulation(){
  grid.clear();
  for (const l of lifeArr) grid.insert(l);
  for (const p of propArr) grid.insert(p);
  for (const v of vorArr) grid.insert(v);

  // Regeneración constante pero gradual de Vida
  lifeSpawnTimer++;
  if (lifeSpawnTimer > 8 && lifeArr.length < CONFIG.life.cap){
    lifeSpawnTimer = 0;
    lifeArr.push(new Life(random(W), random(H)));
  }

  for (const l of lifeArr) l.update();

  const newProp = [];
  for (const p of propArr){
    const nLife = grid.query(p.pos.x,p.pos.y,CONFIG.LIFE_TO_PROP_R).filter(o=>o.kind==='life' && !o.dead);
    const nVor = grid.query(p.pos.x,p.pos.y,CONFIG.PROP_FLEE_VOR_R).filter(o=>o.kind==='vor' && !o.dead);
    const nSame = p.type==='social' ? grid.query(p.pos.x,p.pos.y,CONFIG.SOCIAL_COHESION_R).filter(o=>o.kind==='social') : [];
    const nProp = p.type==='nomad' ? grid.query(p.pos.x,p.pos.y,CONFIG.NOMAD_SEPARATION_R).filter(o=>o.kind==='nomad'||o.kind==='social') : [];

    p.update(nLife, nSame, nVor, nProp);
    p.tryEatLife(nLife);

    const countOfType = propArr.filter(x=>x.type===p.type).length + newProp.filter(x=>x.type===p.type).length;
    const child = p.tryReproduce(countOfType);
    if (child) newProp.push(child);
  }
  propArr = propArr.filter(p=>!p.dead).concat(newProp);
  lifeArr = lifeArr.filter(l=>!l.dead);

  const totalPropCount = propArr.length;
  const newVor = [];
  for (const v of vorArr){
    const nProp = grid.query(v.pos.x,v.pos.y,CONFIG.DETECTION*1.3).filter(o=>o.kind==='nomad'||o.kind==='social');
    v.update(nProp, totalPropCount);
    v.tryEat(nProp);
    const child = v.tryReproduce(vorArr.length + newVor.length);
    if (child) newVor.push(child);
  }
  // Filtrar Voracidad muerta por inanición
  vorArr = vorArr.filter(v=>!v.dead).concat(newVor);
  propArr = propArr.filter(p=>!p.dead);

  // Mecanismo de rescate: si la Voracidad se extingue por completo, reaparece 1 individuo débil
  if (vorArr.length === 0 && frameCount % 180 === 0){
    const v = new Voracity(random(W), random(H));
    v.energy = 40;
    vorArr.push(v);
  }
}

function renderAll(){
  for (const l of lifeArr) l.draw();
  for (const p of propArr) p.draw();
  for (const v of vorArr) v.draw();
}

function drawBackground(){
  background(6,4,14);

  blendMode(ADD);
  noStroke();
  fill(90,40,140,8);
  circle(W*0.2,H*0.25, W*0.5);
  fill(30,80,140,7);
  circle(W*0.8,H*0.7, W*0.55);
  fill(140,50,90,6);
  circle(W*0.5,H*0.85, W*0.4);
  blendMode(BLEND);

  noStroke();
  for (const s of starfield){
    const tw = 0.5 + 0.5*sin(frameCount*s.speed + s.phase);
    fill(255,255,255, 40+tw*130);
    circle(s.x, s.y, s.r*(0.7+tw*0.6));
  }
}

function updateHUD(){
  if (frameCount % 6 !== 0) return;
  document.getElementById('cLife').textContent = lifeArr.length;
  document.getElementById('cNomad').textContent = propArr.filter(p=>p.type==='nomad').length;
  document.getElementById('cSocial').textContent = propArr.filter(p=>p.type==='social').length;
  document.getElementById('cVor').textContent = vorArr.length;
}
</script>
</body>
</html>
```
### Autoevaluación:
(aun no aplica es solo que pegué la que hice en el anterior para tener el formato)
| Criterio | Cumplo | No cumplo | Evidencia |
|----------|:-------:|:---------:|-----------|
| Encargo completo: interpreto los cinco momentos dentro de un mismo sistema visual. | ◼ | ☐ | [Evidencia](#1)|
| Simulación con intención: utilizo al menos tres conceptos de la unidad para comunicar las ideas del encargo. | ◼ | ☐ | [Evidencia](#1) |
| Interacción significativa: la interacción modifica el comportamiento o las probabilidades del sistema, que también funciona sin intervención. | ◼ | ☐ |[Evidencia](#1) |
| Prototipo funcional: la experiencia puede ejecutarse y recorrerse completa sin errores que impidan comprenderla. | ◼ | ☐ |[Evidencia](#2) |
| Proceso documentado: la bitácora evidencia avances, decisiones, dificultades, soluciones, uso de IA y enlace al prototipo. | ◼ | ☐ |[Evidencia](#3) |
