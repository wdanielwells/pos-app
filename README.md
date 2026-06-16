<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="POS">
<meta name="theme-color" content="#0F1A0F">
<title>Personal Operating System</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:wght@300;400;500;600&family=DM+Mono:wght@400;500&display=swap');
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
:root{
  --bg:#0F1A0F;--bg2:#162016;--bg3:#1E2A1E;--bd:#2A3A2A;
  --green:#4ADE80;--green2:#22863A;--greenlt:rgba(74,222,128,.12);
  --tx:#E8F0E8;--tx2:#8FA88F;--tx3:#4A5E4A;
  --warn:#FBBF24;--red:#F87171;--gold:#F59E0B;--goldlt:rgba(245,158,11,.12);
  --blue:#60A5FA;
  --ff:'DM Sans',sans-serif;--fm:'DM Mono',monospace;--fd:'DM Serif Display',serif;
}
html,body{height:100%;background:var(--bg);color:var(--tx);font-family:var(--ff);font-size:16px;overflow:hidden;}
#wrap{display:flex;flex-direction:column;height:100vh;height:100dvh;}
#topbar{flex-shrink:0;background:var(--bg);border-bottom:1px solid var(--bd);padding:12px 18px;display:flex;align-items:center;justify-content:space-between;z-index:10;}
.logo{font-family:var(--fd);font-size:1.2rem;color:var(--green);}
.datechip{font-family:var(--fm);font-size:.65rem;color:var(--tx2);}
#content{flex:1;overflow-y:auto;-webkit-overflow-scrolling:touch;padding:20px 18px 24px;}
#bottomnav{flex-shrink:0;background:var(--bg2);border-top:1px solid var(--bd);display:flex;}
.tab{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:3px;padding:10px 4px 8px;background:none;border:none;color:var(--tx3);font-family:var(--fm);font-size:.54rem;letter-spacing:.06em;text-transform:uppercase;cursor:pointer;}
.tab svg{width:22px;height:22px;stroke:currentColor;fill:none;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round;}
.tab.on{color:var(--green);}
.screen{display:none;}
.screen.on{display:block;}
h1{font-family:var(--fd);font-size:1.8rem;margin-bottom:4px;}
.sub{font-family:var(--fm);font-size:.65rem;color:var(--tx2);letter-spacing:.08em;margin-bottom:22px;}
.sh{font-family:var(--fm);font-size:.6rem;letter-spacing:.12em;text-transform:uppercase;color:var(--tx3);border-bottom:1px solid var(--bd);padding-bottom:5px;margin:20px 0 12px;}
.card{background:var(--bg2);border:1px solid var(--bd);border-radius:12px;padding:16px;margin-bottom:12px;}
.card2{background:var(--bg3);border:1px solid var(--bd);border-radius:8px;padding:12px 14px;margin-bottom:8px;}
.btn{width:100%;padding:15px;background:var(--green);border:none;border-radius:12px;font-family:var(--fm);font-size:.8rem;font-weight:500;color:var(--bg);cursor:pointer;letter-spacing:.08em;}
.btn:active{opacity:.85;}
.btn.ghost{background:var(--bg3);color:var(--tx2);border:1px solid var(--bd);}
.inp{width:100%;background:var(--bg3);border:1px solid var(--bd);border-radius:8px;padding:11px 13px;color:var(--tx);font-family:var(--ff);font-size:.9rem;outline:none;margin-bottom:12px;}
.inp:focus{border-color:var(--green2);}
textarea.inp{resize:none;min-height:80px;line-height:1.5;}
label.lbl{font-size:.78rem;color:var(--tx2);margin-bottom:5px;display:block;}

/* HOME */
.hero{background:var(--greenlt);border:1px solid var(--green2);border-radius:14px;padding:20px;margin-bottom:18px;display:flex;align-items:center;justify-content:space-between;}
.heronum{font-family:var(--fd);font-size:3.2rem;color:var(--green);line-height:1;}
.herolbl{font-family:var(--fm);font-size:.6rem;color:var(--green2);letter-spacing:.1em;text-transform:uppercase;margin-top:2px;}
.heromsg{font-size:.8rem;color:var(--tx2);max-width:150px;text-align:right;line-height:1.4;}
.stats3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;margin-bottom:16px;}
.statbox{background:var(--bg2);border:1px solid var(--bd);border-radius:10px;padding:12px 8px;text-align:center;}
.statnum{font-family:var(--fm);font-size:1rem;font-weight:500;}
.statlbl{font-size:.65rem;color:var(--tx2);margin-top:2px;}
.bigbtn{background:var(--green);border-radius:12px;padding:15px 18px;display:flex;align-items:center;justify-content:space-between;cursor:pointer;border:none;width:100%;margin-bottom:10px;}
.bigbtn .bt{text-align:left;}
.bigbtn .btitle{font-weight:600;font-size:.95rem;color:var(--bg);}
.bigbtn .bsub{font-size:.75rem;color:var(--green2);margin-top:2px;}
.bigbtn .barrow{font-size:1.4rem;color:var(--bg);}
.bigbtn.outline{background:var(--bg2);border:1px solid var(--green2);}
.bigbtn.outline .btitle{color:var(--green);}
.bigbtn.outline .bsub{color:var(--tx2);}
.bigbtn.outline .barrow{color:var(--green);}
.aibx{background:var(--bg2);border:1px solid var(--green2);border-radius:12px;padding:16px;margin-bottom:12px;}
.aihead{display:flex;align-items:center;gap:7px;margin-bottom:10px;}
.aidot{width:7px;height:7px;border-radius:50%;background:var(--green);animation:pulse 2s infinite;}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:.3}}
.ailbl{font-family:var(--fm);font-size:.62rem;letter-spacing:.1em;color:var(--green);text-transform:uppercase;}
.aibody{font-size:.85rem;line-height:1.65;color:var(--tx2);white-space:pre-wrap;}
.dim{font-style:italic;color:var(--tx3);}

/* CHECK-IN */
.dimrow{background:var(--bg2);border:1px solid var(--bd);border-radius:10px;padding:12px 14px;margin-bottom:10px;}
.dimlbl{font-size:.82rem;font-weight:500;margin-bottom:8px;display:flex;justify-content:space-between;}
.dimval{font-family:var(--fm);font-size:.78rem;color:var(--green);}
.pips{display:flex;gap:3px;}
.pip{flex:1;height:30px;border-radius:4px;border:1px solid var(--bd);background:var(--bg3);font-family:var(--fm);font-size:.68rem;color:var(--tx3);cursor:pointer;display:flex;align-items:center;justify-content:center;transition:all .1s;}
.pip.lo{background:#7f1d1d;border-color:var(--red);color:#fca5a5;}
.pip.md{background:#78350f;border-color:var(--warn);color:#fde68a;}
.pip.hi{background:#14532d;border-color:var(--green);color:var(--green);}
.sobrow{display:flex;gap:8px;margin-top:4px;}
.sobopt{flex:1;padding:10px;border-radius:8px;border:1px solid var(--bd);background:var(--bg3);font-family:var(--fm);font-size:.7rem;color:var(--tx2);cursor:pointer;text-align:center;transition:all .15s;}
.sobopt.yes{background:#14532d;border-color:var(--green);color:var(--green);}
.sobopt.no{background:#7f1d1d;border-color:var(--red);color:var(--red);}

/* WORKOUT */
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:14px;}
.tile{background:var(--bg2);border:1.5px solid var(--bd);border-radius:12px;padding:14px 10px;text-align:center;cursor:pointer;transition:all .15s;}
.tile.on{border-color:var(--green);background:var(--greenlt);}
.tileico{font-size:1.6rem;margin-bottom:5px;}
.tilelbl{font-size:.8rem;font-weight:600;}
.tile.on .tilelbl{color:var(--green);}
.tilesub{font-size:.68rem;color:var(--tx2);margin-top:2px;}
.durrow{display:flex;gap:6px;margin-bottom:14px;}
.duropt{flex:1;padding:9px 4px;border:1px solid var(--bd);border-radius:8px;background:var(--bg3);font-family:var(--fm);font-size:.7rem;color:var(--tx2);text-align:center;cursor:pointer;transition:all .15s;}
.duropt.on{border-color:var(--green);background:var(--greenlt);color:var(--green);}
.erow{display:flex;gap:4px;margin-bottom:18px;}
.epip{flex:1;height:34px;border-radius:6px;border:1px solid var(--bd);background:var(--bg3);font-family:var(--fm);font-size:.7rem;color:var(--tx3);display:flex;align-items:center;justify-content:center;cursor:pointer;transition:all .1s;}
.epip.lo{background:#3d1515;border-color:var(--red);color:var(--red);}
.epip.md{background:#3d2e10;border-color:var(--gold);color:var(--gold);}
.epip.hi{background:#0f3020;border-color:var(--green);color:var(--green);}
.wkhdr{background:var(--greenlt);border:1px solid var(--green2);border-radius:12px;padding:14px 16px;margin-bottom:14px;}
.wkbar{height:4px;background:var(--bd);border-radius:2px;margin-top:8px;}
.wkfill{height:100%;border-radius:2px;background:var(--green);transition:width .4s;}
.excard{border:1px solid var(--bd);border-radius:10px;overflow:hidden;margin-bottom:10px;}
.excard.cur{border-color:var(--green2);}
.excard.done{opacity:.6;}
.exhdr{padding:12px 14px;background:var(--bg2);display:flex;align-items:center;justify-content:space-between;cursor:pointer;}
.exnum{font-family:var(--fm);font-size:.6rem;color:var(--tx3);letter-spacing:.1em;}
.exname{font-size:.9rem;font-weight:600;margin-top:2px;}
.extgt{font-size:.72rem;color:var(--tx2);margin-top:2px;}
.exchk{width:24px;height:24px;border-radius:50%;border:1.5px solid var(--bd);display:flex;align-items:center;justify-content:center;font-size:.8rem;flex-shrink:0;}
.exchk.done{background:var(--green);border-color:var(--green);}
.exbody{padding:12px 14px;background:var(--bg3);display:none;}
.excard.cur .exbody{display:block;}
.setrow{display:grid;grid-template-columns:24px 1fr 1fr 32px;gap:6px;align-items:center;margin-bottom:6px;}
.setlbl{font-family:var(--fm);font-size:.65rem;color:var(--tx3);text-align:center;}
.setinp{background:var(--bg2);border:1px solid var(--bd);border-radius:6px;padding:8px;color:var(--tx);font-family:var(--fm);font-size:.85rem;outline:none;text-align:center;width:100%;}
.setinp:focus{border-color:var(--green2);}
.setinp.pr{border-color:var(--gold);color:var(--gold);}
.setbtn{width:28px;height:28px;border-radius:50%;border:1.5px solid var(--bd);background:var(--bg);color:var(--tx3);font-size:.75rem;cursor:pointer;display:flex;align-items:center;justify-content:center;}
.setbtn.done{background:var(--green);border-color:var(--green);color:var(--bg);}
.restbar{background:var(--bg2);border:1px solid var(--bd);border-radius:8px;padding:8px 12px;display:flex;align-items:center;justify-content:space-between;margin-bottom:10px;}
.restlbl{font-family:var(--fm);font-size:.65rem;color:var(--tx2);}
.restbtns{display:flex;gap:5px;}
.restbtn{font-family:var(--fm);font-size:.65rem;padding:4px 9px;border-radius:5px;border:1px solid var(--bd);background:var(--bg3);color:var(--tx2);cursor:pointer;}
.nextbtn{width:100%;padding:11px;background:var(--bg);border:1px solid var(--green2);border-radius:9px;color:var(--green);font-family:var(--fm);font-size:.72rem;cursor:pointer;letter-spacing:.06em;}
.addsetbtn{width:100%;padding:7px;background:transparent;border:1px dashed var(--bd);border-radius:7px;color:var(--tx2);font-family:var(--fm);font-size:.7rem;cursor:pointer;margin-bottom:10px;}
.prbadge{background:var(--goldlt);border:1px solid var(--gold);border-radius:7px;padding:7px 11px;margin-bottom:10px;display:none;font-family:var(--fm);font-size:.7rem;color:var(--gold);}
.prbadge.show{display:block;}
.backupbar{background:rgba(96,165,250,.1);border:1px solid var(--blue);border-radius:9px;padding:9px 12px;margin-bottom:12px;display:flex;align-items:center;gap:9px;cursor:pointer;}
.backuptxt{font-size:.78rem;color:var(--blue);flex:1;}

/* TRACKERS */
.trcard{background:var(--bg2);border:1px solid var(--bd);border-radius:12px;padding:14px;margin-bottom:10px;}
.trtop{display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:9px;}
.trname{font-weight:600;font-size:.9rem;}
.trsrk{font-family:var(--fm);font-size:.7rem;color:var(--green);}
.trchips{display:flex;gap:5px;flex-wrap:wrap;}
.dchip{width:27px;height:27px;border-radius:6px;border:1px solid var(--bd);background:var(--bg3);font-family:var(--fm);font-size:.6rem;color:var(--tx3);display:flex;align-items:center;justify-content:center;cursor:pointer;transition:all .1s;}
.dchip.done{background:var(--greenlt);border-color:var(--green2);color:var(--green);}
.addbtn{width:100%;padding:13px;background:transparent;border:1px dashed var(--bd);border-radius:12px;color:var(--tx2);font-family:var(--ff);font-size:.85rem;cursor:pointer;}

/* HISTORY */
.hentry{background:var(--bg2);border:1px solid var(--bd);border-radius:10px;padding:13px;margin-bottom:9px;}
.htop{display:flex;justify-content:space-between;margin-bottom:7px;}
.hdate{font-family:var(--fm);font-size:.7rem;color:var(--tx2);}
.hscore{font-family:var(--fm);font-size:.88rem;color:var(--green);font-weight:500;}
.hdims{display:flex;flex-wrap:wrap;gap:3px;}
.hdim{font-family:var(--fm);font-size:.6rem;padding:2px 5px;border-radius:4px;}
.dg{background:var(--greenlt);color:var(--green);}
.dy{background:rgba(251,191,36,.12);color:var(--warn);}
.dr{background:rgba(248,113,113,.12);color:var(--red);}

/* PROFILE */
.profhdr{display:flex;align-items:center;gap:12px;margin-bottom:20px;}
.avatar{width:52px;height:52px;border-radius:50%;background:var(--greenlt);border:2px solid var(--green2);display:flex;align-items:center;justify-content:center;font-family:var(--fd);font-size:1.3rem;color:var(--green);flex-shrink:0;}
.profname{font-family:var(--fd);font-size:1.25rem;}
.profday{font-family:var(--fm);font-size:.65rem;color:var(--tx2);margin-top:2px;}
.gbar{height:6px;background:var(--bd);border-radius:3px;}
.gbarfill{height:100%;border-radius:3px;background:var(--green);}

/* MODAL */
.moverlay{position:fixed;inset:0;background:rgba(0,0,0,.72);z-index:1000;display:flex;align-items:flex-end;justify-content:center;}
.moverlay.hide{display:none;}
.modal{background:var(--bg2);border:1px solid var(--bd);border-radius:18px 18px 0 0;padding:22px 18px 34px;width:100%;max-width:480px;max-height:85vh;overflow-y:auto;}
.mtitle{font-family:var(--fd);font-size:1.3rem;margin-bottom:4px;}
.msub{font-size:.8rem;color:var(--tx2);margin-bottom:16px;}
.macts{display:flex;gap:9px;margin-top:6px;}
.mbtn{flex:2;padding:12px;background:var(--green);border:none;border-radius:9px;font-family:var(--fm);font-size:.76rem;color:var(--bg);cursor:pointer;font-weight:500;}
.mbtn2{flex:1;padding:12px;background:transparent;border:1px solid var(--bd);border-radius:9px;font-family:var(--fm);font-size:.76rem;color:var(--tx2);cursor:pointer;}
.tgrid{display:grid;grid-template-columns:1fr 1fr;gap:7px;margin-bottom:14px;}
.topt{padding:9px;border:1px solid var(--bd);border-radius:8px;background:var(--bg3);text-align:center;cursor:pointer;font-size:.8rem;color:var(--tx2);transition:all .15s;}
.topt.on{border-color:var(--green2);background:var(--greenlt);color:var(--green);}

/* PR CELEBRATE */
.proverlay{position:fixed;inset:0;z-index:2000;display:flex;align-items:center;justify-content:center;pointer-events:none;}
.proverlay.hide{display:none;}
.prcelebrate{background:var(--bg2);border:2px solid var(--gold);border-radius:18px;padding:26px 30px;text-align:center;transform:scale(0);transition:transform .3s cubic-bezier(.34,1.56,.64,1);}
.prcelebrate.show{transform:scale(1);}
.prhead{font-family:var(--fd);font-size:1.4rem;color:var(--gold);}

/* TOAST */
.toast{position:fixed;top:70px;left:50%;transform:translateX(-50%);background:var(--green);color:var(--bg);font-family:var(--fm);font-size:.72rem;padding:7px 18px;border-radius:20px;z-index:3000;font-weight:500;pointer-events:none;white-space:nowrap;}
.toast.hide{display:none;}
.toast.gold{background:var(--gold);}

/* PROGRESS */
.liftcard{background:var(--bg2);border:1px solid var(--bd);border-radius:10px;overflow:hidden;margin-bottom:9px;}
.lifthdr{padding:11px 14px;display:flex;justify-content:space-between;align-items:center;cursor:pointer;}
.liftbody{padding:0 14px;max-height:0;overflow:hidden;transition:max-height .3s;}
.liftbody.open{max-height:300px;padding-bottom:12px;}
.liftrow{display:flex;align-items:center;gap:8px;padding:4px 0;border-bottom:1px solid var(--bd);font-size:.78rem;}
.liftrow:last-child{border-bottom:none;}

/* FOOTER */
.footer{text-align:center;padding:18px 0 8px;font-family:var(--fm);font-size:.56rem;color:var(--tx3);}
</style>
</head>
<body>
<div id="wrap">

<div id="topbar">
  <div class="logo">POS</div>
  <div class="datechip" id="topdate"></div>
</div>

<div id="content">

  <!-- HOME -->
  <div class="screen on" id="s-home">
    <h1 id="greeting">Good morning.</h1>
    <div class="sub">DAY <span id="daynum">1</span> OF 90</div>
    <div class="hero">
      <div><div class="heronum" id="streaknum">0</div><div class="herolbl">Day Streak</div></div>
      <div class="heromsg" id="streakmsg">Log your first check-in to start your streak.</div>
    </div>
    <div class="stats3">
      <div class="statbox"><div class="statnum" id="sw">—</div><div class="statlbl">Weight</div></div>
      <div class="statbox"><div class="statnum" id="savg">—</div><div class="statlbl">7-Day Avg</div></div>
      <div class="statbox"><div class="statnum" id="scomp">—</div><div class="statlbl">Compliance</div></div>
    </div>
    <button class="bigbtn" onclick="show('checkin')">
      <div class="bt"><div class="btitle">Log Today's Check-In</div><div class="bsub" id="cistatus">Takes under 2 minutes</div></div>
      <div class="barrow">→</div>
    </button>
    <button class="bigbtn outline" onclick="show('workout')">
      <div class="bt"><div class="btitle">🏋️ Start a Workout</div><div class="bsub" id="wktstatus">Build your AI training plan</div></div>
      <div class="barrow">→</div>
    </button>
    <div class="sh">Last AI Insight</div>
    <div class="aibx">
      <div class="aihead"><div class="aidot"></div><span class="ailbl">Your Coach</span></div>
      <div class="aibody dim" id="homeai">Log a check-in to receive your personalized daily plan.</div>
    </div>
    <div class="footer">© 2025 Personal Operating System · All rights reserved.</div>
  </div>

  <!-- CHECK-IN -->
  <div class="screen" id="s-checkin">
    <h1>Daily Check-In</h1>
    <div class="sub" id="cidatelbl"></div>
    <div id="dimgrid"></div>
    <div id="sobsec" style="display:none">
      <div class="sh">Sobriety</div>
      <div class="sobrow">
        <div class="sobopt" id="sobyes" onclick="setSob('yes')">✓ Maintained</div>
        <div class="sobopt" id="sobno" onclick="setSob('no')">✗ Not maintained</div>
      </div>
    </div>
    <div class="sh">Notes for Today</div>
    <textarea class="inp" id="cinotes" placeholder="How did today go? Any context for your scores..."></textarea>
    <button class="btn" id="cibtn" onclick="submitCI()">Get My Daily Plan →</button>
    <div class="footer">© 2025 Personal Operating System · All rights reserved.</div>
  </div>

  <!-- AI RESULT -->
  <div class="screen" id="s-ai">
    <h1>Your Daily Plan</h1>
    <div class="sub" id="aidatelbl"></div>
    <div class="aibx">
      <div class="aihead"><div class="aidot"></div><span class="ailbl">AI Coach · Personalized for You</span></div>
      <div class="aibody dim" id="aiout">Analyzing your check-in...</div>
    </div>
    <button class="btn ghost" onclick="show('home')" style="margin-bottom:10px;">← Back to Home</button>
    <div class="footer">© 2025 Personal Operating System · All rights reserved.</div>
  </div>

  <!-- WORKOUT -->
  <div class="screen" id="s-workout">
    <div id="wv-setup">
      <h1>Train.</h1>
      <div class="sub">BUILD YOUR WORKOUT</div>
      <div class="sh">Equipment</div>
      <div class="grid2">
        <div class="tile on" onclick="selT(this,'gym')"><div class="tileico">🏋️</div><div class="tilelbl">Full Gym</div><div class="tilesub">Barbells, machines</div></div>
        <div class="tile" onclick="selT(this,'dumbbells')"><div class="tileico">💪</div><div class="tilelbl">Dumbbells</div><div class="tilesub">Free weights only</div></div>
        <div class="tile" onclick="selT(this,'home')"><div class="tileico">🏠</div><div class="tilelbl">Home</div><div class="tilesub">Bodyweight + bands</div></div>
        <div class="tile" onclick="selT(this,'bodyweight')"><div class="tileico">🧘</div><div class="tilelbl">Bodyweight</div><div class="tilesub">No equipment</div></div>
      </div>
      <div class="sh">Time Available</div>
      <div class="durrow">
        <div class="duropt" onclick="selD(this,20)">20 min</div>
        <div class="duropt on" onclick="selD(this,45)">45 min</div>
        <div class="duropt" onclick="selD(this,60)">60 min</div>
        <div class="duropt" onclick="selD(this,90)">90 min</div>
      </div>
      <div class="sh">Energy Level</div>
      <div class="erow" id="erow"></div>
      <div class="sh">Focus</div>
      <div class="grid2" id="focusgrid">
        <div class="tile on" onclick="selF(this,'full')"><div class="tileico">⚡</div><div class="tilelbl">Full Body</div><div class="tilesub">Balanced</div></div>
        <div class="tile" onclick="selF(this,'upper')"><div class="tileico">💪</div><div class="tilelbl">Upper Body</div><div class="tilesub">Chest, back, shoulders</div></div>
        <div class="tile" onclick="selF(this,'lower')"><div class="tileico">🦵</div><div class="tilelbl">Lower Body</div><div class="tilesub">Legs, glutes, core</div></div>
        <div class="tile" onclick="selF(this,'cardio')"><div class="tileico">🏃</div><div class="tilelbl">Cardio</div><div class="tilesub">Conditioning</div></div>
      </div>
      <button class="btn" id="genbtn" onclick="genWorkout()">Build My Workout →</button>
      <div class="footer">© 2025 Personal Operating System · All rights reserved.</div>
    </div>
    <div id="wv-active" style="display:none">
      <div class="wkhdr">
        <div style="display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:5px;">
          <div style="font-family:var(--fd);font-size:1.15rem;" id="wktitle">Loading...</div>
          <div style="font-family:var(--fm);font-size:.65rem;color:var(--green);background:var(--bg);border:1px solid var(--green2);border-radius:20px;padding:3px 9px;" id="wkbadge">0/0</div>
        </div>
        <div style="font-family:var(--fm);font-size:.65rem;color:var(--tx2);" id="wksub"></div>
        <div class="wkbar"><div class="wkfill" id="wkprog" style="width:0%"></div></div>
      </div>
      <div class="backupbar" onclick="loadBackup()">
        <span style="font-size:1rem;">⚡</span>
        <div class="backuptxt">Short on time? Switch to <strong>20-min backup</strong></div>
        <span style="font-family:var(--fm);font-size:.7rem;color:var(--blue);">→</span>
      </div>
      <div id="exlist"></div>
      <button class="btn" id="finbtn" onclick="finishWkt()" style="display:none;margin-top:8px;">Finish Workout ✓</button>
      <div class="footer">© 2025 Personal Operating System · All rights reserved.</div>
    </div>
    <div id="wv-summary" style="display:none">
      <h1>Done.</h1>
      <div class="sub" id="wsumsub">WORKOUT COMPLETE</div>
      <div class="card" id="wsumcard"></div>
      <div id="wsumprs"></div>
      <button class="btn" onclick="resetWkt()" style="margin-top:8px;">Train Again →</button>
      <div class="footer">© 2025 Personal Operating System · All rights reserved.</div>
    </div>
  </div>

  <!-- TRACKERS -->
  <div class="screen" id="s-trackers">
    <h1>My Trackers</h1>
    <div class="sub">CUSTOM HABITS & GOALS</div>
    <div id="trlist"></div>
    <button class="addbtn" onclick="openAddTr()">+ Add a New Tracker</button>
    <div class="footer">© 2025 Personal Operating System · All rights reserved.</div>
  </div>

  <!-- HISTORY -->
  <div class="screen" id="s-history">
    <h1>History</h1>
    <div class="sub">YOUR CHECK-IN LOG</div>
    <div id="hlist"></div>
    <div class="footer">© 2025 Personal Operating System · All rights reserved.</div>
  </div>

  <!-- PROFILE -->
  <div class="screen" id="s-profile">
    <h1>My Profile</h1>
    <div class="sub">90-DAY PROGRAM</div>
    <div class="profhdr">
      <div class="avatar" id="pavatar">?</div>
      <div><div class="profname" id="pname">Your Name</div><div class="profday">Day <span id="pdaynum">1</span> of 90</div></div>
    </div>
    <div id="goalbar"></div>
    <div class="sh">Settings</div>
    <div class="card">
      <label class="lbl">Your Name</label>
      <input class="inp" id="sname" placeholder="First name" oninput="saveS()">
      <label class="lbl">Current Weight (lbs)</label>
      <input class="inp" id="sweight" type="number" placeholder="e.g. 240" oninput="saveS()">
      <label class="lbl">Goal Weight (lbs)</label>
      <input class="inp" id="sgoalwt" type="number" placeholder="e.g. 215" oninput="saveS()">
      <label class="lbl" style="display:flex;align-items:center;gap:8px;cursor:pointer;margin-bottom:0;">
        <input type="checkbox" id="ssober" onchange="saveS()" style="accent-color:var(--green);width:16px;height:16px;">
        Enable sobriety tracking
      </label>
    </div>
    <div class="sh">Primary Goals</div>
    <div class="card">
      <textarea class="inp" id="sgoals" placeholder="e.g. Lose 25 lbs, reverse prediabetes, maintain sobriety..." oninput="saveS()" style="margin-bottom:0;min-height:70px;"></textarea>
    </div>
    <div class="footer">© 2025 Personal Operating System · All rights reserved.</div>
  </div>

  <!-- PROGRESS -->
  <div class="screen" id="s-progress">
    <h1>Progress.</h1>
    <div class="sub">LIFT HISTORY & PRs</div>
    <div id="progsec"></div>
    <div class="footer">© 2025 Personal Operating System · All rights reserved.</div>
  </div>

</div><!-- /content -->

<!-- BOTTOM NAV -->
<div id="bottomnav">
  <button class="tab on" id="t-home" onclick="show('home')">
    <svg viewBox="0 0 24 24"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></svg>
    Home
  </button>
  <button class="tab" id="t-checkin" onclick="show('checkin')">
    <svg viewBox="0 0 24 24"><polyline points="9 11 12 14 22 4"/><path d="M21 12v7a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11"/></svg>
    Check-In
  </button>
  <button class="tab" id="t-workout" onclick="show('workout')">
    <svg viewBox="0 0 24 24"><path d="M6 4v16M18 4v16M3 8h4m10 0h4M3 16h4m10 0h4M7 8h10v8H7z"/></svg>
    Train
  </button>
  <button class="tab" id="t-trackers" onclick="show('trackers')">
    <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><circle cx="12" cy="12" r="3"/></svg>
    Track
  </button>
  <button class="tab" id="t-history" onclick="show('history')">
    <svg viewBox="0 0 24 24"><rect x="3" y="4" width="18" height="18" rx="2" ry="2"/><line x1="16" y1="2" x2="16" y2="6"/><line x1="8" y1="2" x2="8" y2="6"/><line x1="3" y1="10" x2="21" y2="10"/></svg>
    History
  </button>
  <button class="tab" id="t-profile" onclick="show('profile')">
    <svg viewBox="0 0 24 24"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
    Me
  </button>
</div>

</div><!-- /wrap -->

<!-- TRACKER MODAL -->
<div class="moverlay hide" id="trmodal" onclick="if(event.target===this)this.classList.add('hide')">
  <div class="modal">
    <div class="mtitle">New Tracker</div>
    <div class="msub">Track anything — sobriety, waist, reading, water, steps, or any habit.</div>
    <label class="lbl">Name</label>
    <input class="inp" id="tname" placeholder="e.g. Daily Reading, Waist Size...">
    <label class="lbl">Type</label>
    <div class="tgrid">
      <div class="topt on" onclick="selTT(this,'yesno')" data-t="yesno">✓ Yes/No<br><small style="font-size:.68rem;opacity:.7;">Did I do it?</small></div>
      <div class="topt" onclick="selTT(this,'number')" data-t="number">123 Number<br><small style="font-size:.68rem;opacity:.7;">Log a value</small></div>
      <div class="topt" onclick="selTT(this,'streak')" data-t="streak">🔥 Streak<br><small style="font-size:.68rem;opacity:.7;">Count days</small></div>
      <div class="topt" onclick="selTT(this,'scale')" data-t="scale">⚡ Scale 1-10<br><small style="font-size:.68rem;opacity:.7;">Rate it</small></div>
    </div>
    <div id="unitwrap" style="display:none">
      <label class="lbl">Unit (optional)</label>
      <input class="inp" id="tunit" placeholder="e.g. lbs, oz, minutes">
    </div>
    <label class="lbl">Emoji Icon</label>
    <input class="inp" id="temoji" placeholder="📖 💪 🧘 💧" maxlength="4">
    <div class="macts">
      <button class="mbtn2" onclick="document.getElementById('trmodal').classList.add('hide')">Cancel</button>
      <button class="mbtn" onclick="addTracker()">Add Tracker</button>
    </div>
  </div>
</div>

<!-- PR OVERLAY -->
<div class="proverlay hide" id="proverlay">
  <div class="prcelebrate" id="prcelebrate">
    <div style="font-size:2.4rem;margin-bottom:8px;">🏆</div>
    <div class="prhead">Personal Record!</div>
    <div style="font-family:var(--fm);font-size:.76rem;color:var(--tx2);margin-top:6px;" id="prdetail"></div>
  </div>
</div>

<!-- TOAST -->
<div class="toast hide" id="toast"></div>

<script>
// ── STORAGE ──────────────────────────────────────────
function gl(k,d){try{const v=localStorage.getItem(k);return v!==null?JSON.parse(v):d;}catch(e){return d;}}
function sl(k,v){try{localStorage.setItem(k,JSON.stringify(v));}catch(e){}}

// ── DATA ─────────────────────────────────────────────
const DIMS=[
  {k:'weight',l:'Weight',e:'⚖️'},{k:'sleep',l:'Sleep',e:'😴'},
  {k:'energy',l:'Energy',e:'⚡'},{k:'mood',l:'Mood',e:'🧠'},
  {k:'stress',l:'Stress',e:'🌊'},{k:'workout',l:'Workout',e:'🏋️'},
  {k:'digestion',l:'Digestion',e:'🌿'},{k:'protein',l:'Protein',e:'🥩'},
  {k:'water',l:'Water',e:'💧'},{k:'cravings',l:'Cravings',e:'🎯'},
];
const BASE_EX=[
  {id:'bp',n:'Barbell Bench Press',g:'chest',eq:'barbell',e:'🏋️'},
  {id:'dbp',n:'Dumbbell Bench Press',g:'chest',eq:'dumbbell',e:'💪'},
  {id:'pu',n:'Push-Ups',g:'chest',eq:'bodyweight',e:'🤸'},
  {id:'dl',n:'Deadlift',g:'back',eq:'barbell',e:'⚓'},
  {id:'row',n:'Barbell Row',g:'back',eq:'barbell',e:'🚣'},
  {id:'lp',n:'Lat Pulldown',g:'back',eq:'machine',e:'⬇️'},
  {id:'pu2',n:'Pull-Ups',g:'back',eq:'bodyweight',e:'🏔️'},
  {id:'dbr',n:'Dumbbell Row',g:'back',eq:'dumbbell',e:'💪'},
  {id:'ohp',n:'Overhead Press',g:'shoulders',eq:'barbell',e:'🏋️'},
  {id:'lrl',n:'Lateral Raises',g:'shoulders',eq:'dumbbell',e:'🦅'},
  {id:'bc',n:'Barbell Curl',g:'arms',eq:'barbell',e:'💪'},
  {id:'td',n:'Tricep Dips',g:'arms',eq:'bodyweight',e:'⬇️'},
  {id:'sq',n:'Back Squat',g:'legs',eq:'barbell',e:'👑'},
  {id:'leg',n:'Leg Press',g:'legs',eq:'machine',e:'🦵'},
  {id:'bg',n:'Bulgarian Split Squat',g:'legs',eq:'dumbbell',e:'🦵'},
  {id:'bsq',n:'Bodyweight Squat',g:'legs',eq:'bodyweight',e:'🦵'},
  {id:'gob',n:'Goblet Squat',g:'legs',eq:'dumbbell',e:'🏺'},
  {id:'hip',n:'Hip Thrust',g:'glutes',eq:'barbell',e:'🍑'},
  {id:'rdl',n:'Romanian Deadlift',g:'glutes',eq:'barbell',e:'⚓'},
  {id:'drdl',n:'DB Romanian Deadlift',g:'glutes',eq:'dumbbell',e:'⚓'},
  {id:'pl',n:'Plank',g:'core',eq:'bodyweight',e:'🧱'},
  {id:'mc',n:'Mountain Climbers',g:'core',eq:'bodyweight',e:'🏔️'},
  {id:'rv',n:'Rowing Machine',g:'cardio',eq:'machine',e:'🚣'},
  {id:'br',n:'Burpees',g:'cardio',eq:'bodyweight',e:'🔥'},
];
let S   =gl('pos_s',{name:'',weight:'',goalwt:'',sober:false,goals:'',start:new Date().toISOString().slice(0,10)});
let CIs =gl('pos_ci',[]);
let TRs =gl('pos_tr',[
  {id:'t1',name:'Sobriety',type:'streak',emoji:'🙏',logs:{}},
  {id:'t2',name:'Daily Reading',type:'yesno',emoji:'📖',logs:{}},
  {id:'t3',name:'Waist Size',type:'number',unit:'in',emoji:'📏',logs:{}},
]);
let EXs =gl('pos_ex',BASE_EX);
let WLogs=gl('pos_wl',[]);
let PRs  =gl('pos_pr',{});
let wSetup={type:'gym',dur:45,energy:7,focus:'full'};
let wState={wkt:null};
let trType='yesno';
let restTO=null,wSecs=0,wInt=null;

// ── NAVIGATION ───────────────────────────────────────
function show(id){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('on'));
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('on'));
  document.getElementById('s-'+id).classList.add('on');
  const tb=document.getElementById('t-'+id);
  if(tb)tb.classList.add('on');
  document.getElementById('content').scrollTop=0;
  if(id==='home')renderHome();
  if(id==='checkin')renderCI();
  if(id==='trackers')renderTr();
  if(id==='history')renderHist();
  if(id==='profile')renderProf();
  if(id==='progress')renderProg();
}

// ── HOME ─────────────────────────────────────────────
function td(){return new Date().toISOString().slice(0,10);}
function streak(){
  let s=0,d=new Date();
  for(let i=0;i<91;i++){if(CIs.find(c=>c.date===d.toISOString().slice(0,10))){s++;d.setDate(d.getDate()-1);}else break;}
  return s;
}
function renderHome(){
  const h=new Date().getHours();
  const g=h<12?'Good morning.':h<17?'Good afternoon.':'Good evening.';
  document.getElementById('greeting').textContent=g+(S.name?' '+S.name.split(' ')[0]+'.':'');
  const start=new Date(S.start),day=Math.max(1,Math.floor((Date.now()-start)/86400000)+1);
  document.getElementById('daynum').textContent=Math.min(day,90);
  const str=streak();
  document.getElementById('streaknum').textContent=str;
  document.getElementById('streakmsg').textContent=str===0?'Log your first check-in to start your streak.':str<7?str+' day'+(str>1?'s':'')+' in. Keep going.':str<30?str+' days strong.':str+' days. This is who you are now.';
  if(S.weight)document.getElementById('sw').textContent=S.weight+'lb';
  const r7=CIs.slice(-7);
  if(r7.length)document.getElementById('savg').textContent=(r7.reduce((a,b)=>a+b.avg,0)/r7.length).toFixed(1);
  const td2=Math.min(day,90);
  document.getElementById('scomp').textContent=td2>0?Math.round(CIs.length/td2*100)+'%':'—';
  document.getElementById('cistatus').textContent=CIs.find(c=>c.date===td())?'✓ Completed — view your plan':'Takes under 2 minutes';
  document.getElementById('wktstatus').textContent=WLogs.find(w=>w.date===td())?'✓ Workout logged today':'Build your AI training plan';
  const last=CIs[CIs.length-1];
  if(last&&last.air){const el=document.getElementById('homeai');el.textContent=last.air.slice(0,220).replace(/\n/g,' ')+'…';el.classList.remove('dim');}
}

// ── CHECK-IN ──────────────────────────────────────────
function renderCI(){
  document.getElementById('cidatelbl').textContent=new Date().toLocaleDateString('en-US',{weekday:'long',month:'long',day:'numeric'}).toUpperCase();
  const g=document.getElementById('dimgrid');g.innerHTML='';
  DIMS.forEach(dim=>{
    const d=document.createElement('div');d.className='dimrow';
    d.innerHTML=`<div class="dimlbl"><span>${dim.e} ${dim.l}</span><span class="dimval" id="dv-${dim.k}">—</span></div><div class="pips" id="pp-${dim.k}"></div>`;
    g.appendChild(d);
    const pr=document.getElementById('pp-'+dim.k);
    for(let i=1;i<=10;i++){const p=document.createElement('div');p.className='pip';p.textContent=i;p.onclick=()=>selPip(dim.k,i);pr.appendChild(p);}
  });
  document.getElementById('sobsec').style.display=S.sober?'block':'none';
  document.getElementById('sobyes').className='sobopt';
  document.getElementById('sobno').className='sobopt';
  document.getElementById('cinotes').value='';
  window._cs={};window._sob=null;
}
function selPip(k,v){
  window._cs[k]=v;
  document.querySelectorAll('#pp-'+k+' .pip').forEach((p,i)=>{p.className='pip';if(i+1===v)p.classList.add(v<=3?'lo':v<=6?'md':'hi');});
  document.getElementById('dv-'+k).textContent=v;
}
function setSob(v){window._sob=v;document.getElementById('sobyes').className='sobopt'+(v==='yes'?' yes':'');document.getElementById('sobno').className='sobopt'+(v==='no'?' no':'');}
async function submitCI(){
  if(Object.keys(window._cs||{}).length<8){toast('Score at least 8 dimensions');return;}
  const btn=document.getElementById('cibtn');btn.disabled=true;btn.textContent='Generating your plan...';
  const vals=Object.values(window._cs);
  const avg=+(vals.reduce((a,b)=>a+b,0)/vals.length).toFixed(1);
  const notes=document.getElementById('cinotes').value;
  show('ai');
  document.getElementById('aidatelbl').textContent=new Date().toLocaleDateString('en-US',{weekday:'long',month:'long',day:'numeric'}).toUpperCase();
  document.getElementById('aiout').textContent='Analyzing your check-in...';
  document.getElementById('aiout').classList.add('dim');
  const air=await getAI(window._cs,window._sob,notes);
  const entry={date:td(),scores:window._cs,sob:window._sob,notes,avg,air};
  const ei=CIs.findIndex(c=>c.date===td());
  if(ei>=0)CIs[ei]=entry;else CIs.push(entry);
  sl('pos_ci',CIs);
  document.getElementById('aiout').textContent=air;
  document.getElementById('aiout').classList.remove('dim');
  btn.disabled=false;btn.textContent='Get My Daily Plan →';
  toast('Check-in saved ✓');
}
async function getAI(scores,sob,notes){
  const sl2=Object.entries(scores).map(([k,v])=>k+': '+v+'/10').join(', ');
  const avg=+(Object.values(scores).reduce((a,b)=>a+b,0)/Object.values(scores).length).toFixed(1);
  try{
    const r=await fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({model:'claude-sonnet-4-6',max_tokens:1000,system:'You are a personal health and accountability coach for the Personal Operating System. Direct, warm, practical. Give a specific daily plan with 4 sections: TRAINING, NUTRITION, MENTAL, and GOAL CHECK. Reference actual scores. Under 350 words. End with one "Win for Today." If sobriety not maintained, address that first.',messages:[{role:'user',content:`Scores: ${sl2}\nAvg: ${avg}/10\n${sob?'Sobriety: '+(sob==='yes'?'Maintained ✓':'NOT MAINTAINED'):''}${notes?'\nNotes: "'+notes+'"':''}${S.goals?'\nGoals: '+S.goals:''}${S.weight&&S.goalwt?'\nWeight: '+S.weight+'lbs → '+S.goalwt+'lbs goal':''}\n\nGive their personalized daily plan.`}]})});
    const d=await r.json();return d.content?.[0]?.text||'Unable to generate. Try again.';
  }catch(e){return 'Connection error. Check internet and try again.';}
}

// ── WORKOUT ───────────────────────────────────────────
function selT(el,t){document.querySelectorAll('.grid2:not(#focusgrid) .tile').forEach(x=>x.classList.remove('on'));el.classList.add('on');wSetup.type=t;}
function selD(el,d){document.querySelectorAll('.duropt').forEach(x=>x.classList.remove('on'));el.classList.add('on');wSetup.dur=d;}
function selF(el,f){document.querySelectorAll('#focusgrid .tile').forEach(x=>x.classList.remove('on'));el.classList.add('on');wSetup.focus=f;}
function selE(el,v){document.querySelectorAll('.epip').forEach(x=>x.className='epip');el.classList.add(v<=3?'lo':v<=6?'md':'hi');wSetup.energy=v;}
(function(){const r=document.getElementById('erow');for(let i=1;i<=10;i++){const p=document.createElement('div');p.className='epip';p.textContent=i;p.onclick=()=>selE(p,i);if(i===7){p.classList.add('hi');wSetup.energy=7;}r.appendChild(p);}})();

async function genWorkout(){
  const btn=document.getElementById('genbtn');btn.disabled=true;btn.textContent='Building your workout...';
  const rec=WLogs.slice(-5).map(w=>`${w.date}: ${w.focus} ${w.type} ${w.dur}min`).join('\n')||'No history.';
  const prc=Object.entries(PRs).map(([id,pr])=>{const ex=EXs.find(e=>e.id===id);return ex?`${ex.n}: ${pr.w}lbs x ${pr.r}`:null;}).filter(Boolean).slice(0,8).join(', ')||'No PRs.';
  const prompt=`Build a workout for Personal Operating System. Respond ONLY with JSON, no markdown.\n\nEquipment: ${wSetup.type}\nTime: ${wSetup.dur}min\nEnergy: ${wSetup.energy}/10\nFocus: ${wSetup.focus}\nHistory: ${rec}\nPRs: ${prc}\n\nJSON format:\n{"title":"Short name","subtitle":"Description","note":"One coaching sentence","exercises":[{"id":"use existing id or new","name":"Name","sets":3,"reps":"8-10","wtnote":"Start at X lbs","rest":90,"tip":"Form cue"}],"backup":[{"id":"id","name":"Name","sets":2,"reps":"12-15","wtnote":"lighter","rest":60,"tip":"quick"}]}\n\nEnergy 1-4=easier/bodyweight, 7-10=heavier. ${wSetup.dur<=30?'3-4':'4-6'} main exercises, 3 backup. Only ${wSetup.type} equipment.`;
  try{
    const r=await fetch('https://api.anthropic.com/v1/messages',{method:'POST',headers:{'Content-Type':'application/json'},body:JSON.stringify({model:'claude-sonnet-4-6',max_tokens:1000,messages:[{role:'user',content:prompt}]})});
    const d=await r.json();let t=d.content?.[0]?.text||'{}';t=t.replace(/```json|```/g,'').trim();
    startWkt(JSON.parse(t));
  }catch(e){startWkt(fallbackWkt());}
  btn.disabled=false;btn.textContent='Build My Workout →';
}
function fallbackWkt(){
  const em={gym:['barbell','dumbbell','machine','bodyweight'],dumbbells:['dumbbell','bodyweight'],home:['bodyweight','band'],bodyweight:['bodyweight']};
  const fm={full:null,upper:['chest','back','shoulders','arms'],lower:['legs','glutes','core'],cardio:['cardio','core']};
  let pool=EXs.filter(e=>(em[wSetup.type]||['bodyweight']).includes(e.eq));
  const fg=fm[wSetup.focus];if(fg)pool=pool.filter(e=>fg.includes(e.g));
  const picked=pool.sort(()=>Math.random()-.5).slice(0,wSetup.dur<=30?3:4);
  return{title:wSetup.focus.charAt(0).toUpperCase()+wSetup.focus.slice(1)+' Session',subtitle:wSetup.dur+'min '+wSetup.type,note:wSetup.energy>=7?'Energy is high — push the weights.':'Low energy. Focus on form.',exercises:picked.map(e=>({id:e.id,name:e.n,sets:wSetup.energy>=7?4:3,reps:'8-12',wtnote:'Start conservative',rest:90,tip:'Full range of motion.'})),backup:picked.slice(0,3).map(e=>({id:e.id,name:e.n,sets:2,reps:'12-15',wtnote:'Lighter',rest:60,tip:'Quick version'}))};
}
function startWkt(w){
  wState.wkt=w;
  document.getElementById('wv-setup').style.display='none';
  document.getElementById('wv-active').style.display='block';
  document.getElementById('wv-summary').style.display='none';
  document.getElementById('wktitle').textContent=w.title;
  document.getElementById('wksub').textContent=w.note||w.subtitle||'';
  if(wInt)clearInterval(wInt);wSecs=0;wInt=setInterval(()=>wSecs++,1000);
  renderExs(w.exercises);
}
function loadBackup(){
  if(!wState.wkt?.backup)return;
  wState.wkt.exercises=wState.wkt.backup;
  document.getElementById('wktitle').textContent='⚡ '+wState.wkt.title+' (Short)';
  document.querySelector('.backupbar').style.display='none';
  renderExs(wState.wkt.exercises);
  toast('Switched to 20-min version');
}
function renderExs(exList){
  const list=document.getElementById('exlist');list.innerHTML='';
  exList.forEach((ex,idx)=>{
    const pr=PRs[ex.id];
    const card=document.createElement('div');card.className='excard'+(idx===0?' cur':'');card.id='ec-'+idx;
    card.innerHTML=`<div class="exhdr" onclick="toggleEx(${idx})"><div class="ex-info"><div class="exnum">EXERCISE ${idx+1} OF ${exList.length}</div><div class="exname">${EXs.find(e=>e.id===ex.id)?.e||'💪'} ${ex.name}</div><div class="extgt">${ex.sets} sets × ${ex.reps} · ${ex.wtnote}</div></div><div class="exchk${idx===0?' done':''}" id="eck-${idx}">${idx===0?'✓':''}</div></div><div class="exbody"><div class="prbadge" id="prbdg-${idx}">${pr?'🏆 PR: '+pr.w+'lbs × '+pr.r+' ('+pr.date+')':''}</div><div class="set-logger" id="sl-${idx}"><div class="setrow" style="opacity:.5;"><div class="setlbl">#</div><div class="setlbl">REPS</div><div class="setlbl">WEIGHT</div><div></div></div></div><button class="addsetbtn" onclick="addSetRow(${idx})">+ Add Set</button><div class="restbar"><span class="restlbl">Rest Timer</span><div class="restbtns"><button class="restbtn" onclick="startRest(60)">60s</button><button class="restbtn" onclick="startRest(90)">90s</button><button class="restbtn" onclick="startRest(120)">2min</button></div></div><div style="font-size:.76rem;color:var(--tx2);margin-bottom:10px;line-height:1.5;">💡 ${ex.tip||'Full range of motion.'}</div><button class="nextbtn" onclick="nextEx(${idx})">${idx<exList.length-1?'Next Exercise →':'Finish Last Set ✓'}</button></div>`;
    list.appendChild(card);
    if(pr)document.getElementById('prbdg-'+idx).classList.add('show');
    for(let s=0;s<(ex.sets||3);s++)addSetRowN(idx,s,ex);
  });
  updWkProg();
}
function addSetRowN(ei,si,ex){
  const c=document.getElementById('sl-'+ei);if(!c)return;
  const r=document.createElement('div');r.className='setrow';
  r.innerHTML=`<div class="setlbl">${si+1}</div><input class="setinp" type="number" placeholder="${ex?.reps?.split('-')?.[0]||'0'}" id="rp-${ei}-${si}" onchange="onSC(${ei},${si})" inputmode="numeric"><input class="setinp" type="number" placeholder="lbs" step="2.5" id="wt-${ei}-${si}" onchange="onSC(${ei},${si})" inputmode="decimal"><button class="setbtn" id="sb-${ei}-${si}" onclick="togSet(${ei},${si})">○</button>`;
  c.appendChild(r);
}
function addSetRow(ei){
  const c=document.getElementById('sl-'+ei);const count=c.querySelectorAll('.setrow').length-1;const ex=wState.wkt.exercises[ei];addSetRowN(ei,count,ex);}
function onSC(ei,si){
  const w=parseFloat(document.getElementById('wt-'+ei+'-'+si)?.value)||0;
  const r=parseFloat(document.getElementById('rp-'+ei+'-'+si)?.value)||0;
  const ex=wState.wkt.exercises[ei];const p=PRs[ex.id];const we=document.getElementById('wt-'+ei+'-'+si);
  if(w>0&&r>0&&p&&(w*r>p.w*p.r||w>p.w)){we?.classList.add('pr');const b=document.getElementById('prbdg-'+ei);if(b){b.classList.add('show');b.textContent='🔥 POTENTIAL PR — Best: '+p.w+'lbs × '+p.r;}}
  else{we?.classList.remove('pr');}
}
function togSet(ei,si){
  const r=parseFloat(document.getElementById('rp-'+ei+'-'+si)?.value)||0;
  const w=parseFloat(document.getElementById('wt-'+ei+'-'+si)?.value)||0;
  const btn=document.getElementById('sb-'+ei+'-'+si);const done=btn.classList.contains('done');
  btn.classList.toggle('done',!done);btn.textContent=done?'○':'✓';
  if(!done&&r>0)chkPR(ei,r,w);
}
function chkPR(ei,reps,weight){
  const ex=wState.wkt.exercises[ei];const p=PRs[ex.id];const vol=weight*reps;
  if(!p||(weight>0&&reps>0&&(weight>p.w||vol>p.w*p.r))){
    PRs[ex.id]={w:weight,r:reps,vol,date:new Date().toLocaleDateString('en-US',{month:'short',day:'numeric'})};
    sl('pos_pr',PRs);celebratePR(ex.name,weight,reps);
  }
}
function celebratePR(name,w,r){
  document.getElementById('prdetail').textContent=name+' · '+w+'lbs × '+r+' reps';
  const o=document.getElementById('proverlay');const c=document.getElementById('prcelebrate');
  o.classList.remove('hide');setTimeout(()=>c.classList.add('show'),10);
  setTimeout(()=>{c.classList.remove('show');setTimeout(()=>o.classList.add('hide'),300);},2800);
  toast('🏆 New PR!',true);
}
function toggleEx(idx){document.querySelectorAll('.excard').forEach((c,i)=>c.classList.toggle('cur',i===idx));}
function nextEx(idx){
  const ch=document.getElementById('eck-'+idx);if(ch){ch.classList.add('done');ch.textContent='✓';}
  document.getElementById('ec-'+idx)?.classList.add('done');
  const next=idx+1;
  if(next<wState.wkt.exercises.length){toggleEx(next);document.getElementById('ec-'+next)?.scrollIntoView({behavior:'smooth',block:'start'});}
  else{document.getElementById('finbtn').style.display='block';document.getElementById('finbtn').scrollIntoView({behavior:'smooth'});}
  updWkProg();
}
function updWkProg(){
  const tot=wState.wkt?.exercises?.length||1;const done=document.querySelectorAll('.excard.done').length;
  document.getElementById('wkprog').style.width=Math.round(done/tot*100)+'%';
  document.getElementById('wkbadge').textContent=done+'/'+tot;
}
function startRest(s){
  if(restTO)clearTimeout(restTO);let rem=s;
  const upd=()=>{if(rem<=0){toast('Rest done — go! 💪');return;}restTO=setTimeout(upd,1000);rem--;};
  upd();toast('Rest: '+s+'s started');
}
function finishWkt(){
  clearInterval(wInt);const mins=Math.round(wSecs/60);let tv=0;const le=[];
  wState.wkt.exercises.forEach((ex,ei)=>{const sets=[];let si=0;while(document.getElementById('rp-'+ei+'-'+si)){const r=parseFloat(document.getElementById('rp-'+ei+'-'+si)?.value)||0;const w=parseFloat(document.getElementById('wt-'+ei+'-'+si)?.value)||0;const d=document.getElementById('sb-'+ei+'-'+si)?.classList.contains('done');if(r>0){sets.push({r,w,d});tv+=w*r;}si++;}le.push({id:ex.id,name:ex.name,sets});});
  WLogs.push({date:td(),type:wSetup.type,focus:wSetup.focus,dur:mins,vol:Math.round(tv),exercises:le});
  sl('pos_wl',WLogs);
  document.getElementById('wv-active').style.display='none';
  document.getElementById('wv-summary').style.display='block';
  document.getElementById('wsumsub').textContent=new Date().toLocaleDateString('en-US',{weekday:'long',month:'long',day:'numeric'}).toUpperCase();
  const tpr=Object.entries(PRs).filter(([,p])=>p.date===new Date().toLocaleDateString('en-US',{month:'short',day:'numeric'}));
  document.getElementById('wsumcard').innerHTML=`<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;text-align:center;"><div><div style="font-family:var(--fm);font-size:1.35rem;color:var(--green);">${mins}</div><div style="font-size:.68rem;color:var(--tx2);">minutes</div></div><div><div style="font-family:var(--fm);font-size:1.35rem;color:var(--green);">${le.length}</div><div style="font-size:.68rem;color:var(--tx2);">exercises</div></div><div><div style="font-family:var(--fm);font-size:1.35rem;color:var(--green);">${tv>0?Math.round(tv).toLocaleString():'—'}</div><div style="font-size:.68rem;color:var(--tx2);">lbs moved</div></div></div>${tpr.length?`<div style="margin-top:12px;padding-top:10px;border-top:1px solid var(--bd);font-family:var(--fm);font-size:.7rem;color:var(--gold);">🏆 ${tpr.length} new PR${tpr.length>1?'s':''} today</div>`:''}`;
  document.getElementById('wsumprs').innerHTML=tpr.map(([id,pr])=>{const ex=EXs.find(e=>e.id===id);return`<div class="card2" style="border-color:var(--gold);background:var(--goldlt);">🏆 <strong>${ex?.n||id}</strong> · ${pr.w}lbs × ${pr.r} reps</div>`;}).join('');
  toast('Workout saved ✓');
}
function resetWkt(){
  document.getElementById('wv-setup').style.display='block';
  document.getElementById('wv-active').style.display='none';
  document.getElementById('wv-summary').style.display='none';
  document.getElementById('finbtn').style.display='none';
  document.querySelector('.backupbar').style.display='flex';
}

// ── TRACKERS ─────────────────────────────────────────
function renderTr(){
  const list=document.getElementById('trlist');list.innerHTML='';
  if(!TRs.length){list.innerHTML='<div class="card2" style="color:var(--tx3);">No trackers yet.</div>';return;}
  TRs.forEach(t=>{
    const str=calcTStr(t);const l7=last7(t);
    const card=document.createElement('div');card.className='trcard';
    card.innerHTML=`<div class="trtop"><div class="trname">${t.emoji||'📌'} ${t.name} <span style="font-weight:300;color:var(--tx2);font-size:.72rem;">${t.unit||t.type}</span></div><div class="trsrk">${str>0?str+'🔥':''}</div></div><div class="trchips" id="tc-${t.id}"></div>`;
    list.appendChild(card);
    const tc=document.getElementById('tc-'+t.id);
    l7.forEach(({date,label,done})=>{const chip=document.createElement('div');chip.className='dchip'+(done?' done':'');chip.textContent=label;chip.onclick=()=>logTr(t.id,date,t.type);tc.appendChild(chip);});
    if(t.type==='number'||t.type==='scale'){const inp=document.createElement('input');inp.type='number';inp.placeholder=t.type==='scale'?'1-10':'Enter value';inp.className='inp';inp.style='margin-top:8px;margin-bottom:0;';inp.value=t.logs[td()]||'';inp.onchange=()=>{t.logs[td()]=inp.value;sl('pos_tr',TRs);renderTr();};card.appendChild(inp);}
  });
}
function last7(t){const d=[];for(let i=6;i>=0;i--){const dt=new Date();dt.setDate(dt.getDate()-i);const ds=dt.toISOString().slice(0,10);const v=t.logs[ds];const done=t.type==='yesno'||t.type==='streak'?v===true||v===1:v!=null&&v!=='';d.push({date:ds,label:dt.toLocaleDateString('en-US',{weekday:'narrow'}),done});}return d;}
function calcTStr(t){let s=0,d=new Date();for(let i=0;i<365;i++){const ds=d.toISOString().slice(0,10);const v=t.logs[ds];const done=t.type==='yesno'||t.type==='streak'?v===true||v===1:v!=null&&v!=='';if(done){s++;d.setDate(d.getDate()-1);}else break;}return s;}
function logTr(id,date,type){const t=TRs.find(x=>x.id===id);if(!t)return;if(type==='yesno'||type==='streak'){t.logs[date]=!t.logs[date];sl('pos_tr',TRs);renderTr();}}
function openAddTr(){document.getElementById('tname').value='';document.getElementById('temoji').value='';document.getElementById('tunit').value='';document.querySelectorAll('.topt').forEach(o=>o.classList.remove('on'));document.querySelector('[data-t="yesno"]').classList.add('on');trType='yesno';document.getElementById('unitwrap').style.display='none';document.getElementById('trmodal').classList.remove('hide');}
function selTT(el,t){document.querySelectorAll('.topt').forEach(o=>o.classList.remove('on'));el.classList.add('on');trType=t;document.getElementById('unitwrap').style.display=t==='number'?'block':'none';}
function addTracker(){const name=document.getElementById('tname').value.trim();if(!name){toast('Enter a tracker name');return;}TRs.push({id:'t'+Date.now(),name,type:trType,emoji:document.getElementById('temoji').value||'📌',unit:document.getElementById('tunit').value||'',logs:{}});sl('pos_tr',TRs);document.getElementById('trmodal').classList.add('hide');renderTr();toast('Tracker added ✓');}

// ── HISTORY ───────────────────────────────────────────
function renderHist(){
  const list=document.getElementById('hlist');list.innerHTML='';
  if(!CIs.length){list.innerHTML='<div class="card2" style="color:var(--tx3);">No check-ins logged yet.</div>';return;}
  [...CIs].reverse().forEach(ci=>{
    const d=new Date(ci.date+'T12:00:00');const el=document.createElement('div');el.className='hentry';
    const chips=Object.entries(ci.scores).map(([k,v])=>{const cls=v>=7?'dg':v>=5?'dy':'dr';const dim=DIMS.find(x=>x.k===k);return`<span class="hdim ${cls}">${dim?.e||''} ${v}</span>`;}).join('');
    el.innerHTML=`<div class="htop"><span class="hdate">${d.toLocaleDateString('en-US',{weekday:'short',month:'short',day:'numeric'})}</span><span class="hscore">Avg ${ci.avg}</span></div><div class="hdims">${chips}</div>${ci.notes?`<div style="margin-top:7px;font-size:.76rem;color:var(--tx3);">"${ci.notes.slice(0,100)}${ci.notes.length>100?'…':''}"</div>`:''}`;
    list.appendChild(el);
  });
}

// ── PROFILE ───────────────────────────────────────────
function renderProf(){
  document.getElementById('sname').value=S.name||'';
  document.getElementById('sweight').value=S.weight||'';
  document.getElementById('sgoalwt').value=S.goalwt||'';
  document.getElementById('ssober').checked=S.sober||false;
  document.getElementById('sgoals').value=S.goals||'';
  const init=(S.name||'?').split(' ').map(w=>w[0]).join('').slice(0,2).toUpperCase();
  document.getElementById('pavatar').textContent=init||'?';
  document.getElementById('pname').textContent=S.name||'Your Name';
  const start=new Date(S.start),day=Math.max(1,Math.floor((Date.now()-start)/86400000)+1);
  document.getElementById('pdaynum').textContent=Math.min(day,90);
  const gb=document.getElementById('goalbar');gb.innerHTML='';
  if(S.weight&&S.goalwt){
    const curr=parseFloat(S.weight),goal=parseFloat(S.goalwt);
    const sw=gl('pos_sw',curr);if(!gl('pos_sw',null))sl('pos_sw',curr);
    const tl=sw-goal,lost=sw-curr,pct=tl>0?Math.min(100,Math.round(lost/tl*100)):0;
    gb.innerHTML=`<div class="card"><div style="display:flex;justify-content:space-between;font-size:.8rem;margin-bottom:5px;"><span>Weight: ${curr}lb → ${goal}lb</span><span style="font-family:var(--fm);font-size:.7rem;color:var(--green);">${pct}%</span></div><div class="gbar"><div class="gbarfill" style="width:${pct}%"></div></div><div style="font-size:.72rem;color:var(--tx3);margin-top:4px;">${lost>0?lost+' lbs lost · ':''}${tl-lost>0?Math.round(tl-lost)+' to go':'🎯 Goal reached!'}</div></div>`;
  }
}
function saveS(){S.name=document.getElementById('sname').value;S.weight=document.getElementById('sweight').value;S.goalwt=document.getElementById('sgoalwt').value;S.sober=document.getElementById('ssober').checked;S.goals=document.getElementById('sgoals').value;sl('pos_s',S);const i=(S.name||'?').split(' ').map(w=>w[0]).join('').slice(0,2).toUpperCase();document.getElementById('pavatar').textContent=i||'?';document.getElementById('pname').textContent=S.name||'Your Name';}

// ── PROGRESS ─────────────────────────────────────────
function renderProg(){
  const c=document.getElementById('progsec');
  if(!WLogs.length){c.innerHTML='<div class="card2" style="color:var(--tx2);">No workouts logged yet.</div>';return;}
  const tw=WLogs.length,tv=WLogs.reduce((a,b)=>a+(b.vol||0),0),tm=WLogs.reduce((a,b)=>a+(b.dur||0),0),pc=Object.keys(PRs).length;
  let h=`<div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:18px;"><div class="card2" style="text-align:center;"><div style="font-family:var(--fm);font-size:1.4rem;color:var(--green);">${tw}</div><div style="font-size:.7rem;color:var(--tx2);">workouts</div></div><div class="card2" style="text-align:center;"><div style="font-family:var(--fm);font-size:1.4rem;color:var(--gold);">${pc}</div><div style="font-size:.7rem;color:var(--tx2);">personal records</div></div><div class="card2" style="text-align:center;"><div style="font-family:var(--fm);font-size:1.4rem;color:var(--green);">${Math.round(tm/60)}h</div><div style="font-size:.7rem;color:var(--tx2);">training time</div></div><div class="card2" style="text-align:center;"><div style="font-family:var(--fm);font-size:1.4rem;color:var(--green);">${tv>0?(tv/1000).toFixed(0)+'k':'—'}</div><div style="font-size:.7rem;color:var(--tx2);">lbs volume</div></div></div><div class="sh">Personal Records</div>`;
  const pre=Object.entries(PRs);
  if(!pre.length)h+='<div class="card2" style="color:var(--tx2);">No PRs yet. Log weights during workouts.</div>';
  else pre.forEach(([id,pr])=>{const ex=EXs.find(e=>e.id===id);if(!ex)return;const hist=WLogs.flatMap(w=>w.exercises.filter(e=>e.id===id).flatMap(e=>e.sets.filter(s=>s.w>0).map(s=>({date:w.date,w:s.w,r:s.r,vol:s.w*s.r}))));h+=`<div class="liftcard"><div class="lifthdr" onclick="this.nextElementSibling.classList.toggle('open')"><div><div style="font-weight:600;font-size:.88rem;">${ex.e||'💪'} ${ex.n}</div><div style="font-size:.7rem;color:var(--tx2);margin-top:2px;">${hist.length} sets logged</div></div><div style="text-align:right;"><div style="font-family:var(--fm);font-size:.75rem;color:var(--gold);">🏆 ${pr.w}lbs × ${pr.r}</div><div style="font-size:.62rem;color:var(--tx3);">${pr.date}</div></div></div><div class="liftbody">${hist.slice(-5).reverse().map(h2=>`<div class="liftrow"><span style="font-family:var(--fm);font-size:.66rem;color:var(--tx3);min-width:55px;">${new Date(h2.date+'T12:00').toLocaleDateString('en-US',{month:'short',day:'numeric'})}</span><span style="font-family:var(--fm);font-size:.78rem;">${h2.w}lbs × ${h2.r}</span></div>`).join('')}</div></div>`;});
  h+=`<div class="sh">Recent Sessions</div>${[...WLogs].reverse().slice(0,6).map(w=>`<div class="card2" style="display:flex;justify-content:space-between;align-items:center;"><div><div style="font-size:.85rem;font-weight:500;">${w.focus?.charAt(0).toUpperCase()+w.focus?.slice(1)||'Workout'}</div><div style="font-family:var(--fm);font-size:.62rem;color:var(--tx3);">${new Date(w.date+'T12:00').toLocaleDateString('en-US',{weekday:'short',month:'short',day:'numeric'})}</div></div><div style="text-align:right;"><div style="font-family:var(--fm);font-size:.78rem;color:var(--green);">${w.dur||'?'}min</div><div style="font-size:.65rem;color:var(--tx3);">${w.vol?(w.vol.toLocaleString()+' lbs'):'—'}</div></div></div>`).join('')}`;
  c.innerHTML=h+'<div class="footer">© 2025 Personal Operating System · All rights reserved.</div>';
}

// ── TOAST ─────────────────────────────────────────────
let toastTO=null;
function toast(msg,gold=false){
  const t=document.getElementById('toast');t.textContent=msg;t.className='toast'+(gold?' gold':'');
  if(toastTO)clearTimeout(toastTO);toastTO=setTimeout(()=>t.classList.add('hide'),2400);
}

// ── INIT ─────────────────────────────────────────────
document.getElementById('topdate').textContent=new Date().toLocaleDateString('en-US',{weekday:'short',month:'short',day:'numeric'}).toUpperCase();
renderHome();
</script>
</body>
</html>
