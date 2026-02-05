  :root{
    --bg:#111; --panel:#1b1b1b; --muted:#333; --violet:#b05cff; --green:#4cff4c; --finger-off:#555;
  }
  body{
    margin:0; font-family:system-ui,Arial,Helvetica,sans-serif; background:var(--bg); color:#eee;
    display:flex; gap:28px; height:100vh; box-sizing:border-box;
    justify-content: space-between; 
  }

  /* ------------- SIDEBAR HISTORIAL ------------- */
  #historyPanel{
    width:220px;
    padding:14px;
    box-sizing:border-box;
    background:var(--panel);
    border-right:1px solid var(--muted);
    overflow-y:auto;
  }
  #historyPanel h3{ margin:0 0 10px 0; font-size:15px; color:#ddd; text-align:center; }
  #historyList{ display:flex; flex-direction:column; gap:18px; }

  .histBlock{
    padding-bottom:8px;
    border-bottom:1px solid rgba(255,255,255,0.03);
  }

  .miniRow{
    display:flex; 
    justify-content:center;
    gap:6px;
    align-items:flex-end;
  }

  .miniHand{ display:flex; gap:3px; align-items:flex-end; justify-content:center; }

  .miniFinger{
    width:6px; 
    border-radius:3px;
    transition:height 0.18s;
  }

  /* ------------- SIDEBAR PRESETS ------------- */
  #presetsPanel{
    width:220px;
    padding:14px;
    box-sizing:border-box;
    background:var(--panel);
    border-left:1px solid var(--muted);
    overflow-y:auto;
    display: flex;
    flex-direction: column;
    gap: 15px;
  }
  #presetsPanel h3{ margin:0 0 10px 0; font-size:15px; color:#ddd; text-align:center; }

  #presetsList button{
    width: 100%;
    padding: 10px 8px;
    margin-bottom: 5px;
    border-radius: 6px;
    border: 1px solid var(--muted);
    background: #2a2a2a;
    color: #eee;
    cursor: pointer;
    font-size: 14px;
    text-align: center;
    transition: background 0.1s;
  }
  #presetsList button:hover{ background: #3a3a3a; }
  .presetActive{ 
    background: var(--violet) !important; 
    color: var(--bg) !important;
    border-color: var(--violet) !important;
  }

  /* ------------- MAIN ------------- */
#main{
  flex:1;
  padding:26px;
  box-sizing:border-box;
  display:flex;
  flex-direction:column;
  align-items:center;

  overflow-y: auto;   /* ← CLAVE */
}
  header{ 
  width:100%; 
  display:flex; 
  flex-direction: column; /* Apila el contenido (H1 y controles) */
  align-items: center;    /* Centra horizontalmente */
  gap:12px; 
}
h1{ margin:0; font-size:20px; text-align: center; } /* Aseguramos que el H1 esté centrado */
/* ... [CSS anterior] ... */

/* Aseguramos que los grupos de controles también se centren */
.controls-group{
  display:flex; 
  gap:14px; 
  align-items:center;
  justify-content: center; /* Centra los grupos dentro de sí mismos */
}

  .controls-group{
    display:flex; gap:14px; align-items:center;
  }

  /* Contenedores de botones de modo/ciclo */
  .modeBtns{ 
    display:flex; 
    gap:8px; 
    /* Aumento el margen interno para que no se vean pegados a otros controles */
    padding: 5px 0; 
  }
  
  /* ESTILOS DE BOTONES AMPLIADOS (Binario/Ternario y Ciclo 4/6) */
  .modeBtns button {
    padding: 12px 16px; /* Aumento del padding interno */
    border-radius: 8px; /* Borde más redondeado */
    border: 2px solid var(--violet); /* Borde más grueso */
    background: var(--panel); 
    color: var(--violet);    
    cursor: pointer;
    font-size: 16px; /* Aumento del tamaño de la fuente */
    /*font-weight: **bolder**; /* Grosor de letra más fuerte */
    transition: background-color 0.1s, color 0.1s, border-color 0.1s;  }

.modeBtns button {
  /* ... otras propiedades ... */
  font-size: 15px; /* ¡Letra más grande! */
  font-weight: 600; /* ¡Máximo grosor! */
  /* ... otras propiedades ... */
}

  .modeActive{ 
    background: var(--green) !important; 
    color: var(--bg) !important;       
    border-color: var(--green) !important; /* Borde del color activo */
  }  

/* ... [Resto del CSS] ... */

/* Estilo para los botones Iniciar/Detener y el input BPM (ya estaban bien, solo para referencia) */
.controls input[type=number]{ width:60px; padding:6px; border-radius:6px; border:1px solid #333; background:#151515; color:#eee; }
.controls button{ 
  padding:10px 12px; 
  border-radius:6px; 
  border:1px solid #333; 
  background:#222; 
  color:#eee; 
  cursor:pointer; 
  font-weight: bold;
}

  #combo{ color: #111; margin-top:18px; font-weight:#111; font-size:20px; letter-spacing:4px; text-align:center; }

  /* Contenedor principal de las 4 manos */
  .hands-grid{ 
    display:grid; 
    grid-template-columns: repeat(2, 1fr); 
    gap: 40px 80px; 
    margin-top:22px; 
    max-width: 600px;
  }

  /* Por defecto, manos superiores ocultas (para el modo 2 sets) */
  #handUL, #handUR { display: none; }

  /* Ajustamos el layout si solo hay 2 manos visibles */
  .hands-grid.hands-2-set {
    display: flex;
    justify-content: center;
    gap: 80px;
  }
  .hands-grid.hands-2-set .hand { margin-top: 40px; }

  /* Nuevo estilo para botones inactivos (por defecto) */
.modeBtns button {
  background: var(--panel); /* Fondo oscuro */
  color: var(--violet);    /* Texto violeta para inactivo */
  border: 1px solid var(--violet);
  transition: background 0.1s, color 0.1s;
}

  .hand{ display:flex; gap:8px; align-items:flex-end; }

  .finger{
    width:20px; border-radius:6px; transition:height .18s, background-color .18s, opacity .18s;
  }
  .on{ height:120px; opacity:1; }
  .off{ height:60px; opacity:0.45; }

  .previewColor{ background:var(--violet); }
  .activeColor{ background:var(--green); }

  .pulse{
    width:24px; height:24px; background:#444; border-radius:50%; margin-top:18px; transition:transform .12s, background .12s;
  }
  .pulse.flash{ transform:scale(1.5); }

  footer{ margin-top:auto; color:#bbb; font-size:13px; padding-bottom:10px; }

  /* small screens: collapse sidebars */
  @media (max-width:1300px){
    #historyPanel, #presetsPanel{ width: 180px; }
  }
  @media (max-width:1100px){
    header{ flex-direction:column; align-items:flex-start; }
    .controls-group{ flex-wrap:wrap; margin-top:10px; }
    body{ display:block; padding: 12px; }
    #historyPanel, #presetsPanel{ display:none; }
    #main{ width: 100%; padding: 12px; }
  }
.preset-controls {
  display: flex;
  gap: 8px;
  margin: 12px 0;
}

#presetName {
  flex: 1;
  padding: 8px 10px;
  border-radius: 6px;
  border: 1px solid var(--muted);
  background: #222;
  color: #eee;
  font-size: 14px;
}

#btnSavePreset,
#btnLoadPreset,
#btnDeletePreset {
  padding: 8px 12px;
  border-radius: 6px;
  border: 1px solid var(--violet);
  background: var(--panel);
  color: var(--violet);
  cursor: pointer;
  font-size: 14px;
}

#btnSavePreset:hover { background: #3a3a3a; }
#btnLoadPreset:hover:not(:disabled) { background: var(--green); color: #111; }
#btnDeletePreset:hover:not(:disabled) { background: #ff4444; color: white; }

#presetsList {
  display: flex;
  flex-direction: column;
  gap: 6px;
  max-height: 380px;
  overflow-y: auto;
}

.preset-item {
  padding: 10px 12px;
  background: #222;
  border-radius: 6px;
  cursor: pointer;
  border: 1px solid transparent;
  transition: all 0.15s;
  font-size: 14px;
}

.preset-item:hover {
  background: #333;
  border-color: var(--violet);
}

.preset-item.selected {
  background: var(--violet);
  color: #111;
  border-color: var(--violet);
}

.preset-item .bits {
  font-size: 11px;
  opacity: 0.7;
  margin-left: 8px;
}

.preset-controls {
  display: flex;
  gap: 8px;
  margin: 12px 0;
}

#presetName {
  flex: 1;
  padding: 8px 10px;
  border-radius: 6px;
  border: 1px solid var(--muted);
  background: #222;
  color: #eee;
  font-size: 14px;
}

#btnSavePreset,
#btnLoadPreset,
#btnDeletePreset {
  padding: 8px 14px;
  border-radius: 6px;
  border: 1px solid var(--violet);
  background: var(--panel);
  color: var(--violet);
  cursor: pointer;
  font-size: 14px;
}

#btnSavePreset:hover { background: #3a3a3a; }

#btnLoadPreset:hover:not(:disabled) {
  background: var(--green);
  color: #111;
}

#btnDeletePreset:hover:not(:disabled) {
  background: #ff4444;
  color: white;
}

#btnLoadPreset:disabled,
#btnDeletePreset:disabled {
  opacity: 0.4;
  cursor: not-allowed;
}
.pluma-view{
  width: 100%;
  max-height: 50vh;
  overflow-y: auto;
  padding: 20px 0;
}
.pluma-view .miniHand {
  gap: 8px;
}

.pluma-view .miniFinger {
  width: 22px;
  border-radius: 6px;
}


.pluma-row {
  display: flex;
  gap: 40px;
  align-items: flex-end;
}

.pluma-label {
  width: 70px;
  font-size: 12px;
  color: #888;
  text-align: right;
}

.pluma-hand {
  display: flex;
  gap: 10px;
}
.pluma-view {
  position: relative;
  z-index: 1;
}

.controls,
button {
  position: relative;
  z-index: 5;
}
.hands-container{
  width: 100%;
  max-width: 600px;   /* igual que el grid de arriba */
}
.plumas-panel {
  position: fixed;
  right: 10px;
  top: 100px;
  width: 130px;
  padding: 10px;
  background: #111;
  border: 1px solid #222;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0,0,0,.4);
  z-index: 20;
}

.plumas-panel h4 {
  margin: 0 0 12px 0;
  font-size: 13px;
  color: #aaa;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.pluma-btn {
  width: 100%;
  padding: 10px;
  margin-bottom: 6px;
  background: #1a1a1a;
  color: #aaa;
  border: 1px solid #333;
  cursor: pointer;
}

.pluma-btn:hover {
  background: #222;
}

.pluma-btn.active {
  background: #0f5;
  color: #000;
  border-color: #0f5;
  box-shadow: 0 0 8px rgba(0,255,120,0.6);
}
.pluma-row {
  opacity: 0.25;
  transition: opacity 0.2s, transform 0.2s;
}

.pluma-row.preview {
  opacity: 0.5;
}

.pluma-row.active {
  opacity: 1;
  transform: scale(1.05);
}
:root {
  --pluma-preview: #b05cff; 
}


/*nuevo desde aca



/* Por defecto (escritorio) siempre visible */
.hands-container {
  transition: all 0.3s ease;
}

/* En móvil */
@media (max-width: 768px) {
  .hands-container {
    max-height: 0;
    overflow: hidden;
    opacity: 0;
    transition: max-height 0.4s ease, opacity 0.3s ease;
    background: rgba(30,30,30,0.9);
    border-radius: 8px;
    margin: 0 10px;
    padding: 0 10px;
  }

  .hands-container.expanded {
    max-height: 60vh;          /* o 70vh, lo que te guste */
    opacity: 1;
    padding: 15px 10px;
  }

  #plumaToggle {
    background: #222;
    padding: 10px 15px;
    border-radius: 8px 8px 0 0;
    margin: 0 10px;
    text-align: center;
    font-size: 16px;
    cursor: pointer;
    user-select: none;
  }

  #plumaIcon {
    margin-left: 8px;
    transition: transform 0.3s;
  }

  #plumaToggle.active #plumaIcon {
    transform: rotate(180deg);
  }

  .pluma-view {
    max-height: none; /* quitamos límite para que crezca natural */
    overflow-y: auto;
  }
}

/* Escritorio: siempre completo */
@media (min-width: 769px) {
  .hands-container {
    max-height: none;
    opacity: 1;
  }
}
@media (max-width: 768px) {
  #plumaContainer {
    max-height: 0;
    overflow: hidden;
    opacity: 0;
    transition: max-height 0.4s ease, opacity 0.3s ease;
    background: rgba(30,30,30,0.95);
    border-radius: 8px;
    margin: 10px;
    padding: 0;
  }

  #plumaContainer.expanded {
    max-height: 70vh;  /* ajustá según necesites */
    opacity: 1;
    padding: 15px;
  }

  .plumas-panel {
    position: static !important;  /* importante: sacamos fixed en móvil */
    width: 100%;
    box-shadow: none;
    border: none;
    background: transparent;
  }

  #plumaToggle {
    background: #222;
    padding: 12px;
    margin: 10px;
    border-radius: 8px;
    text-align: center;
    font-size: 16px;
  }
}

@media (min-width: 769px) {
  #plumaContainer {
    max-height: none !important;
    opacity: 1 !important;
  }
  .plumas-panel {
    position: fixed;
    /* mantiene el estilo original en escritorio */
  }
}

#beatIndicator {
  margin-top: 14px;
  opacity: 0.8;
}

#beatLine {
  transform-origin: 50% 50%;
  transition: transform 0.12s ease-out, opacity 0.1s;
  opacity: 0; /* oculta por defecto */
}

