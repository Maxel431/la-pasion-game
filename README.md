# la-pasion-game
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>El Viaje de la Electricidad - Pro ⚡</title>
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700&family=Nunito:wght@300;600;800&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <canvas id="bg-canvas"></canvas>

  <div class="ui">
    <header class="topbar">
      <div class="title">El Viaje de la Electricidad <span class="spark">⚡</span></div>
      <div class="controls">
        <button id="btn-sound" class="icon">🔊</button>
        <button id="btn-start" class="primary">INICIAR VIAJE</button>
      </div>
    </header>

    <main class="main">
      <aside class="panel left">
        <div class="level-card">
          <h3 id="level-title">Estación</h3>
          <div id="level-art" class="level-art"></div>
          <div class="meter">
            <div class="meter-label">Progreso del Sistema</div>
            <div class="meter-bar"><div id="meter-fill" class="meter-fill"></div></div>
            <div id="score" class="score">Puntaje: 0</div>
          </div>
        </div>
      </aside>

      <section class="panel center">
        <div id="game-area" class="game-area hidden">
          <div id="question-card" class="question-card">
            <div id="question-number" class="qnum">Nivel 1 • Pregunta 1</div>
            <h2 id="question-text">Texto pregunta...</h2>
            <div id="answers" class="answers"></div>
          </div>
          <div id="feedback" class="feedback"></div>
          <div class="actions">
            <button id="btn-next" class="btn" style="display:none;">Siguiente</button>
            <button id="btn-skip" class="btn secondary">Omitir (-0.5)</button>
          </div>
        </div>

        <div id="start-screen" class="start-screen">
          <h2>Bienvenido, Crono-Técnico</h2>
          <p>Responde correctamente para que la energía fluya y la ciudad brille. ¡2-3 preguntas por nivel!</p>
          <div class="start-hint">Usá los botones o el teclado (1-4) para elegir</div>
        </div>

        <div id="end-screen" class="end-screen hidden">
          <h2 id="end-title">¡Viaje completado!</h2>
          <p id="end-text">Resultado</p>
          <button id="btn-restart" class="primary">Reiniciar Viaje</button>
        </div>
      </section>

      <aside class="panel right">
        <div class="timeline">
          <h4>Estaciones</h4>
          <ol id="levels-list" class="levels-list"></ol>
        </div>
      </aside>
    </main>

    <footer class="footer">Proyecto Pro · El Viaje de la Electricidad · Hecho por Axel</footer>
  </div>

  <script src="script.js"></script>
</body>
</html>

/* Pro styles for El Viaje de la Electricidad */
:root{
  --bg1:#020214; --accent:#00eaff; --accent2:#7cffb2; --muted:#9fb7c9;
  --card: rgba(255,255,255,0.03);
}

*{box-sizing:border-box}
html,body{height:100%;margin:0;font-family:Nunito,system-ui,Arial;background:var(--bg1);color:#eaf7ff;overflow:hidden}
canvas#bg-canvas{position:fixed;left:0;top:0;width:100%;height:100%;z-index:0;display:block;filter:contrast(1.05)}

.ui{position:relative;z-index:2;max-width:1200px;margin:24px auto;padding:16px;border-radius:12px}
.topbar{display:flex;justify-content:space-between;align-items:center;padding:8px 12px}
.title{font-family:Orbitron,monospace;font-weight:700;color:var(--accent);font-size:20px;display:flex;gap:8px;align-items:center}
.spark{animation:blink 1.2s infinite}
@keyframes blink{0%{opacity:1}50%{opacity:0.4}100%{opacity:1}}

.controls{display:flex;gap:10px}
.icon{background:transparent;border:1px solid rgba(255,255,255,0.04);color:var(--accent);padding:8px 10px;border-radius:8px;cursor:pointer}
.primary{background:linear-gradient(90deg,var(--accent),#4bd6ff);color:#022; padding:10px 14px;border-radius:10px;border:none;font-weight:800;cursor:pointer}

.main{display:grid;grid-template-columns:300px 1fr 220px;gap:18px;align-items:start;margin-top:12px}
.panel{background:var(--card);padding:14px;border-radius:12px;border:1px solid rgba(255,255,255,0.02)}

/* left panel */
.level-card h3{margin:0 0 10px 0;color:var(--accent)}
.level-art{height:120px;border-radius:8px;background:linear-gradient(180deg,#022,#034);box-shadow:0 8px 20px rgba(0,0,0,0.6);margin-bottom:12px}
.meter{margin-top:6px}
.meter-label{font-size:12px;color:var(--muted);margin-bottom:6px}
.meter-bar{background:rgba(255,255,255,0.02);height:12px;border-radius:8px;overflow:hidden}
.meter-fill{height:100%;width:0;background:linear-gradient(90deg,var(--accent),var(--accent2));transition:width 600ms ease}

.score{margin-top:10px;color:var(--accent2);font-weight:800}

/* center */
.question-card{background:linear-gradient(180deg,rgba(255,255,255,0.02),rgba(255,255,255,0.01));padding:16px;border-radius:10px}
.qnum{font-size:12px;color:var(--muted);margin-bottom:8px}
h2#question-text{margin:0 0 12px 0;color:#fff}
.answers{display:flex;flex-direction:column;gap:10px}
.answer-btn{background:transparent;border:1px solid rgba(255,255,255,0.04);padding:12px;border-radius:10px;color:var(--accent);text-align:left;cursor:pointer;font-weight:700;transition:transform 160ms,box-shadow 160ms}
.answer-btn:hover{transform:translateY(-4px);box-shadow:0 10px 30px rgba(0,0,0,0.6)}
.answer-correct{background:linear-gradient(90deg,#9effc2,#2bf0a8);color:#022b1e;border:none}
.answer-wrong{background:linear-gradient(90deg,#ffb3b3,#ff6b6b);color:#3a0202;border:none}

.feedback{min-height:28px;margin-top:12px;color:#ffdca1;font-weight:700}

/* actions */
.actions{display:flex;gap:10px;justify-content:flex-end;margin-top:12px}
.btn{background:linear-gradient(90deg,#0077ff,#4ba6ff);color:white;padding:8px 12px;border-radius:8px;border:none;cursor:pointer;font-weight:700}
.secondary{background:rgba(255,255,255,0.03);color:#cfefff}

/* right timeline */
.levels-list{list-style:none;padding:0;margin:6px 0 0 0;display:flex;flex-direction:column;gap:6px}
.levels-list li{padding:8px;border-radius:8px;background:rgba(255,255,255,0.01);color:var(--muted);display:flex;justify-content:space-between;align-items:center}
.levels-list li.active{background:linear-gradient(90deg,rgba(0,234,255,0.08),rgba(123,255,180,0.05));color:var(--accent)}

/* start & end screens */
.start-screen, .end-screen{padding:24px;text-align:center}
.hidden{display:none}

.footer{text-align:center;color:var(--muted);margin-top:12px;font-size:13px}

/* responsive */
@media (max-width:980px){
  .main{grid-template-columns:1fr;min-height:0}
  .panel.right{order:3}
  .panel.left{order:2}
  .panel.center{order:1}
}

// Pro version script for El Viaje de la Electricidad
const LEVELS = [
  { id:'gen', title:'Central - Generación', color:'#013a5d', questions:[
    { q:'¿Qué componente gira dentro de una central hidroeléctrica para generar energía?', opts:['Motor','Turbina','Batería','Transformador'], a:1 },
    { q:'¿Qué energía convierte la turbina en electricidad?', opts:['Luminosa','Química','Mecánica','Térmica'], a:2 }
  ]},
  { id:'trans', title:'Transformador', color:'#3b2b6b', questions:[
    { q:'¿Cuál es la función principal de un transformador?', opts:['Cambiar voltaje','Almacenar energía','Producir luz','Medir corriente'], a:0 },
    { q:'¿Los transformadores suelen operar con corriente?', opts:['Alterna (AC)','Continua (DC)','Ambas','Ninguna'], a:0 }
  ]},
  { id:'red', title:'Red de Transmisión', color:'#003b2b', questions:[
    { q:'¿Por qué se usan líneas de alta tensión en transmisión?', opts:['Por estética','Para reducir pérdidas','Porque son más baratas','Para enfriar'], a:1 },
    { q:'¿Qué material es común en cables por su conductividad?', opts:['Plástico','Cobre','Madera','Vidrio'], a:1 }
  ]},
  { id:'ciudad', title:'Distribución - Ciudad', color:'#2b3b7f', questions:[
    { q:'¿Qué aparato protege contra sobrecargas en casa?', opts:['Transformador','Fusible/Interruptor','Generador','Panel solar'], a:1 },
    { q:'¿Qué es eficiente para el consumo doméstico?', opts:['Bombillas incandescentes','Bombillas LED','Dejar todo encendido','Uso excesivo'], a:1 }
  ]}
];

// DOM
const btnStart = document.getElementById('btn-start');
const btnSound = document.getElementById('btn-sound');
const btnNext = document.getElementById('btn-next');
const btnSkip = document.getElementById('btn-skip');
const btnRestart = document.getElementById('btn-restart');
const gameArea = document.getElementById('game-area');
const startScreen = document.getElementById('start-screen');
const endScreen = document.getElementById('end-screen');
const levelTitle = document.getElementById('level-title');
const levelArt = document.getElementById('level-art');
const meterFill = document.getElementById('meter-fill');
const scoreEl = document.getElementById('score');
const answersDiv = document.getElementById('answers');
const feedback = document.getElementById('feedback');
const levelsList = document.getElementById('levels-list');
const questionNumber = document.getElementById('question-number');
const questionText = document.getElementById('question-text');

let currentLevel = 0, currentQuestion = 0, score = 0, audioOn = true;

// populate levels list
LEVELS.forEach((lv, idx)=>{
  const li = document.createElement('li');
  li.textContent = lv.title;
  if(idx===0) li.classList.add('active');
  levelsList.appendChild(li);
});

function renderLevel(){
  const lv = LEVELS[currentLevel];
  levelTitle.textContent = lv.title;
  levelArt.style.background = `linear-gradient(180deg, ${lv.color}, #001)`;
  // show question
  const q = lv.questions[currentQuestion];
  questionNumber.textContent = `Nivel ${currentLevel+1} • Pregunta ${currentQuestion+1}`;
  questionText.textContent = q.q;
  answersDiv.innerHTML = '';
  q.opts.forEach((opt, i)=>{
    const b = document.createElement('button');
    b.className = 'answer-btn';
    b.textContent = `${String.fromCharCode(65+i)}. ${opt}`;
    b.addEventListener('click', ()=> selectAnswer(i, b));
    answersDiv.appendChild(b);
  });
  feedback.textContent = '';
  btnNext.style.display = 'none';
  updateMeter();
  highlightLevels();
}

function selectAnswer(i, btn){
  const lv = LEVELS[currentLevel];
  const q = lv.questions[currentQuestion];
  const correct = q.a;
  const buttons = Array.from(answersDiv.children);
  buttons.forEach(b=> b.disabled = true);
  if(i===correct){
    btn.classList.add('answer-correct');
    feedback.textContent = '¡Correcto! La energía fluye.';
    score += 1;
    playTone(900,0.12);
  } else {
    btn.classList.add('answer-wrong');
    buttons[correct].classList.add('answer-correct');
    feedback.textContent = 'Incorrecto. Pérdida parcial de energía.';
    score -= 0.5;
    playTone(260,0.18);
  }
  score = Math.max(0, score);
  scoreEl.textContent = 'Puntaje: ' + (Math.round(score*10)/10);
  btnNext.style.display = 'inline-block';
  updateMeter();
}

function updateMeter(){
  const totalQ = LEVELS.reduce((s,lv)=> s + lv.questions.length, 0);
  const answered = LEVELS.slice(0,currentLevel).reduce((s,lv)=> s + lv.questions.length, 0) + currentQuestion + 1;
  const pct = Math.round((answered/totalQ)*100);
  meterFill.style.width = pct + '%';
}

function highlightLevels(){
  const items = levelsList.children;
  for(let i=0;i<items.length;i++){
    items[i].classList.toggle('active', i===currentLevel);
  }
}

btnStart.addEventListener('click', ()=>{
  startScreen.classList.add('hidden');
  gameArea.classList.remove('hidden');
  btnStart.style.display = 'none';
  btnSound.textContent = audioOn ? '🔊' : '🔈';
  renderLevel();
  playBackground();
});

btnNext.addEventListener('click', ()=>{
  const lv = LEVELS[currentLevel];
  if(currentQuestion < lv.questions.length - 1){
    currentQuestion++;
  } else {
    if(currentLevel < LEVELS.length - 1){
      currentLevel++; currentQuestion = 0;
    } else {
      finishGame(); return;
    }
  }
  renderLevel();
});

btnSkip.addEventListener('click', ()=>{
  score -= 0.5; score = Math.max(0, score);
  scoreEl.textContent = 'Puntaje: ' + (Math.round(score*10)/10);
  btnNext.click();
});

btnRestart.addEventListener('click', ()=> location.reload());

btnSound.addEventListener('click', ()=>{
  audioOn = !audioOn;
  btnSound.textContent = audioOn ? '🔊' : '🔈';
  if(!audioOn) stopBackground();
  else playBackground();
});

function finishGame(){
  gameArea.classList.add('hidden');
  endScreen.classList.remove('hidden');
  document.getElementById('end-title').textContent = score >= (LEVELS.length*2) ? '¡Maestro de la Electricidad!' : 'Buen trabajo — sigue aprendiendo';
  document.getElementById('end-text').textContent = `Puntaje final: ${Math.round(score*10)/10}`;
  stopBackground();
  playVictory();
}

// keyboard 1-4
window.addEventListener('keydown', (e)=>{
  if(gameArea.classList.contains('hidden')) return;
  const idx = ['Digit1','Digit2','Digit3','Digit4'].indexOf(e.code);
  if(idx>=0){
    const btn = answersDiv.children[idx];
    if(btn) btn.click();
  }
});

// --- Audio: WebAudio background hum + tones
let audioCtx, bgOsc, bgGain;
function initAudio(){
  if(audioCtx) return;
  audioCtx = new (window.AudioContext || window.webkitAudioContext)();
}
function playBackground(){
  if(!audioOn) return;
  initAudio();
  bgOsc = audioCtx.createOscillator();
  bgGain = audioCtx.createGain();
  bgOsc.type = 'sine'; bgOsc.frequency.value = 60;
  bgGain.gain.value = 0.02;
  bgOsc.connect(bgGain); bgGain.connect(audioCtx.destination);
  bgOsc.start();
}
function stopBackground(){ if(bgOsc){ bgOsc.stop(); bgOsc.disconnect(); bgOsc=null; } }

function playTone(freq, duration=0.12){
  if(!audioOn) return;
  initAudio();
  const o = audioCtx.createOscillator(); const g = audioCtx.createGain();
  o.type='sine'; o.frequency.value = freq; g.gain.value=0.08;
  o.connect(g); g.connect(audioCtx.destination);
  o.start(); setTimeout(()=> o.stop(), duration*1000);
}

function playVictory(){
  if(!audioOn) return;
  playTone(880,0.18); setTimeout(()=> playTone(1200,0.12), 200);
}

// --- Background canvas animation (particles + lightning lines)
const canvas = document.getElementById('bg-canvas');
const ctx = canvas.getContext('2d');
let W = canvas.width = innerWidth, H = canvas.height = innerHeight;
window.addEventListener('resize', ()=>{ W = canvas.width = innerWidth; H = canvas.height = innerHeight; initParticles(); });

let particles = [];
function initParticles(){ particles = []; const count = Math.max(60, Math.floor((W*H)/90000)); for(let i=0;i<count;i++){ particles.push({x:Math.random()*W,y:Math.random()*H,r:Math.random()*1.6+0.6,vx:(Math.random()-0.5)*0.6,vy:(Math.random()-0.5)*0.6,alpha:Math.random()*0.6+0.2}); } }
function draw(){ ctx.clearRect(0,0,W,H);
  // gradient bg
  const g = ctx.createLinearGradient(0,0,0,H); g.addColorStop(0,'#001021'); g.addColorStop(1,'#000610'); ctx.fillStyle = g; ctx.fillRect(0,0,W,H);
  // electric lines
  for(let i=0;i<5;i++){ ctx.beginPath(); const y = H*(0.12 + i*0.18); ctx.moveTo(0,y); for(let x=0;x<W;x+=40){ ctx.lineTo(x, y + Math.sin((x*0.02) + Date.now()*0.002 + i)*18); } ctx.strokeStyle = 'rgba(0,180,255,0.03)'; ctx.lineWidth = 1; ctx.stroke(); }
  // particles
  for(const p of particles){ p.x+=p.vx; p.y+=p.vy; if(p.x<0) p.x=W; if(p.x>W) p.x=0; if(p.y<0) p.y=H; if(p.y>H) p.y=0; ctx.beginPath(); ctx.arc(p.x,p.y,p.r,0,Math.PI*2); ctx.fillStyle = 'rgba(60,200,255,'+p.alpha+')'; ctx.fill(); }
  requestAnimationFrame(draw);
}
initParticles(); draw();

// start with start screen visible
// show levels list titles
(function init(){
  const list = document.getElementById('levels-list');
  list.innerHTML = '';
  LEVELS.forEach(l=>{ const li = document.createElement('li'); li.textContent = l.title; list.appendChild(li); });
})();
