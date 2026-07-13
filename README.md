<!DOCTYPE html>
<html>
<head>
<meta charset='UTF-8'><meta name='viewport' content='width=device-width,initial-scale=1'>
<title>Raksha Bandhan Surprise 💖</title>
<style>
body{margin:0;font-family:cursive;background:linear-gradient(#ffd6e7,#ffeaf4);overflow:hidden;text-align:center}
h1{color:#ff1493} button{padding:14px 22px;border:0;border-radius:30px;font-size:18px;cursor:pointer}
#gift{background:#ff69b4;color:#fff} #award{background:#ffb6c1} #ghost{background:#000;color:#fff}
.heart{position:fixed;font-size:22px;animation:f 6s linear infinite}
@keyframes f{from{transform:translateY(100vh)}to{transform:translateY(-10vh)}}
#msg,#awardMsg,#ghostMsg{display:none;background:#fff;padding:15px;margin:15px;border-radius:20px}
.cell{width:80px;height:80px;font-size:40px}
</style>
</head>
<body>
<h1>Happy Raksha Bandhan 💖</h1>
<div id='hearts'></div><br>
<button id='gift'>🎁 Click Me</button>
<div id='msg'>
<h2>💞</h2>
<p><b>My dearest sister,</b> I may not have solutions to all your problems, but I promise you'll never face them alone. No matter what happens, I'll always stand beside you, protect you at any cost, and annoy you forever 😜. Thank you for being the best sister in the world! 🫶</p>
<button onclick='window.open(`https://youtube.com/shorts/CUe1aWV0QVo?si=q-D1MlpDUjXFS-w5`)'>🎵 Play Our Song</button>
</div><br>
<button id='award'>🏆 Click Me</button>
<div id='awardMsg'><h2>🎊🎊</h2><h3>And the Best Sister Award goes to YOU! 👑💕</h3></div><br>
<h2>Tic Tac Toe 🎮</h2>
<div id='board'></div><p id='status'></p><br>
<button id='ghost'>☠️ Click Me</button>
<div id='ghostMsg'><h2>👻🧟‍♀️💀</h2><p><b>Even if I die and become a ghost, I'll still come back to protect you! 😂❤️</b></p></div>
<script>
for(let i=0;i<30;i++){let h=document.createElement('div');h.className='heart';h.innerHTML=['💖','💕','💗','💘','🥰'][Math.floor(Math.random()*5)];h.style.left=Math.random()*100+'vw';h.style.animationDuration=3+Math.random()*4+'s';document.body.appendChild(h);}
gift.onclick=()=>{for(let i=0;i<20;i++){let h=document.createElement('div');h.className='heart';h.innerHTML='💖';h.style.left=Math.random()*100+'vw';h.style.animationDuration='2s';document.body.appendChild(h);}msg.style.display='block';};
let tries=0;award.onclick=()=>{tries++; if(tries<=5){award.style.position='absolute';award.style.left=Math.random()*(innerWidth-120)+'px';award.style.top=Math.random()*(innerHeight-80)+'px';} else awardMsg.style.display='block';};
ghost.onclick=()=>ghostMsg.style.display='block';
const b=document.getElementById('board'); let cells=Array(9).fill(''); 
for(let i=0;i<9;i++){let bt=document.createElement('button');bt.className='cell';bt.onclick=()=>move(i,bt);b.appendChild(bt);}
function move(i,bt){if(cells[i])return; cells[i]='X'; bt.innerText='X'; if(win('X'))return end('You Win! 💖'); let e=cells.findIndex(x=>!x); if(e!=-1){cells[e]='O'; b.children[e].innerText='O';} if(win('X'))end('You Win! 💖');}
function win(p){return [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]].some(a=>a.every(i=>cells[i]==p));}
function end(t){status.innerText=t; for(let c of b.children)c.disabled=true;}
</script>
</body>
</html>
