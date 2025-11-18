<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Running Advent Calendar</title>
  <style>
    :root{
      --bg: #0f172a;          /* slate-900 */
      --card: #111827;        /* gray-900  */
      --accent: #22c55e;      /* green-500 */
      --accent-2: #14b8a6;    /* teal-500  */
      --muted: #94a3b8;       /* slate-400 */
      --text: #e5e7eb;        /* gray-200  */
      --danger: #ef4444;      /* red-500   */
      --gold: #f59e0b;        /* amber-500 */
    }
    html, body { height: 100%; }
    body{
      margin:0; font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji", "Segoe UI Emoji";
      background: radial-gradient(1200px 800px at 20% -10%, rgba(34,197,94,.18), transparent 60%),
                  radial-gradient(1200px 800px at 120% 10%, rgba(20,184,166,.18), transparent 60%),
                  var(--bg);
      color: var(--text);
      display:flex; align-items:center; justify-content:center;
      padding: 32px;
    }
    .app{ width: min(1100px, 100%); }
    header{ display:flex; align-items:center; justify-content:space-between; gap:16px; flex-wrap: wrap; margin-bottom: 18px; }
    header h1{ font-size: clamp(1.4rem, 1.2rem + 1.2vw, 2rem); margin:0; letter-spacing: 0.5px; }
    header .sub{ color: var(--muted); font-size: .95rem; }

    .bar{ display:flex; gap:8px; flex-wrap:wrap; }
    .btn{
      background: linear-gradient(135deg, var(--accent), var(--accent-2));
      color: #0b0f19;
      border: 0; padding: 10px 14px; border-radius: 999px; font-weight: 700; cursor:pointer;
      box-shadow: 0 8px 16px rgba(0,0,0,.25), inset 0 1px 0 rgba(255,255,255,.35);
      transition: transform .06s ease;
    }
    .btn.secondary{ background: #1f2937; color: var(--text); box-shadow: inset 0 1px 0 rgba(255,255,255,.06); }
    .btn.danger{ background: var(--danger); color: white; }
    .btn:active{ transform: translateY(1px) scale(.99); }

    .grid{
      display:grid; grid-template-columns: repeat(6, 1fr); gap: 12px; 
      background: rgba(255,255,255,.05); border-radius: 16px; padding: 14px; 
      box-shadow: inset 0 1px 0 rgba(255,255,255,.05), 0 8px 24px rgba(0,0,0,.35);
    }

    .door{
      position:relative; aspect-ratio: 1 / 1; perspective: 900px; border-radius: 16px; overflow: hidden; 
      user-select:none; -webkit-tap-highlight-color: transparent;
    }
    .door .front, .door .back{
      position:absolute; inset:0; display:flex; align-items:center; justify-content:center;
      border-radius: 16px; font-weight: 900; font-size: clamp(1.4rem, 1rem + 1.2vw, 2rem);
      transition: transform .7s cubic-bezier(.2,.8,.2,1);
      backface-visibility: hidden;
    }
    .front{
      background: linear-gradient(160deg, #1f2937, #0b1220);
      border: 1px solid rgba(255,255,255,.06);
      color: #cbd5e1;
    }
    .front .badge{ position:absolute; top:8px; left:8px; font-size:.7rem; background: rgba(245,158,11,.15); color: #fde68a; padding:4px 8px; border-radius:999px; border:1px solid rgba(245,158,11,.35); }
    .front.locked{ filter: grayscale(0.4) brightness(0.75); }

    .back{
      transform: rotateY(180deg);
      background: linear-gradient(160deg, #052e1f, #032016);
      border: 1px solid rgba(34,197,94,.35);
      color: #bbf7d0;
      padding: 10px;
      text-align:center;
    }
    .door.open .front{ transform: rotateY(180deg); }
    .door.open .back{ transform: rotateY(360deg); }

    .km{ font-size: clamp(1.8rem, 1.2rem + 2vw, 2.8rem); display:block; }
    .km small{ font-weight:700; font-size: .8rem; color:#86efac; letter-spacing: .1em; }
    .hint{ color: var(--muted); margin-top: 8px; font-size: .9rem; }

    footer{ margin-top: 18px; color: var(--muted); font-size: .9rem; display:flex; align-items:center; justify-content:space-between; gap:12px; flex-wrap:wrap; }
    code.inline{ background: rgba(255,255,255,.08); padding: 2px 6px; border-radius: 6px; }

    @media (max-width: 700px){
      .grid{ grid-template-columns: repeat(4, 1fr); }
    }
  </style>
</head>
<body>
  <div class="app">
    <header>
      <div>
        <h1>Running Advent Calendar</h1>
        <div class="sub">Open one door per day from <strong>December 1–24</strong>. The distance equals the day number: <strong>1 km</strong> on Dec 1 … <strong>24 km</strong> on Dec 24.</div>
      </div>
      <div class="bar">
        <button class="btn secondary" id="exportBtn" title="Copy your 1–24 order to clipboard">Export order</button>
        <button class="btn secondary" id="logBtn" title="Copy your run log to clipboard">Export log</button>
        <button class="btn danger" id="resetBtn" title="Reset everything (order + progress)">Reset</button>
      </div>
    </header>

    <div id="calendar" class="grid" aria-live="polite"></div>

    <footer>
      <div>
        <span id="status"></span>
        <div class="hint">Tip: add <code class="inline">?debug=1</code> to the URL to open any door for testing.</div>
      </div>
      <div id="todayMsg"></div>
    </footer>
  </div>

  <script>
    (function(){
      const qs = new URLSearchParams(location.search);
      const DEBUG = qs.get('debug') === '1';

      // Use the December of the viewer's current year
      const now = new Date();
      const year = now.getFullYear();
      const IS_DECEMBER = now.getMonth() === 11; // 0-indexed months
      const TODAY = now.getDate();

      const KEY = `runAdvent:${year}`; // namespaced per-year
      const calendarEl = document.getElementById('calendar');
      const statusEl = document.getElementById('status');
      const todayMsg = document.getElementById('todayMsg');

      const state = loadOrInit();
      render();
      updateStatus();

      // --- UI buttons ---
      document.getElementById('resetBtn').onclick = () => {
        if(confirm('Reset order and progress for ' + year + '?')){
          localStorage.removeItem(KEY);
          location.reload();
        }
      };

      document.getElementById('exportBtn').onclick = () => {
        const order = state.order.join(',');
        navigator.clipboard.writeText(order).then(() => toast('Order copied to clipboard.'));
      };

      document.getElementById('logBtn').onclick = () => {
        const lines = [];
        for(let d=1; d<=24; d++){
          const km = state.order[d-1];
          const opened = !!state.opened[d];
          lines.push(`Dec ${String(d).padStart(2,'0')}: ${km} km${opened ? ' ✅' : ''}`);
        }
        const txt = lines.join('\n');
        navigator.clipboard.writeText(txt).then(() => toast('Run log copied to clipboard.'));
      };

      function toast(msg){
        statusEl.textContent = msg;
        setTimeout(()=>{ statusEl.textContent=''; }, 3000);
      }

      function loadOrInit(){
        const raw = localStorage.getItem(KEY);
        if(raw){
          try{ return JSON.parse(raw); }catch(e){}
        }
        const order = [...Array(24)].map((_,i)=> i+1);
        const opened = {};
        const s = { year, order, opened };
        localStorage.setItem(KEY, JSON.stringify(s));
        return s;
      }

      function save(){ localStorage.setItem(KEY, JSON.stringify(state)); }

      function shuffle(arr){
        // Fisher–Yates
        for(let i=arr.length-1; i>0; i--){
          const j = Math.floor(Math.random() * (i+1));
          [arr[i], arr[j]] = [arr[j], arr[i]];
        }
        return arr;
      }

      function canOpen(day){
        if(DEBUG) return true;
        if(!IS_DECEMBER) return false;
        if(day < 1 || day > 24) return false;
        return TODAY >= day; // gate by today within December
      }

      function render(){
        calendarEl.innerHTML = '';
        for(let day=1; day<=24; day++){
          const km = state.order[day-1];
          const opened = !!state.opened[day];
          const door = document.createElement('button');
          door.className = 'door' + (opened ? ' open' : '');
          door.setAttribute('aria-label', `Day ${day}${opened ? `: ${km} kilometers revealed` : ''}`);
          door.title = opened ? `Revealed: ${km} km` : (canOpen(day) ? 'Click to open' : 'Locked until its day');

          const front = document.createElement('div');
          front.className = 'front' + (canOpen(day) ? '' : ' locked');
          front.innerHTML = `<div class="badge">${day}</div>Open`; 

          const back = document.createElement('div');
          back.className = 'back';
          back.innerHTML = `<div class="km"><span>${km}</span> <small>km</small></div>`;

          door.appendChild(front); door.appendChild(back);

          door.addEventListener('click', () => {
            if(!canOpen(day)){
              toast('Not yet! Doors unlock on their day in December' + (DEBUG ? ' (debug override is ON)' : ''));
              return;
            }
            if(!opened){
              state.opened[day] = true; save();
              door.classList.add('open');
              toast(`Day ${day}: ${km} km`);
              announceToday(day, km);
            }else{
              toast(`Already opened: Day ${day} • ${km} km`);
            }
          });

          calendarEl.appendChild(door);
        }

        // Show today's message if applicable
        if(IS_DECEMBER && TODAY >= 1 && TODAY <= 24){
          const kmToday = state.order[TODAY-1];
          const done = !!state.opened[TODAY];
          todayMsg.innerHTML = done 
            ? `✅ <strong>Today (${formatDate(year, 11, TODAY)})</strong>: Completed <strong>${kmToday} km</strong>.`
            : `🎯 <strong>Today (${formatDate(year, 11, TODAY)})</strong>: Run <strong>${kmToday} km</strong>.`;
        } else {
          todayMsg.textContent = '';
        }
      }

      function updateStatus(){
        const openedCount = Object.keys(state.opened).length;
        const remaining = 24 - openedCount;
        statusEl.textContent = `Opened ${openedCount}/24 • Remaining ${remaining}` + (DEBUG ? ' • DEBUG MODE' : '');
      }

      function announceToday(day, km){
        if(day === TODAY && IS_DECEMBER){
          todayMsg.innerHTML = `✅ <strong>Today (${formatDate(year, 11, TODAY)})</strong>: Completed <strong>${km} km</strong>.`;
        }
        updateStatus();
      }

      function formatDate(y, m, d){
        // m is 0-indexed
        const dt = new Date(y, m, d);
        return dt.toLocaleDateString(undefined, { year:'numeric', month:'short', day:'numeric' });
      }
    })();
  </script>
</body>
</html>
