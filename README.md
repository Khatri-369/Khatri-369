<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>Om Khatri — MERN Stack Developer</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
<link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500&family=Space+Grotesk:wght@300;400;500;600;700&display=swap" rel="stylesheet"/>
<style>
  *{margin:0;padding:0;box-sizing:border-box}
  body{
    min-height:100vh;
    background:#060914;
    display:flex;align-items:center;justify-content:center;
    padding:24px;
    font-family:'Space Grotesk',sans-serif;
  }
  .profile-wrap{
    position:relative;width:100%;max-width:680px;
    min-height:720px;overflow:hidden;
    border-radius:20px;
    border:0.5px solid rgba(255,255,255,0.08);
    background:rgba(8,10,20,0.9);
    backdrop-filter:blur(12px);
  }
  #canvas3d{position:absolute;top:0;left:0;z-index:0;width:100%;height:100%}
  .content{position:relative;z-index:10;padding:40px 36px 36px;color:#e8eaf6}

  /* Hero */
  .hero{display:flex;align-items:center;gap:24px;margin-bottom:28px}
  .avatar-ring{
    width:88px;height:88px;border-radius:50%;padding:3px;flex-shrink:0;
    background:linear-gradient(135deg,#6C63FF,#00D4FF,#00FF9D);
    animation:spinRing 6s linear infinite;
  }
  @keyframes spinRing{to{transform:rotate(360deg)}}
  .avatar-inner{
    width:100%;height:100%;border-radius:50%;
    background:#0d1128;
    display:flex;align-items:center;justify-content:center;
    font-size:28px;font-weight:700;color:#6C63FF;
    font-family:'Fira Code',monospace;
    animation:spinRing 6s linear infinite reverse;
  }
  .hero-text h1{font-size:24px;font-weight:700;color:#fff;letter-spacing:-0.3px}
  .hero-text .role{font-family:'Fira Code',monospace;font-size:12px;color:#00D4FF;margin-top:5px}
  .hero-text .at{font-size:12px;color:#6a7490;margin-top:5px}

  /* Badges */
  .badge-row{display:flex;flex-wrap:wrap;gap:6px;margin-bottom:28px}
  .badge{
    font-family:'Fira Code',monospace;font-size:11px;
    padding:4px 11px;border-radius:20px;border:1px solid;font-weight:400;
  }
  .b-purple{color:#b89cff;border-color:#4a3a7a;background:rgba(108,99,255,0.12)}
  .b-cyan{color:#00D4FF;border-color:#0a4a5a;background:rgba(0,212,255,0.1)}
  .b-green{color:#00FF9D;border-color:#004a30;background:rgba(0,255,157,0.1)}
  .b-amber{color:#ffb74d;border-color:#5a3a00;background:rgba(255,183,77,0.1)}
  .b-pink{color:#f48fb1;border-color:#5a1a30;background:rgba(244,143,177,0.1)}

  /* Section label */
  .section-label{
    font-family:'Fira Code',monospace;font-size:10px;color:#00D4FF;
    letter-spacing:2.5px;text-transform:uppercase;
    margin-bottom:14px;
    display:flex;align-items:center;gap:10px;
  }
  .section-label::after{content:'';flex:1;height:1px;background:linear-gradient(90deg,rgba(0,212,255,0.35),transparent)}

  /* Cards */
  .grid2{display:grid;grid-template-columns:1fr 1fr;gap:14px;margin-bottom:28px}
  .card3d{
    background:rgba(255,255,255,0.03);
    border:0.5px solid rgba(255,255,255,0.08);
    border-radius:14px;padding:18px;
    transition:transform 0.35s cubic-bezier(.23,1,.32,1),box-shadow 0.35s;
    cursor:default;
  }
  .card3d:hover{
    transform:translateY(-5px) rotateX(4deg) rotateY(-2deg);
    box-shadow:0 16px 40px rgba(108,99,255,0.22);
    border-color:rgba(108,99,255,0.3);
  }
  .card-icon{font-size:24px;margin-bottom:10px}
  .card-title{font-size:13px;font-weight:600;color:#c8d0e0;margin-bottom:5px}
  .card-sub{font-size:11px;color:#6a7490;line-height:1.6}

  /* Tech pills */
  .tech-grid{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:28px}
  .tech-pill{
    display:flex;align-items:center;gap:6px;
    font-family:'Fira Code',monospace;font-size:11px;
    padding:5px 11px;border-radius:8px;
    border:0.5px solid rgba(255,255,255,0.1);
    background:rgba(255,255,255,0.04);color:#8892b0;
    transition:all 0.2s;cursor:default;
  }
  .tech-pill:hover{background:rgba(108,99,255,0.15);border-color:#6C63FF;color:#b89cff;transform:translateY(-2px)}
  .tech-dot{width:7px;height:7px;border-radius:50%;flex-shrink:0}

  /* Goals */
  .goals-list{display:flex;flex-direction:column;gap:10px;margin-bottom:28px}
  .goal-item{display:flex;align-items:center;gap:12px;font-size:12px}
  .goal-name{width:150px;flex-shrink:0;color:#c8d0e0}
  .goal-bar-wrap{flex:1;height:4px;background:rgba(255,255,255,0.07);border-radius:2px;overflow:hidden}
  .goal-bar{height:100%;border-radius:2px;width:0%;transition:width 1.8s cubic-bezier(.23,1,.32,1)}
  .goal-pct{font-family:'Fira Code',monospace;font-size:10px;color:#6a7490;flex-shrink:0;width:30px;text-align:right}

  /* Stats */
  .stat-row{display:grid;grid-template-columns:repeat(3,1fr);gap:12px;margin-bottom:28px}
  .stat-box{
    text-align:center;
    background:rgba(255,255,255,0.03);
    border:0.5px solid rgba(255,255,255,0.08);
    border-radius:12px;padding:14px 8px;
    transition:border-color 0.2s,transform 0.2s;
  }
  .stat-box:hover{border-color:rgba(108,99,255,0.3);transform:translateY(-3px)}
  .stat-num{
    font-size:22px;font-weight:700;font-family:'Fira Code',monospace;
    background:linear-gradient(135deg,#6C63FF,#00D4FF);
    -webkit-background-clip:text;-webkit-text-fill-color:transparent;
    background-clip:text;
  }
  .stat-lbl{font-size:10px;color:#6a7490;margin-top:4px;letter-spacing:0.5px}

  /* CTA */
  .cta{text-align:center;padding-top:18px;border-top:0.5px solid rgba(255,255,255,0.07)}
  .cta p{font-size:12px;color:#6a7490;font-family:'Fira Code',monospace;margin-bottom:14px}
  .connect-btns{display:flex;justify-content:center;gap:10px;flex-wrap:wrap}
  .cta-btn{
    display:inline-flex;align-items:center;gap:8px;
    font-family:'Fira Code',monospace;font-size:11px;
    padding:9px 20px;border-radius:8px;
    border:0.5px solid rgba(108,99,255,0.4);
    background:rgba(108,99,255,0.15);color:#b89cff;
    cursor:pointer;text-decoration:none;
    transition:all 0.2s;
  }
  .cta-btn:hover{background:rgba(108,99,255,0.3);border-color:#6C63FF;color:#fff;transform:translateY(-2px)}
  .cta-btn.primary{background:linear-gradient(135deg,#6C63FF,#4a54b8);color:#fff;border:none}
  .cta-btn.primary:hover{opacity:0.88;transform:translateY(-2px)}

  @media(max-width:520px){
    .content{padding:28px 20px 24px}
    .hero-text h1{font-size:20px}
    .grid2{grid-template-columns:1fr}
    .stat-row{grid-template-columns:repeat(3,1fr)}
  }
</style>
</head>
<body>

<div class="profile-wrap">
  <canvas id="canvas3d"></canvas>

  <div class="content">
    <!-- Hero -->
    <div class="hero">
      <div class="avatar-ring">
        <div class="avatar-inner">OK</div>
      </div>
      <div class="hero-text">
        <h1>Om Khatri</h1>
        <div class="role">&lt; MERN Stack Developer /&gt;</div>
        <div class="at">💼 Full-Stack Dev Intern @ Nayoda &nbsp;·&nbsp; Vadodara, IN</div>
      </div>
    </div>

    <!-- Badges -->
    <div class="badge-row">
      <span class="badge b-purple">Full-Stack Dev</span>
      <span class="badge b-cyan">MERN Stack</span>
      <span class="badge b-green">DSA Enthusiast</span>
      <span class="badge b-amber">Open Source</span>
      <span class="badge b-pink">React.js</span>
    </div>

    <!-- About cards -->
    <div class="section-label">About Me</div>
    <div class="grid2">
      <div class="card3d">
        <div class="card-icon">🚀</div>
        <div class="card-title">Current Role</div>
        <div class="card-sub">Full-Stack Dev Intern @ Nayoda · Building production-grade MERN applications</div>
      </div>
      <div class="card3d">
        <div class="card-icon">🧠</div>
        <div class="card-title">Learning</div>
        <div class="card-sub">Advanced MERN · DSA · Backend Architecture · System Design · Scalable Apps</div>
      </div>
      <div class="card3d">
        <div class="card-icon">💬</div>
        <div class="card-title">Ask Me About</div>
        <div class="card-sub">React, Node, MongoDB, JWT Auth, REST APIs, Express, Problem Solving</div>
      </div>
      <div class="card3d">
        <div class="card-icon">⚡</div>
        <div class="card-title">Fun Fact</div>
        <div class="card-sub">I enjoy transforming ideas into real-world web applications that people love</div>
      </div>
    </div>

    <!-- Tech Stack -->
    <div class="section-label">Tech Stack</div>
    <div class="tech-grid">
      <span class="tech-pill"><span class="tech-dot" style="background:#61DAFB"></span>React.js</span>
      <span class="tech-pill"><span class="tech-dot" style="background:#339933"></span>Node.js</span>
      <span class="tech-pill"><span class="tech-dot" style="background:#888;border:1px solid #555"></span>Express.js</span>
      <span class="tech-pill"><span class="tech-dot" style="background:#47A248"></span>MongoDB</span>
      <span class="tech-pill"><span class="tech-dot" style="background:#F7DF1E"></span>JavaScript</span>
      <span class="tech-pill"><span class="tech-dot" style="background:#3178C6"></span>TypeScript</span>
      <span class="tech-pill"><span class="tech-dot" style="background:#E34F26"></span>HTML5</span>
      <span class="tech-pill"><span class="tech-dot" style="background:#1572B6"></span>CSS3</span>
      <span class="tech-pill"><span class="tech-dot" style="background:#F05032"></span>Git & GitHub</span>
      <span class="tech-pill"><span class="tech-dot" style="background:#CB3837"></span>REST APIs</span>
      <span class="tech-pill"><span class="tech-dot" style="background:#6C63FF"></span>JWT Auth</span>
      <span class="tech-pill"><span class="tech-dot" style="background:#00D4FF"></span>DSA & CP</span>
    </div>

    <!-- Goals -->
    <div class="section-label">Current Goals</div>
    <div class="goals-list">
      <div class="goal-item">
        <span class="goal-name">Master MERN Stack</span>
        <div class="goal-bar-wrap"><div class="goal-bar" data-w="78" style="background:linear-gradient(90deg,#6C63FF,#00D4FF)"></div></div>
        <span class="goal-pct">78%</span>
      </div>
      <div class="goal-item">
        <span class="goal-name">Strengthen DSA</span>
        <div class="goal-bar-wrap"><div class="goal-bar" data-w="55" style="background:linear-gradient(90deg,#00D4FF,#00FF9D)"></div></div>
        <span class="goal-pct">55%</span>
      </div>
      <div class="goal-item">
        <span class="goal-name">System Design</span>
        <div class="goal-bar-wrap"><div class="goal-bar" data-w="35" style="background:linear-gradient(90deg,#00FF9D,#ffb74d)"></div></div>
        <span class="goal-pct">35%</span>
      </div>
      <div class="goal-item">
        <span class="goal-name">Production Apps</span>
        <div class="goal-bar-wrap"><div class="goal-bar" data-w="62" style="background:linear-gradient(90deg,#ffb74d,#ff7043)"></div></div>
        <span class="goal-pct">62%</span>
      </div>
    </div>

    <!-- Stats -->
    <div class="section-label">GitHub Stats</div>
    <div class="stat-row">
      <div class="stat-box"><div class="stat-num" id="commits">0</div><div class="stat-lbl">Commits</div></div>
      <div class="stat-box"><div class="stat-num" id="repos">0</div><div class="stat-lbl">Repos</div></div>
      <div class="stat-box"><div class="stat-num" id="prs">0</div><div class="stat-lbl">Pull Requests</div></div>
    </div>

    <!-- CTA -->
    <div class="cta">
      <p>⭐ Let's build something amazing together</p>
      <div class="connect-btns">
        <a href="https://github.com/" class="cta-btn">🐙 GitHub</a>
        <a href="https://linkedin.com/" class="cta-btn">🔗 LinkedIn</a>
        <a href="mailto:om@example.com" class="cta-btn primary">📬 Contact Me</a>
      </div>
    </div>
  </div>
</div>

<script>
// ── 3D Particle Canvas ──────────────────────────────────────────────
const canvas = document.getElementById('canvas3d');
const ctx = canvas.getContext('2d');

function resize(){
  const wrap = canvas.parentElement;
  canvas.width = wrap.offsetWidth;
  canvas.height = wrap.offsetHeight;
}
resize();
window.addEventListener('resize', resize);

const COLS = ['#6C63FF','#00D4FF','#00FF9D','#ffb74d','#f48fb1'];
const particles = Array.from({length:70},()=>({
  x: Math.random()*680, y: Math.random()*720,
  r: Math.random()*1.6+0.3,
  vx: (Math.random()-0.5)*0.45,
  vy: (Math.random()-0.5)*0.45,
  c: COLS[Math.floor(Math.random()*COLS.length)],
  o: Math.random()*0.5+0.15,
}));

let mouseX=340,mouseY=360;
document.querySelector('.profile-wrap').addEventListener('mousemove',e=>{
  const r=e.currentTarget.getBoundingClientRect();
  mouseX=e.clientX-r.left; mouseY=e.clientY-r.top;
});

function hexAlpha(hex,a){
  const n=parseInt(hex.slice(1),16);
  const r=(n>>16)&255,g=(n>>8)&255,b=n&255;
  return `rgba(${r},${g},${b},${a})`;
}

function draw(){
  ctx.clearRect(0,0,canvas.width,canvas.height);

  // grid
  ctx.lineWidth=0.5;
  for(let x=0;x<canvas.width;x+=44){
    ctx.strokeStyle='rgba(108,99,255,0.05)';
    ctx.beginPath();ctx.moveTo(x,0);ctx.lineTo(x,canvas.height);ctx.stroke();
  }
  for(let y=0;y<canvas.height;y+=44){
    ctx.strokeStyle='rgba(108,99,255,0.05)';
    ctx.beginPath();ctx.moveTo(0,y);ctx.lineTo(canvas.width,y);ctx.stroke();
  }

  // mouse glow
  const grd=ctx.createRadialGradient(mouseX,mouseY,0,mouseX,mouseY,160);
  grd.addColorStop(0,'rgba(108,99,255,0.06)');
  grd.addColorStop(1,'transparent');
  ctx.fillStyle=grd;
  ctx.fillRect(0,0,canvas.width,canvas.height);

  // connections
  for(let i=0;i<particles.length;i++){
    for(let j=i+1;j<particles.length;j++){
      const dx=particles[i].x-particles[j].x,dy=particles[i].y-particles[j].y;
      const d=Math.sqrt(dx*dx+dy*dy);
      if(d<90){
        ctx.strokeStyle=`rgba(108,99,255,${0.15*(1-d/90)})`;
        ctx.lineWidth=0.4;
        ctx.beginPath();ctx.moveTo(particles[i].x,particles[i].y);
        ctx.lineTo(particles[j].x,particles[j].y);ctx.stroke();
      }
    }
  }

  // dots
  particles.forEach(p=>{
    p.x+=p.vx; p.y+=p.vy;
    if(p.x<0)p.x=canvas.width; if(p.x>canvas.width)p.x=0;
    if(p.y<0)p.y=canvas.height; if(p.y>canvas.height)p.y=0;
    ctx.beginPath();ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
    ctx.fillStyle=hexAlpha(p.c,p.o);ctx.fill();
  });

  requestAnimationFrame(draw);
}
draw();

// ── Animate goal bars ───────────────────────────────────────────────
setTimeout(()=>{
  document.querySelectorAll('.goal-bar').forEach(b=>{
    b.style.width=b.dataset.w+'%';
  });
},300);

// ── Count-up stats ──────────────────────────────────────────────────
function countUp(id,target,dur){
  const el=document.getElementById(id);
  let start=0;
  const step=target/(dur/16);
  const t=setInterval(()=>{
    start+=step;
    if(start>=target){el.textContent=target;clearInterval(t);}
    else el.textContent=Math.floor(start);
  },16);
}
setTimeout(()=>{
  countUp('commits',432,1800);
  countUp('repos',18,1200);
  countUp('prs',64,1500);
},500);
</script>
</body>
</html>
