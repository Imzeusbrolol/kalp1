<!doctype html>
<html lang="tr">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Happy Birthday 💖</title>
<style>
  html,body{
    height:100%;
    margin:0;
    font-family: "Segoe UI", Roboto, Arial, sans-serif;
    background: radial-gradient(circle at 10% 10%, #2b0f3a 0%, #0b0510 60%);
    color: white;
    display:flex;
    align-items:center;
    justify-content:center;
    flex-direction:column;
  }

  canvas{
    position:relative;
    width:320px;
    height:320px;
    display:block;
  }

  h1{
    margin-top:18px;
    font-size:28px;
    letter-spacing:1px;
    text-align:center;
    text-shadow: 0 6px 18px rgba(0,0,0,0.7);
  }

  /* küçük ekranlarda canvas'ı küçült */
  @media (max-width:420px){
    canvas{ width:260px; height:260px; }
    h1{ font-size:20px; }
  }
</style>
</head>
<body>
  <canvas id="c" width="320" height="320" aria-label="Kalp animasyonu"></canvas>
  <h1 id="msg">Happy Birthday!</h1>

<script>
const c = document.getElementById('c');
const ctx = c.getContext('2d');

let t = 0;                // zaman
const FPS = 60;
const centerX = c.width/2;
const centerY = c.height/2 + 20;

// Kalp şekli parametreyle çizilecek (polar/parametrik)
function drawHeart(scale, color, shadow){
  ctx.save();
  ctx.translate(centerX, centerY);
  ctx.scale(scale, scale);
  ctx.beginPath();
  // Parametrik kalp (k = param)
  // denklemi kullanan yaklaşık şekil
  const steps = 200;
  for(let i=0;i<=steps;i++){
    const ang = (i/steps) * Math.PI * 2;
    // klasik kalp benzeri fonksiyon
    const x = 16 * Math.pow(Math.sin(ang),3);
    const y = - (13 * Math.cos(ang) - 5 * Math.cos(2*ang) - 2 * Math.cos(3*ang) - Math.cos(4*ang));
    if(i===0) ctx.moveTo(x, y);
    else ctx.lineTo(x, y);
  }
  ctx.closePath();

  // gölge
  if(shadow){
    ctx.shadowColor = "rgba(0,0,0,0.6)";
    ctx.shadowBlur = 25;
    ctx.shadowOffsetY = 8;
  } else {
    ctx.shadowColor = "transparent";
  }

  // dolgu degrade
  const g = ctx.createLinearGradient(-60,-80,60,80);
  g.addColorStop(0, color[0]);
  g.addColorStop(0.5, color[1]);
  g.addColorStop(1, color[2]);
  ctx.fillStyle = g;
  ctx.fill();

  // dış çizgi
  ctx.lineWidth = 2.2;
  ctx.strokeStyle = "rgba(255,255,255,0.08)";
  ctx.stroke();

  ctx.restore();
}

// küçük parıltılar
function sparkle(){
  const n = 6;
  for(let i=0;i<n;i++){
    const a = Math.random()*Math.PI*2;
    const r = 60 + Math.random()*60;
    const sx = centerX + Math.cos(a)*r;
    const sy = centerY + Math.sin(a)*r*0.6 - 20;
    ctx.beginPath();
    ctx.fillStyle = "rgba(255,255,255,"+ (0.08 + Math.random()*0.12) +")";
    ctx.arc(sx, sy, 1+Math.random()*2, 0, Math.PI*2);
    ctx.fill();
  }
}

// animasyon döngüsü
function loop(){
  t += 1/FPS;
  // kalp atışı için ölçek: sin ile
  const beat = 1 + 0.12 * Math.abs(Math.sin(t*2.2)) + 0.02 * Math.sin(t*6);
  ctx.clearRect(0,0,c.width,c.height);

  // arka yumuşak halkalar
  for(let i=0;i<3;i++){
    const s = 0.9 + i*0.18;
    ctx.beginPath();
    ctx.globalAlpha = 0.06 - i*0.015;
    drawHeart(s * (1 + 0.02*Math.sin(t*1.7 + i)), ["#ff8aa2","#ff4d6d","#ff1e3b"], false);
    ctx.globalAlpha = 1;
  }

  // ana kalp degrade renk
  drawHeart(beat * 8.5, ["#ff7ab6","#ff2b6b","#d5003b"], true);

  // minik parıltılar
  sparkle();

  requestAnimationFrame(loop);
}

// Responsive: canvas iç piksel boyutu ile element boyutu hizala
function resizeCanvas(){
  // CSS boyutunu oku
  const cssW = c.clientWidth;
  const cssH = c.clientHeight;
  // yüksek DPR için
  const dpr = Math.min(window.devicePixelRatio || 1, 2);
  c.width = Math.round(cssW * dpr);
  c.height = Math.round(cssH * dpr);
  ctx.setTransform(dpr,0,0,dpr,0,0);
}

// başlangıçta canvas ölçüsünü uygun ayarla
(function init(){
  // elementin CSS genişlik/yüksekliğini ayarla (320x320)
  c.style.width = "320px";
  c.style.height = "320px";
  resizeCanvas();
  // yeniden boyutlandırma dinle
  window.addEventListener('resize', resizeCanvas);
  loop();
})();
</script>
</body>
</html>
