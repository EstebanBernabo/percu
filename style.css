
/* ================= AUDIO ================ */
let audioCtx = null;
function ensureAudio(){
  if(!audioCtx) audioCtx = new (window.AudioContext || window.webkitAudioContext)();
}
const plumaCumbia = {
  name: "Pluma Cumbia",
  fingers: 4,          // 4 = binario, 3 = ternario
  sequence: [
    { R: "1111", L: "1011" },
    { R: "1110", L: "1111" },
    { R: "1000", L: "0010" },
    { R: "0000", L: "1100" },
    { R: "1111", L: "1011" },
    { R: "1110", L: "1111" },
    { R: "1011", L: "0110" },
    { R: "1001", L: "0010" }
  ]
};
const plumaRumba = {
  fingers: 4,          // 4 = binario, 3 = ternario
  name: "Pluma Rumba",
  sequence: [
    { R: "0111", L: "0101" },
    { R: "1010", L: "1101" },
    { R: "0110", L: "1010" },
    { R: "1001", L: "1000" }
    ]
};


const plumaZentangle = {
  fingers: 4,
  name: "Pluma Zentangle",
  sequence: [ 
    { R: "1001", L: "0010" },
    { R: "0100", L: "1010" },
    { R: "1001", L: "0010" },
    { R: "0100", L: "1010" }]
};

let activePluma = null;

const beatDirections = {
  2: [0, 180],                 // abajo, arriba
  3: [0, -90, 180],            // abajo, izquierda, arriba
  4: [0, -90, 90, 180]         // abajo, izquierda, derecha, arriba
};

function getBeatCount(){
  if(cycleLength === 4) return 2;
  if(cycleLength === 5) return 3;
  if(cycleLength === 6) return 4;
}


// Preview sound: grave y suave
function playPreviewClick(time = 0){
  ensureAudio();
  const osc = audioCtx.createOscillator();
  const gain = audioCtx.createGain();
  osc.type = 'sine';
  osc.frequency.value = 300;
  gain.gain.setValueAtTime(0.12, audioCtx.currentTime + time);
  gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + time + 0.08);
  osc.connect(gain); gain.connect(audioCtx.destination);
  osc.start(audioCtx.currentTime + time);
  osc.stop(audioCtx.currentTime + time + 0.09);
}


// Active sound: claro y más marcado
function playActiveClick(time = 0){
  ensureAudio();
  const osc = audioCtx.createOscillator();
  const gain = audioCtx.createGain();
  osc.type = 'sine';
  osc.frequency.value = 1000;
  gain.gain.setValueAtTime(0.28, audioCtx.currentTime + time);
  gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + time + 0.06);
  osc.connect(gain); gain.connect(audioCtx.destination);
  osc.start(audioCtx.currentTime + time);
  osc.stop(audioCtx.currentTime + time + 0.07);
}

/* =============== STATE ================ */
let numFingers = 4;        // 4 (Binario) o 3 (Ternario)
let cycleLength = 4;       // 4 o 6 steps
let timer = null;
let step = 0;              
let comboActual = null;
let playMode = "random"; // "random" | "pluma"
let plumaStep = 0;
let plumaPhase = "preview"; // "preview" | "active"
let plumaPulse = 0; // pulso real (cada beep)



/* UI elements */
const handsGrid = document.getElementById('handsGrid');
const handUL = document.getElementById('handUL');
const handUR = document.getElementById('handUR');
const handLL = document.getElementById('handLL');
const handLR = document.getElementById('handLR');
const comboLabel = document.getElementById('combo');
const pulse = document.getElementById('pulse');
const historyList = document.getElementById('historyList');
const footerText = document.getElementById('footerText');

/* Buttons */
const btnBin = document.getElementById('btnBin');
const btnTer = document.getElementById('btnTer');
const btnCycle4 = document.getElementById('btnCycle4');
const btnCycle3 = document.getElementById('btnCycle3');
const btnCycle6 = document.getElementById('btnCycle6');

/* =============== HELPERS ================ */
function stop(){
  if(timer) { clearInterval(timer); timer = null; }
  step = 0; 
}

// Alternar entre Binario (4) y Ternario (3)
function setModeTime(mode){
  stop(); 
  numFingers = (mode === 'binario') ? 4 : 3;

  btnBin.classList.toggle('modeActive', mode === 'binario');
  btnTer.classList.toggle('modeActive', mode === 'ternario');

  historyList.innerHTML = '';
  updateUI(true);
}

// FUNCIÓN CLAVE: Muestra/Oculta manos superiores
function updateHandVisibility(){
  // Resetear todo
  handUL.style.display = 'none';
  handUR.style.display = 'none';

  // Ciclo 6 → 4 manos
  if(cycleLength === 6){
    handUL.style.display = 'flex';
    handUR.style.display = 'flex';
  }

  // Ciclo 5 → 3 manos (UL + LL + LR)
  if(cycleLength === 5){
    handUL.style.display = 'flex';
  }

  // Ciclo 4 → 2 manos (solo LL + LR)
  handsGrid.classList.toggle('hands-2-set', cycleLength === 4);
}



// Alternar entre Ciclo 4 (2P+2A) y Ciclo 6 (2P+4A)
function setCycleLength(length){
  stop(); 
  cycleLength = length;

  btnCycle4.classList.toggle('modeActive', length === 4);
  btnCycle6.classList.toggle('modeActive', length === 6);

  // 1. Ajustar la visibilidad de las manos
  updateHandVisibility();

  // 2. Actualizar el texto del footer
  const activeSteps = cycleLength - 2;
  footerText.textContent = `Ciclo: ${cycleLength} pulsos — 2 previsualización (violeta) + ${activeSteps} activación (verde).`;
  
  // 3. Resetear la UI con el número correcto de manos
  updateUI(true);
}

/* genera un string con numFingers bits '0'/'1' */
function randBits(){
  let s='';
  for(let i=0;i<numFingers;i++) s += (Math.random() < 0.5) ? '1' : '0';
  return s;
}

/* Genera 2 o 4 sets de bits según el cycleLength */
function randCombo(){
  const combo = {
    ll: randBits(),
    lr: randBits(),
    ul: '',
    ur: ''
  };

  // Ciclo 6 → 4 manos
  if (cycleLength === 6) {
    combo.ul = randBits();
    combo.ur = randBits();
  }

  // Ciclo 5 → 3 manos (UL + LL + LR)
  if (cycleLength === 5) {
    combo.ul = randBits();
  }

  return combo;
}


/* dibuja una mano (bits como string '1010') */
function drawHand(container, bits, activeStage=false){
  container.innerHTML = '';
  // Solo dibuja si 'bits' no está vacío
  if(bits.length > 0) {
    for(const c of bits){
      const d = document.createElement('div');
      d.className = 'finger ' + (c === '1' ? 'on' : 'off') + ' ' + (activeStage ? 'activeColor' : 'previewColor');
      container.appendChild(d);
    }
  }
}

/* Dibuja las manos visibles */
function drawHands(combo, activeStage=false){
  // Manos inferiores (siempre)
  drawHand(handLL, combo.ll, activeStage);
  drawHand(handLR, combo.lr, activeStage);

  // Mano superior izquierda (ciclo 5 y 6)
  if(cycleLength === 5 || cycleLength === 6){
    drawHand(handUL, combo.ul, activeStage);
  } else {
    handUL.innerHTML = '';
  }

  // Mano superior derecha (solo ciclo 6)
  if(cycleLength === 6){
    drawHand(handUR, combo.ur, activeStage);
  } else {
    handUR.innerHTML = '';
  }
}


/* actualiza etiqueta combo */
function updateComboLabel(combo){
  let text = `${combo.ll} ${combo.lr}`; // Muestra LL y LR
  if (cycleLength === 6) {
    // Si es ciclo 6, añade UL y UR al principio
    text = `${combo.ul} ${combo.ur}   ${text}`;
  }
  comboLabel.textContent = text.trim();
}

/* pulso visual */
function flashPulse(){
  pulse.classList.add('flash');
  setTimeout(()=> pulse.classList.remove('flash'), 120);
}

/* Actualiza la UI de las manos y combo (usado en inicialización y cambio de modo/ciclo) */
function updateUI(reset=false){
    let combo;
    if(reset || !comboActual){
        // Genera el placeholder 
        const placeholderBits = '0'.repeat(numFingers);
        combo = { 
            ll: placeholderBits, 
            lr: placeholderBits,
            ul: (cycleLength === 6) ? placeholderBits : '',
            ur: (cycleLength === 6) ? placeholderBits : ''
        };
        comboActual = combo; 
    } else {
        combo = comboActual;
    }

    drawHands(combo, false);
    updateComboLabel(combo);
}

/* ================= HISTORIAL ================= */
function pushToHistory(combo){
  const block = document.createElement('div');
  block.className = 'histBlock';
  const row = document.createElement('div');
  row.className = 'miniRow';
  
  let combosArray = [combo.ll, combo.lr]; // Siempre registra LL y LR

  if (cycleLength === 6) {
    // Si es ciclo 6, registra las 4 manos
    combosArray = [combo.ul, combo.ur, combo.ll, combo.lr];
  }

  for(const bits of combosArray){
    const miniHand = document.createElement('div');
    miniHand.className = 'miniHand';
    for(const c of bits){
      const f = document.createElement('div');
      f.className = 'miniFinger';
      f.style.background = (c === '1') ? 'var(--green)' : 'var(--finger-off)';
      f.style.height = (c === '1') ? '30px' : '14px';
      f.style.opacity = (c === '1') ? '1' : '0.4';
      miniHand.appendChild(f);
    }
    row.appendChild(miniHand);
  }

  block.appendChild(row);
  historyList.prepend(block);
  while(historyList.children.length > 10) historyList.removeChild(historyList.lastChild);
}

/* ================== CICLO ================== */
function start() {
  ensureAudio();
  stop();

  if (playMode === "pluma" && activePluma) {
    startPluma();
  } else {
    startRandom();
  }
}
function startRandom() {
  const bpmVal = parseFloat(document.getElementById('bpm').value) || 80;
  const interval = 60000 / bpmVal;

  step = 0;
  comboActual = randCombo();

  runTick();
  timer = setInterval(runTick, interval);
}
function startPluma() {
  const bpmVal = parseFloat(document.getElementById('bpm').value) || 80;
  const interval = 60000 / bpmVal;

    plumaPulse = 0;
    plumaPhase = "preview";

  runPlumaTick();
  timer = setInterval(runPlumaTick, interval);
}

function runPlumaTick() {
  flashPulse();

  const rowIndex = Math.floor(plumaPulse / 2);
  const isRightHand = plumaPulse % 2 === 0;

  // PREVIEW (2 pulsos = 1 fila completa)
  if (plumaPhase === "preview") {
    highlightPlumaRow(rowIndex, false);
    playPreviewClick();

    plumaPulse++;

    if (plumaPulse >= 2) { // 2 filas = 2 pulsos de preview por mano
      plumaPhase = "active";
      plumaPulse = 0;
    }
    return;
  }

  // ACTIVACIÓN
  highlightPlumaRow(rowIndex, true);
  playActiveClick();

  plumaPulse++;

  // fin de la pluma
  if (rowIndex >= activePluma.sequence.length) {
    stop();
  }
}



/* El tick actual (llamado cada compás) */
function runTick(){
  flashPulse();

  // Primeros 2 steps: PREVIEW (0 y 1)
  if(step < 2){
    drawHands(comboActual, false); // color preview (violeta)
    updateComboLabel(comboActual);
    playPreviewClick();
    
    document.getElementById('beatLine').style.opacity = 0;

  } 
  // Siguientes steps: ACTIVE 
  else {
    // Si step === 2, registrar en historial al comenzar la activación
    if(step === 2){
      pushToHistory(comboActual);
    }
    drawHands(comboActual, true); // color active (verde)
    updateComboLabel(comboActual);
    playActiveClick();
    updateBeatIndicator();
  }

  // Avanzar el step (usando cycleLength: 4 o 6)
  step = (step + 1) % cycleLength;

  // Si volvemos a step 0, generamos el nuevo combo para el siguiente ciclo de preview
if(step === 0){
  comboActual = randCombo();
}
}

/* ============== Event bindings ============== */
document.getElementById('btnStart').addEventListener('click', start);
document.getElementById('btnStop').addEventListener('click', stop);

// Modo de tiempo (Binario/Ternario)
btnBin.addEventListener('click', ()=> setModeTime('binario'));
btnTer.addEventListener('click', ()=> setModeTime('ternario'));

// Largo del ciclo (4/6 compases)
btnCycle4.addEventListener('click', ()=> setCycleLength(4));
btnCycle3.addEventListener('click', ()=> setCycleLength(5));
btnCycle6.addEventListener('click', ()=> setCycleLength(6));

/* Inicialización: Estado por defecto */
setCycleLength(4); 
setModeTime('binario'); 

/* ============== Atajo de Teclado (Barra Espaciadora) ============== */
document.addEventListener('keydown', function(event) {
  // 32 es el keycode para la barra espaciadora
  if (event.code === 'Space') {
    event.preventDefault(); // Evita que la barra espaciadora haga scroll en la página
    
    // Si el metrónomo está corriendo, lo detenemos (pausa)
    if (timer !== null) {
      document.getElementById('btnStop').click(); // Simula el clic en Detener
    } else {
      // Si está detenido, lo iniciamos
      document.getElementById('btnStart').click(); // Simula el clic en Iniciar
    }
  }
});

/* ================== PLUMA VIEW ================== */

const plumaContainer = document.getElementById('plumaView');

/**
 * Renderiza una pluma completa (N manos, N*dedos)
 * pluma = {
 *   fingers: 4,
 *   hands: [
 *     "1111",
 *     "1011",
 *     "1110",
 *     ...
 *   ]
 * }
 */
function renderPluma(pluma) {
  const container = document.getElementById('plumaView');
  container.innerHTML = '';

    pluma.sequence.forEach((pulso, i) => {
    const isPreview = i < 0;
    const row = document.createElement('div');
    row.dataset.index = i;
    row.classList.add("pluma-row");
    row.style.display = 'flex';
    row.style.gap = '36px';
    row.style.marginBottom = '12px';
    row.style.justifyContent = 'center';
    row.style.alignItems = 'flex-end';

    // mano derecha
    const handR = document.createElement('div');
    handR.className = 'miniHand';
    [...pulso.R].forEach(bit => {
      const f = document.createElement('div');
      f.className = 'miniFinger';
      f.style.height = bit === '1' ? '70px' : '34px';
      f.style.background =
  bit === '1'
    ? (isPreview ? 'var(--pluma-preview)' : 'var(--green)')
    : 'var(--finger-off)';

f.style.opacity = bit === '1'
  ? (isPreview ? '0.7' : '1')
  : '0.35';

      handR.appendChild(f);
    });

    // mano izquierda
    const handL = document.createElement('div');
    handL.className = 'miniHand';
    [...pulso.L].forEach(bit => {
      const f = document.createElement('div');
      f.className = 'miniFinger';
      f.style.height = bit === '1' ? '70px' : '34px';
      f.style.background =
        bit === '1'
        ? (isPreview ? 'var(--pluma-preview)' : 'var(--green)')
        : 'var(--finger-off)';

      f.style.opacity = bit === '1'
     ? (isPreview ? '0.7' : '1')
    : '0.35';

      handL.appendChild(f);
    });

    row.appendChild(handR);
    row.appendChild(handL);
    container.appendChild(row);
  });
}

function highlightPlumaRow(index, active) {
  document.querySelectorAll(".pluma-row").forEach((row, i) => {
    row.classList.remove("preview", "active");

    if (i === index) {
      row.classList.add(active ? "active" : "preview");
    }
  });
}

//renderPluma(plumaCumbia);

function showPluma(pluma, btnId) {
  const title = document.getElementById("plumaTitle");
  const view  = document.getElementById("plumaView");

  view.innerHTML = "";

  if (!pluma) {
    title.textContent = "";
    activePluma = null;
    playMode = "random";
    setActivePlumaButton(null);
    return;
  }

  activePluma = pluma;
  playMode = "pluma";
  title.textContent = pluma.name;
  setActivePlumaButton(btnId);

  renderPluma(pluma);
}



document.getElementById("btnPlumaCumbia").addEventListener("click", () => {
  showPluma(plumaCumbia, "btnPlumaCumbia");
});

document.getElementById("btnPlumaRumba").addEventListener("click", () => {
  showPluma(plumaRumba, "btnPlumaRumba");
});

document.getElementById("btnPlumaZentangle").addEventListener("click", () => {
  showPluma(plumaZentangle, "btnPlumaZentangle");
});
document.getElementById("btnPlumaClear").addEventListener("click", clearPluma);


function clearPluma() {
  showPluma(null);
}

function setActivePlumaButton(activeId) {
  document.querySelectorAll(".pluma-btn").forEach(btn => {
    btn.classList.toggle("active", btn.id === activeId);
  });
}

// Toggle panel Plumas en móvil
document.addEventListener('DOMContentLoaded', () => {
  const toggle = document.getElementById('plumaToggle');
  const container = document.getElementById('plumaContainer');
  const icon = document.getElementById('plumaIcon');

  if (!toggle || !container) return;

  toggle.addEventListener('click', () => {
    const isExpanded = container.classList.toggle('expanded');
    toggle.classList.toggle('active', isExpanded);

    // Cambia flecha ↑/↓
    icon.textContent = isExpanded ? '▲' : '▼';
  });
});

function getBeatStartStep(){
  return 2; // siempre empieza al comenzar la activación
}

function updateBeatIndicator(){
  const beatCount = getBeatCount();
  const startStep = getBeatStartStep();
  const beatLine = document.getElementById('beatLine');

  // Antes de la activación → oculto
  if(step < startStep){
    beatLine.style.opacity = 0;
    return;
  }

  const beatIndex = step - startStep;

  // Ya no hay más beats → oculto
  if(beatIndex >= beatCount){
    beatLine.style.opacity = 0;
    return;
  }

  // Beat válido → muestro línea
  beatLine.style.opacity = 1;

  const angle = beatDirections[beatCount][beatIndex];
  beatLine.style.transform = `rotate(${angle}deg)`;
}



