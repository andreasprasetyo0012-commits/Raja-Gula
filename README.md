<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Nauryz Quest: Guardians of Spring</title>
<meta name="description" content="A CEFR B2 English listening adventure through the Nauryz Festival of Kazakhstan." />
<style>
/* =====================================================================
   1. DESIGN TOKENS & RESET
   ===================================================================== */
:root{
  --gold:#E0A93C;
  --gold-2:#F6CE6A;
  --turquoise:#2BB6B0;
  --turquoise-2:#1E8F8A;
  --emerald:#2E7D5B;
  --emerald-2:#1F5A3F;
  --skyblue:#BFE3F1;
  --cream:#FFF8EC;
  --ink:#1B2A2E;
  --ink-soft:#3a4d52;
  --paper:#FFFFFF;
  --shadow: 0 12px 28px rgba(31,90,63,.18), 0 4px 8px rgba(31,90,63,.08);
  --radius: 18px;
  --radius-sm: 10px;
  --font-display: "Merriweather", Georgia, "Times New Roman", serif;
  --font-body: "Nunito", "Segoe UI", system-ui, -apple-system, sans-serif;
  --fs: 16px;
}
[data-theme="dark"]{
  --cream:#0E1B1F;
  --paper:#142529;
  --ink:#F2EAD3;
  --ink-soft:#bfc9c9;
  --skyblue:#1E3A45;
}
[data-theme="contrast"]{
  --cream:#000;
  --paper:#000;
  --ink:#FFFF00;
  --ink-soft:#FFFFFF;
  --gold:#FFFF00;
  --turquoise:#00FFFF;
  --emerald:#00FF66;
  --shadow:none;
}
*{box-sizing:border-box}
html,body{margin:0;padding:0}
body{
  font-family:var(--font-body);
  font-size:var(--fs);
  color:var(--ink);
  background:
    radial-gradient(1200px 600px at 10% -10%, rgba(43,182,176,.20), transparent 60%),
    radial-gradient(1000px 500px at 110% 10%, rgba(224,169,60,.18), transparent 60%),
    linear-gradient(180deg, var(--cream), #F1E9D4 60%, var(--cream));
  min-height:100vh;
  overflow-x:hidden;
}
[data-theme="dark"] body, body[data-theme="dark"]{
  background:
    radial-gradient(1200px 600px at 10% -10%, rgba(43,182,176,.18), transparent 60%),
    radial-gradient(1000px 500px at 110% 10%, rgba(224,169,60,.10), transparent 60%),
    linear-gradient(180deg, #0E1B1F, #0A1417);
}
button{font-family:inherit; cursor:pointer}
:focus-visible{outline:3px solid var(--gold); outline-offset:3px; border-radius:8px}

/* Decorative Kazakh-pattern divider (CSS only) */
.pattern-band{
  height:14px;
  background:
    radial-gradient(circle at 10px 7px, var(--gold) 4px, transparent 5px) repeat-x,
    radial-gradient(circle at 30px 7px, var(--emerald) 4px, transparent 5px) repeat-x,
    linear-gradient(90deg, var(--turquoise), var(--emerald), var(--gold), var(--emerald), var(--turquoise));
  background-size: 40px 14px, 40px 14px, 100% 100%;
  border-radius:6px;
  margin:14px 0;
  opacity:.85;
}

/* =====================================================================
   2. LAYOUT
   ===================================================================== */
.app{
  max-width:1100px;
  margin:0 auto;
  padding:20px clamp(14px,3vw,28px) 60px;
}
header.topbar{
  display:flex;align-items:center;justify-content:space-between;
  gap:12px;flex-wrap:wrap;
  padding:14px 18px;border-radius:var(--radius);
  background:linear-gradient(135deg, rgba(43,182,176,.10), rgba(224,169,60,.10));
  border:1px solid rgba(31,90,63,.12);
  backdrop-filter: blur(8px);
}
.logo{
  display:flex;align-items:center;gap:12px;
  font-family:var(--font-display);font-weight:900;letter-spacing:.3px;
}
.logo .crest{
  width:42px;height:42px;border-radius:50%;
  background:
    radial-gradient(circle at 50% 55%, var(--gold-2) 0 35%, var(--gold) 36% 60%, var(--emerald) 61% 100%);
  position:relative;box-shadow:var(--shadow);
}
.logo .crest::after{
  content:"";position:absolute;inset:8px;border-radius:50%;
  background:
    conic-gradient(from 0deg, transparent 0 25%, rgba(255,255,255,.45) 25% 27%, transparent 27% 50%,
                  rgba(255,255,255,.45) 50% 52%, transparent 52% 75%, rgba(255,255,255,.45) 75% 77%, transparent 77% 100%);
}
.logo h1{font-size:clamp(18px,2.4vw,22px); margin:0; line-height:1}
.logo small{display:block;font-family:var(--font-body);font-weight:600;color:var(--ink-soft); font-size:12px; letter-spacing:.4px}

.toolbar{display:flex;gap:8px;flex-wrap:wrap;align-items:center}
.tool-btn{
  background:var(--paper); color:var(--ink);
  border:1px solid rgba(31,90,63,.15);
  padding:8px 12px;border-radius:999px;font-weight:700;font-size:13px;
  display:inline-flex;align-items:center;gap:6px;
  transition: transform .15s ease, box-shadow .15s ease, background .2s;
}
.tool-btn:hover{transform:translateY(-1px); box-shadow:var(--shadow)}
.tool-btn[aria-pressed="true"]{background:var(--emerald);color:#fff;border-color:transparent}

/* =====================================================================
   3. SCREENS
   ===================================================================== */
.screen{display:none; animation: fadeUp .5s ease both}
.screen.active{display:block}
@keyframes fadeUp{
  from{opacity:0; transform: translateY(14px)}
  to{opacity:1; transform:none}
}

.card{
  background:var(--paper);
  border-radius:var(--radius);
  padding:clamp(18px,3vw,28px);
  box-shadow:var(--shadow);
  border:1px solid rgba(31,90,63,.08);
  margin-top:18px;
}
h2.section-title{
  font-family:var(--font-display);
  margin:0 0 6px; font-size:clamp(22px,3vw,30px); line-height:1.15;
}
.muted{color:var(--ink-soft)}
p{line-height:1.65}

/* Welcome hero */
.hero{
  display:grid;grid-template-columns: 1.2fr .8fr;gap:24px;align-items:center;
}
@media (max-width:820px){ .hero{grid-template-columns:1fr} }
.hero-art{
  position:relative;height:280px;border-radius:var(--radius);overflow:hidden;
  background:
    linear-gradient(180deg, #BFE3F1 0%, #E9F6FA 55%, #F6F1DE 55%, #DDB976 100%);
  box-shadow:var(--shadow);
}
.hero-art .sun{position:absolute;top:30px;right:36px;width:84px;height:84px;border-radius:50%;
  background:radial-gradient(circle, #FFE9A8, var(--gold) 70%);
  box-shadow: 0 0 50px rgba(224,169,60,.55);
  animation: floaty 6s ease-in-out infinite;
}
.hero-art .mountains{position:absolute;left:-10%;right:-10%;bottom:42%;height:60%;
  background:
    linear-gradient(180deg, transparent 38%, #2E7D5B 38% 100%);
  clip-path: polygon(0 100%, 10% 60%, 20% 80%, 32% 45%, 45% 75%, 58% 35%, 72% 70%, 85% 50%, 100% 80%, 100% 100%);
}
.hero-art .mountains.snow{filter: hue-rotate(-10deg) brightness(1.05);
  clip-path: polygon(0 100%, 14% 70%, 26% 85%, 38% 55%, 52% 80%, 64% 45%, 78% 75%, 92% 60%, 100% 80%, 100% 100%);
  opacity:.6;
}
.hero-art .yurt{
  position:absolute;left:38%;bottom:8%;width:120px;height:90px;
  background: linear-gradient(180deg,#FFF 0 55%, var(--gold) 55% 100%);
  border-radius:60px 60px 8px 8px;
  box-shadow: 0 6px 14px rgba(0,0,0,.18);
}
.hero-art .yurt::before{
  content:"";position:absolute;left:50%;top:-14px;transform:translateX(-50%);
  width:18px;height:18px;background:var(--turquoise);border-radius:50%;
  box-shadow:0 0 0 4px #fff inset;
}
.hero-art .yurt::after{
  content:"";position:absolute;left:50%;bottom:0;transform:translateX(-50%);
  width:30px;height:42px;background:var(--emerald-2);border-radius:14px 14px 0 0;
}
.hero-art .flower{position:absolute;width:14px;height:14px;border-radius:50%;
  background:radial-gradient(circle,#FFF 0 30%, var(--turquoise) 31% 100%);
  animation: floaty 4s ease-in-out infinite;
}
.hero-art .f1{left:18%;bottom:14%}
.hero-art .f2{left:70%;bottom:10%; animation-delay:.6s}
.hero-art .f3{left:84%;bottom:18%; background:radial-gradient(circle,#FFF 0 30%, var(--gold) 31% 100%); animation-delay:1.1s}
@keyframes floaty{
  0%,100%{transform:translateY(0)}
  50%{transform:translateY(-8px)}
}

.cta-row{display:flex;gap:10px;flex-wrap:wrap;margin-top:16px}
.btn{
  border:none;border-radius:999px;padding:12px 22px;font-weight:800;font-size:15px;
  display:inline-flex;align-items:center;gap:10px;
  transition: transform .15s, box-shadow .2s, background .2s;
}
.btn-primary{background:linear-gradient(135deg, var(--emerald), var(--turquoise)); color:#fff; box-shadow:var(--shadow)}
.btn-primary:hover{transform:translateY(-2px)}
.btn-gold{background:linear-gradient(135deg, var(--gold), var(--gold-2)); color:#3a2a00; box-shadow:var(--shadow)}
.btn-ghost{background:transparent;color:var(--ink);border:1.5px solid rgba(31,90,63,.25)}
.btn-ghost:hover{background:rgba(43,182,176,.08)}
.btn[disabled]{opacity:.45; cursor:not-allowed; transform:none}

/* Stats panel */
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:10px;margin-top:10px}
.stat{
  background:linear-gradient(180deg, rgba(43,182,176,.10), rgba(43,182,176,.02));
  border:1px solid rgba(43,182,176,.20);
  padding:12px;border-radius:14px;
}
.stat .v{font-weight:900;font-size:20px}
.stat .l{font-size:12px;color:var(--ink-soft);text-transform:uppercase;letter-spacing:.6px}

/* Avatar select */
.avatars{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:14px;margin-top:14px}
.avatar{
  border-radius:var(--radius);padding:16px;text-align:center;
  background:var(--paper);border:2px solid rgba(31,90,63,.10);
  transition: transform .15s, border-color .2s, box-shadow .2s;
  cursor:pointer;
}
.avatar:hover{transform:translateY(-3px); box-shadow:var(--shadow)}
.avatar.selected{border-color:var(--gold); box-shadow:0 0 0 4px rgba(224,169,60,.18), var(--shadow)}
.avatar .face{
  width:72px;height:72px;margin:0 auto 8px;border-radius:50%;
  background:linear-gradient(135deg,var(--turquoise),var(--emerald));
  display:flex;align-items:center;justify-content:center;color:#fff;font-weight:900;font-size:28px;
  font-family:var(--font-display);
  box-shadow:inset 0 -8px 12px rgba(0,0,0,.15);
}
.avatar.exp .face{background:linear-gradient(135deg,#2BB6B0,#1F5A3F)}
.avatar.hist .face{background:linear-gradient(135deg,#E0A93C,#7A5510)}
.avatar.mus .face{background:linear-gradient(135deg,#BFE3F1,#2BB6B0); color:#0E3338}
.avatar.amb .face{background:linear-gradient(135deg,#F6CE6A,#E0A93C); color:#3a2a00}
.avatar h4{margin:6px 0 2px;font-family:var(--font-display)}
.avatar p{margin:0;font-size:12px;color:var(--ink-soft)}

/* Briefing */
.rules{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:10px;margin-top:10px}
.rule{
  padding:12px 14px;border-radius:14px;background:rgba(224,169,60,.08);
  border:1px solid rgba(224,169,60,.25);
}
.rule b{font-family:var(--font-display); display:block; margin-bottom:4px; color:var(--emerald-2)}
[data-theme="dark"] .rule b{color:var(--gold-2)}

/* Listening controls */
.audio-panel{
  display:grid;grid-template-columns:1fr 1fr;gap:18px;align-items:start;
}
@media (max-width:780px){ .audio-panel{grid-template-columns:1fr} }
.player{
  border-radius:var(--radius);padding:18px;
  background:linear-gradient(135deg, rgba(43,182,176,.10), rgba(224,169,60,.10));
  border:1px solid rgba(31,90,63,.12);
}
.player .controls{display:flex;gap:8px;flex-wrap:wrap;margin-top:10px}
.player .meter{
  height:8px;border-radius:8px;margin-top:14px;
  background:linear-gradient(90deg, var(--turquoise), var(--emerald), var(--gold));
  background-size:200% 100%;
  animation: shimmer 2.4s linear infinite;
  opacity:.5;
}
.player.playing .meter{opacity:1; animation-duration:1s}
@keyframes shimmer{
  from{background-position:200% 0}
  to{background-position:0 0}
}
.volume{display:flex;align-items:center;gap:8px;margin-top:10px}
.volume input[type=range]{accent-color: var(--emerald)}
.transcript{
  background:var(--paper);border:1px dashed rgba(31,90,63,.25);
  padding:14px;border-radius:14px;max-height:340px;overflow:auto;
}
.transcript.hidden{display:none}
.transcript p{margin:0 0 10px}
.transcript mark{background:rgba(224,169,60,.45); padding:0 4px; border-radius:4px}

/* Festival Map */
.map{
  display:grid;grid-template-columns:repeat(5,1fr);gap:10px;margin-top:6px;
}
@media (max-width:780px){ .map{grid-template-columns:repeat(2,1fr)} }
.loc{
  position:relative;border-radius:14px;padding:14px;
  background:linear-gradient(180deg, var(--paper), rgba(43,182,176,.08));
  border:1.5px solid rgba(31,90,63,.10);
  text-align:center;
  transition: transform .2s, box-shadow .2s, border-color .2s;
}
.loc .icon{
  width:46px;height:46px;border-radius:50%;margin:0 auto 8px;
  background:linear-gradient(135deg, var(--turquoise), var(--emerald));
  display:flex;align-items:center;justify-content:center;color:#fff;font-weight:900;
  font-family:var(--font-display);
}
.loc.locked{opacity:.45; filter:grayscale(.6)}
.loc.current{border-color:var(--gold); box-shadow: 0 0 0 4px rgba(224,169,60,.20)}
.loc.done .icon{background:linear-gradient(135deg, var(--gold), var(--gold-2)); color:#3a2a00}
.loc h5{margin:0;font-family:var(--font-display);font-size:14px}
.loc small{display:block;color:var(--ink-soft);font-size:11px;margin-top:2px}

/* Challenge */
.hud{
  display:grid;grid-template-columns: repeat(auto-fit,minmax(120px,1fr));gap:10px;margin:8px 0 14px;
}
.hud .chip{
  background:var(--paper);border:1px solid rgba(31,90,63,.12);
  border-radius:12px;padding:10px;text-align:center;
}
.hud .chip b{display:block;font-size:18px}
.hud .chip span{font-size:11px;color:var(--ink-soft);letter-spacing:.4px;text-transform:uppercase}

.xp-wrap{height:14px;background:rgba(31,90,63,.10);border-radius:999px;overflow:hidden;border:1px solid rgba(31,90,63,.10)}
.xp-bar{height:100%;width:0;background:linear-gradient(90deg, var(--gold), var(--turquoise), var(--emerald));
  transition: width .6s cubic-bezier(.2,.7,.2,1);
  background-size:200% 100%;
  animation: shimmer 3s linear infinite;
}

.q-card{padding:18px;border-radius:var(--radius);background:var(--paper);box-shadow:var(--shadow);border:1px solid rgba(31,90,63,.10)}
.q-meta{display:flex;justify-content:space-between;align-items:center;gap:10px;flex-wrap:wrap;margin-bottom:8px}
.q-meta .tag{background:rgba(43,182,176,.15);color:var(--turquoise-2);padding:4px 10px;border-radius:999px;font-weight:800;font-size:12px;letter-spacing:.5px}
[data-theme="dark"] .q-meta .tag{color:#7be2dc}
.q-text{font-family:var(--font-display);font-size:clamp(17px,2.4vw,22px);line-height:1.35;margin:6px 0 14px}
.options{display:grid;gap:10px}
.opt{
  display:flex;align-items:center;gap:12px;
  padding:12px 14px;border-radius:12px;
  background:var(--paper);border:1.5px solid rgba(31,90,63,.14);
  font-weight:600; text-align:left; color:var(--ink);
  transition: transform .12s, border-color .2s, background .2s;
}
.opt:hover{transform:translateY(-1px); border-color:var(--turquoise)}
.opt .key{
  width:28px;height:28px;border-radius:8px;display:inline-flex;align-items:center;justify-content:center;
  background:rgba(43,182,176,.15);color:var(--turquoise-2);font-weight:900;flex-shrink:0;
}
.opt.correct{background:rgba(46,125,91,.12); border-color:var(--emerald); color:var(--emerald-2)}
[data-theme="dark"] .opt.correct{color:#7bd3a9}
.opt.wrong{background:rgba(200,60,60,.10); border-color:#c83c3c; color:#a73030}
.opt.eliminated{opacity:.4; text-decoration:line-through}
.opt[disabled]{cursor:default}

.feedback{
  margin-top:12px;padding:12px;border-radius:12px;font-weight:700;
  display:none;
}
.feedback.show{display:block; animation: fadeUp .35s ease both}
.feedback.ok{background:rgba(46,125,91,.12); color:var(--emerald-2); border:1px solid rgba(46,125,91,.30)}
.feedback.no{background:rgba(200,60,60,.12); color:#a73030; border:1px solid rgba(200,60,60,.30)}
[data-theme="dark"] .feedback.ok{color:#9be8c5}

.q-actions{display:flex;gap:10px;flex-wrap:wrap;margin-top:12px}

/* Timer */
.timer{
  height:6px;border-radius:999px;background:rgba(31,90,63,.12);overflow:hidden;margin-top:10px;
}
.timer-bar{height:100%;width:100%;background:linear-gradient(90deg, var(--emerald), var(--gold), #c83c3c);
  transform-origin: left center;
}

/* Results */
.report{display:grid;grid-template-columns: 1.1fr .9fr; gap:18px}
@media (max-width: 820px){ .report{grid-template-columns:1fr} }
.badge-big{
  text-align:center;padding:20px;border-radius:var(--radius);
  background:linear-gradient(135deg, var(--gold), var(--gold-2));
  color:#3a2a00; box-shadow:var(--shadow);
  position:relative; overflow:hidden;
}
.badge-big .medal{
  width:120px;height:120px;border-radius:50%;
  margin:6px auto 8px;
  background:
    radial-gradient(circle at 50% 45%, #FFF6D5 0 22%, #F6CE6A 23% 60%, #B98A1B 61% 100%);
  box-shadow: inset 0 -8px 14px rgba(0,0,0,.25), 0 8px 16px rgba(0,0,0,.18);
  position:relative;
  animation: spinIn .9s ease both;
}
@keyframes spinIn{
  from{transform: rotate(-30deg) scale(.6); opacity:0}
  to{transform:none; opacity:1}
}
.badge-big .medal::after{
  content:"★";position:absolute;inset:0;display:flex;align-items:center;justify-content:center;
  font-size:46px;color:#7A5510;
}
.bars{display:grid;gap:10px;margin-top:10px}
.bar-row{display:grid;grid-template-columns:140px 1fr 50px;gap:10px;align-items:center}
.bar-row .label{font-size:13px;color:var(--ink-soft)}
.bar-track{height:12px;border-radius:999px;background:rgba(31,90,63,.10);overflow:hidden}
.bar-fill{height:100%;background:linear-gradient(90deg, var(--turquoise), var(--emerald)); width:0; transition:width 1s ease}
.bar-fill.gold{background:linear-gradient(90deg, var(--gold), var(--gold-2))}
.bar-fill.danger{background:linear-gradient(90deg, #f6a26a, #c83c3c)}

.donut{
  --p:0;
  width:160px;height:160px;border-radius:50%;
  background: conic-gradient(var(--emerald) calc(var(--p)*1%), rgba(31,90,63,.10) 0);
  display:grid;place-items:center;margin:0 auto;
  position:relative;
}
.donut::after{content:""; width:72%; height:72%; background:var(--paper); border-radius:50%; position:absolute}
.donut .val{position:relative; font-family:var(--font-display); font-size:28px; font-weight:900}

/* Glossary */
.gloss-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:12px}
.gloss{
  perspective: 800px; cursor:pointer; min-height:140px;
}
.gloss .flip{
  position:relative;width:100%;height:100%;min-height:140px;transition:transform .6s;
  transform-style: preserve-3d;
}
.gloss.open .flip{transform: rotateY(180deg)}
.gloss .face{
  position:absolute;inset:0; border-radius:14px; padding:14px;
  backface-visibility: hidden;
  background:var(--paper);
  border:1px solid rgba(31,90,63,.12);
  box-shadow: var(--shadow);
  display:flex;flex-direction:column;justify-content:center;
}
.gloss .front{background: linear-gradient(135deg, rgba(43,182,176,.10), rgba(224,169,60,.10))}
.gloss .back{transform: rotateY(180deg)}
.gloss h5{margin:0;font-family:var(--font-display);font-size:18px}
.gloss small{color:var(--ink-soft)}

/* Achievement gallery */
.badges{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:10px}
.bd{
  text-align:center;padding:14px;border-radius:14px;
  background:var(--paper);border:1.5px dashed rgba(31,90,63,.20);
  transition: transform .2s;
}
.bd .ic{
  width:54px;height:54px;border-radius:50%;margin:0 auto 6px;
  background:linear-gradient(135deg, #d8d8d8, #b9b9b9);
  display:flex;align-items:center;justify-content:center;color:#fff;font-weight:900;font-family:var(--font-display);
  font-size:22px;
}
.bd.unlocked{border-style:solid; border-color: var(--gold); transform: translateY(-2px)}
.bd.unlocked .ic{background:linear-gradient(135deg, var(--gold), var(--gold-2)); color:#3a2a00}

/* Museum */
.museum-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:12px}
.museum .card-flip{perspective:900px; min-height:170px; cursor:pointer}
.museum .inner{position:relative;width:100%;min-height:170px;transition:transform .6s;transform-style:preserve-3d}
.museum .card-flip.open .inner{transform:rotateY(180deg)}
.museum .face{position
