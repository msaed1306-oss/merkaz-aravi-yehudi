[index (1).html](https://github.com/user-attachments/files/22769723/index.1.html)
<!doctype html>
<html lang="ar" dir="rtl">
<head><meta charset="utf-8"><meta name="viewport" content="width=device-width, initial-scale=1">
<title>Flipbook – Fullscreen</title>

<style>
  :root {
    --bg: #f7f5ff;
    --ink: #1f2328;
    --muted: #606174;
    --accent: #d8cffc;
  }
  * { box-sizing: border-box; }
  html, body { height: 100%; margin:0; }
  body {
    font-family: system-ui, -apple-system, "Segoe UI", Roboto, Arial, "Noto Sans", sans-serif;
    background: var(--bg); color: var(--ink);
  }
  .toolbar {
    position: sticky; top:0; z-index: 10;
    display:flex; align-items:center; justify-content: space-between;
    gap: 12px; padding: 10px 12px; background:#ffffffc7; backdrop-filter: saturate(1.1) blur(6px);
    border-bottom: 1px solid #eee;
  }
  .toolbar .btn {
    padding: 8px 12px; border:1px solid #e6e6ef; border-radius: 10px; background: white;
    cursor: pointer; font-size: 0.95rem;
  }
  .wrap {
    height: calc(100% - 56px);
    display:flex; align-items:center; justify-content:center;
    padding: clamp(6px, 2vw, 16px);
  }
  .book {
    position: relative;
    width: min(95vw, 920px);
    aspect-ratio: 1/1.414;
    background: white;
    box-shadow: 0 10px 25px rgba(0,0,0,.08), 0 1px 0 rgba(0,0,0,.06);
    border-radius: 12px; overflow: hidden;
    border: 1px solid #e9e9f3;
  }
  .page {
    position:absolute; inset:0;
    background: #fff center/contain no-repeat;
    transform-origin: left center;
  }
  .page img { width:100%; height:100%; object-fit: contain; display:block; }
  .hidden { display:none; }
  @keyframes inRight { 0% { transform: perspective(1200px) rotateY(-80deg); box-shadow: 0 0 0 rgba(0,0,0,0);} 100% { transform: perspective(1200px) rotateY(0deg); box-shadow: 0 10px 25px rgba(0,0,0,.08);} }
  @keyframes outLeft { 0% { transform: perspective(1200px) rotateY(0deg); } 100% { transform: perspective(1200px) rotateY(80deg); filter: brightness(.95); } }
  @keyframes inLeft { 0% { transform: perspective(1200px) rotateY(80deg); } 100% { transform: perspective(1200px) rotateY(0deg); } }
  @keyframes outRight { 0% { transform: perspective(1200px) rotateY(0deg); } 100% { transform: perspective(1200px) rotateY(-80deg); filter: brightness(.95); } }
  .flip-in-right { animation: inRight .45s ease both; }
  .flip-out-left { animation: outLeft .45s ease both; }
  .flip-in-left { animation: inLeft .45s ease both; }
  .flip-out-right { animation: outRight .45s ease both; }
  .counter { color: var(--muted); font-variant-numeric: tabular-nums; }
  .brand { font-weight: 600; }
  .fs .toolbar { display:none; }
  .fs .wrap { height: 100%; padding: 0; }
  .hint { color: var(--muted); font-size:.9rem; }
</style>

</head>
<body class="fs">
<div class="wrap">
  <div class="book">
    <div class="page"><img src="pages/page_001.jpg" alt="Page 1"></div><div class="page"><img src="pages/page_002.jpg" alt="Page 2"></div><div class="page"><img src="pages/page_003.jpg" alt="Page 3"></div><div class="page"><img src="pages/page_004.jpg" alt="Page 4"></div><div class="page"><img src="pages/page_005.jpg" alt="Page 5"></div><div class="page"><img src="pages/page_006.jpg" alt="Page 6"></div><div class="page"><img src="pages/page_007.jpg" alt="Page 7"></div><div class="page"><img src="pages/page_008.jpg" alt="Page 8"></div><div class="page"><img src="pages/page_009.jpg" alt="Page 9"></div><div class="page"><img src="pages/page_010.jpg" alt="Page 10"></div><div class="page"><img src="pages/page_011.jpg" alt="Page 11"></div><div class="page"><img src="pages/page_012.jpg" alt="Page 12"></div><div class="page"><img src="pages/page_013.jpg" alt="Page 13"></div><div class="page"><img src="pages/page_014.jpg" alt="Page 14"></div><div class="page"><img src="pages/page_015.jpg" alt="Page 15"></div><div class="page"><img src="pages/page_016.jpg" alt="Page 16"></div><div class="page"><img src="pages/page_017.jpg" alt="Page 17"></div><div class="page"><img src="pages/page_018.jpg" alt="Page 18"></div><div class="page"><img src="pages/page_019.jpg" alt="Page 19"></div><div class="page"><img src="pages/page_020.jpg" alt="Page 20"></div><div class="page"><img src="pages/page_021.jpg" alt="Page 21"></div><div class="page"><img src="pages/page_022.jpg" alt="Page 22"></div><div class="page"><img src="pages/page_023.jpg" alt="Page 23"></div><div class="page"><img src="pages/page_024.jpg" alt="Page 24"></div><div class="page"><img src="pages/page_025.jpg" alt="Page 25"></div><div class="page"><img src="pages/page_026.jpg" alt="Page 26"></div><div class="page"><img src="pages/page_027.jpg" alt="Page 27"></div>
  </div>
</div>

<script>
(function(){
  let cur = 0;
  const pages = Array.from(document.querySelectorAll('.page'));
  const counter = document.getElementById('counter');
  const total = pages.length;
  function updateCounter(){
    if (counter) counter.textContent = (cur+1) + ' / ' + total;
  }
  function show(i, dir=1){
    if (i < 0 || i >= total || i === cur) return;
    const curEl = pages[cur];
    const nextEl = pages[i];
    nextEl.classList.remove('hidden','flip-in-left','flip-in-right','flip-out-left','flip-out-right');
    curEl.classList.remove('hidden','flip-in-left','flip-in-right','flip-out-left','flip-out-right');
    if (dir > 0) { nextEl.classList.add('flip-in-right'); curEl.classList.add('flip-out-left'); }
    else { nextEl.classList.add('flip-in-left'); curEl.classList.add('flip-out-right'); }
    nextEl.style.zIndex = 2; curEl.style.zIndex = 1;
    nextEl.addEventListener('animationend', function handler(){
      nextEl.removeEventListener('animationend', handler);
      pages.forEach(p=>{ p.classList.add('hidden'); p.style.zIndex='1'; });
      nextEl.classList.remove('flip-in-left','flip-in-right','flip-out-left','flip-out-right','hidden');
      cur = i; pages[cur].classList.remove('hidden'); updateCounter();
    });
  }
  function next(){ show(cur+1, +1); }
  function prev(){ show(cur-1, -1); }
  pages.forEach((p,k)=>{ if (k!==0) p.classList.add('hidden'); });
  updateCounter();
  const btnNext = document.getElementById('next');
  const btnPrev = document.getElementById('prev');
  if (btnNext) btnNext.addEventListener('click', next);
  if (btnPrev) btnPrev.addEventListener('click', prev);
  document.addEventListener('keydown', (e)=>{
    if (e.key==='ArrowRight' || e.key==='PageDown') next();
    if (e.key==='ArrowLeft' || e.key==='PageUp') prev();
  });
  let sx=0, sy=0, dx=0, dy=0, touching=false;
  window.addEventListener('touchstart', (e)=>{ touching=true; sx=e.touches[0].clientX; sy=e.touches[0].clientY; },{passive:true});
  window.addEventListener('touchmove', (e)=>{ if(!touching) return; dx=e.touches[0].clientX-sx; dy=e.touches[0].clientY-sy; },{passive:true});
  window.addEventListener('touchend', ()=>{ touching=false; if (Math.abs(dx) > 40 && Math.abs(dx) > Math.abs(dy)) { if (dx < 0) next(); else prev(); } dx=dy=0; });
})();
</script>

</body>
</html>
