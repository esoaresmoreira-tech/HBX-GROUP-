<!DOCTYPE html>
<html lang="es" translate="no" class="notranslate">
<head>
<meta charset="UTF-8">
<meta name="google" content="notranslate">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Mallorca Water Score</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Sora:wght@500;600;700;800&family=Figtree:wght@400;500;600;700&family=JetBrains+Mono:wght@500&display=swap">
<style>
/* Prototipo: Mallorca Water Score · Equipo Second Life · datos simulados
   Layout: cabecera + 5 vistas en flujo (huésped → hotel → zona → distribuidor → Mallorca) */
:root{
  --bg:#EDF3F6; --surface:#FFFFFF; --ink:#0D2738; --muted:#557083; --line:#D2DFE6;
  --accent:#0B7FA8; --accent-soft:#D5ECF4; --deep:#0A3A55;
  --good:#1E8A5A; --good-soft:#D8F0E3; --warn:#C27A10; --warn-soft:#FBEBD0; --bad:#C23B3B; --bad-soft:#F7DADA;
  --f-display:"Sora", "Trebuchet MS", system-ui, sans-serif;
  --f-body:"Figtree", system-ui, -apple-system, "Segoe UI", sans-serif;
  --f-mono:"JetBrains Mono", ui-monospace, Menlo, monospace;
}
@media (prefers-color-scheme: dark){:root{
  --bg:#08151E; --surface:#0F2230; --ink:#E2EEF4; --muted:#93AEBE; --line:#21394A;
  --accent:#3DB7E0; --accent-soft:#123447; --deep:#061019;
  --good:#4CC48C; --good-soft:#123628; --warn:#E8A94A; --warn-soft:#3A2C14; --bad:#EF7B7B; --bad-soft:#3D1C1C; color-scheme:dark}}
*{box-sizing:border-box}
[hidden]{display:none!important}
body{margin:0;background:var(--bg);color:var(--ink);font-family:var(--f-body);font-size:15px;line-height:1.5}
.wrap{max-width:1140px;margin:0 auto;padding:20px 16px 48px}
header.top{display:flex;flex-wrap:wrap;align-items:flex-end;justify-content:space-between;gap:12px 24px;margin-bottom:18px}
h1{font-family:var(--f-display);font-weight:800;font-size:clamp(26px,4vw,36px);letter-spacing:-.02em;margin:0;line-height:1.05}
h1 span{color:var(--accent)}
.top p{margin:4px 0 0;color:var(--muted);font-size:14px}
.sim{font-family:var(--f-mono);font-size:11px;letter-spacing:.06em;text-transform:uppercase;background:var(--warn-soft);border:1px dashed var(--warn);padding:5px 9px;border-radius:6px;white-space:nowrap}
nav.steps{display:grid;grid-template-columns:repeat(5,minmax(0,1fr));gap:8px;margin-bottom:22px}
nav.steps a{display:flex;gap:10px;align-items:center;padding:10px 12px;border-radius:10px;border:1px solid var(--line);background:var(--surface);color:var(--ink);text-decoration:none;min-width:0}
nav.steps b{font-family:var(--f-mono);font-size:12px;width:24px;height:24px;flex:none;display:grid;place-items:center;border-radius:50%;background:var(--accent-soft);color:var(--accent)}
nav.steps span{font-weight:600;font-size:14px;line-height:1.2;min-width:0}
nav.steps small{display:block;color:var(--muted);font-weight:400;font-size:12px}
nav.steps a[aria-current="page"]{border-color:var(--accent);box-shadow:inset 0 0 0 1px var(--accent)}
nav.steps a[aria-current="page"] b{background:var(--accent);color:#fff}
@media (max-width:900px){nav.steps{grid-template-columns:repeat(3,minmax(0,1fr))} nav.steps small{display:none}}
@media (max-width:520px){nav.steps{grid-template-columns:repeat(2,minmax(0,1fr))}}
a:focus-visible,button:focus-visible,input:focus-visible{outline:2px solid var(--accent);outline-offset:2px}

h2{font-family:var(--f-display);font-size:24px;margin:0;line-height:1.15;text-wrap:balance}
.head{display:flex;flex-wrap:wrap;justify-content:space-between;align-items:flex-end;gap:12px;margin-bottom:16px}
.head p{margin:2px 0 0;color:var(--muted);font-size:13px;max-width:70ch}
.card{background:var(--surface);border:1px solid var(--line);border-radius:14px;padding:16px;min-width:0}
.card h3{margin:0 0 4px;font-size:15px}
.card .sub{color:var(--muted);font-size:12px;margin:0 0 12px}
.grid2{display:grid;grid-template-columns:minmax(0,1.3fr) minmax(0,1fr);gap:12px}
.grid3{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:12px}
@media (max-width:860px){.grid2,.grid3{grid-template-columns:1fr}}
.kpis{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:12px;margin-bottom:12px}
@media (max-width:860px){.kpis{grid-template-columns:repeat(2,minmax(0,1fr))}}
.kpi{background:var(--surface);border:1px solid var(--line);border-radius:14px;padding:14px}
.kpi small{display:block;color:var(--muted);font-size:12px;text-transform:uppercase;letter-spacing:.05em}
.kpi b{display:block;font-family:var(--f-display);font-size:clamp(22px,3vw,30px);font-variant-numeric:tabular-nums;line-height:1.15;margin-top:4px}
.kpi em{font-style:normal;font-size:12px;color:var(--muted)}
.kpi.hero{background:var(--deep);border-color:var(--deep);color:#fff}
.kpi.hero small,.kpi.hero em{color:rgba(255,255,255,.8)}
.next{margin-top:14px;display:inline-flex;color:var(--accent);font-weight:700;text-decoration:none}
.btn{font:inherit;font-weight:700;border:0;border-radius:12px;padding:13px 16px;background:var(--ink);color:var(--surface);cursor:pointer;width:100%}
.btn:hover{filter:brightness(1.15)}
.chip{border:1px solid var(--line);background:var(--surface);color:var(--ink);border-radius:99px;padding:6px 10px;font:inherit;font-size:12px;cursor:pointer}
.chip[aria-pressed="true"]{background:var(--accent);border-color:var(--accent);color:#fff}
.lvl{display:inline-flex;align-items:center;gap:6px;font-size:12px;font-weight:700;border-radius:99px;padding:3px 10px}
.lvl.gota{background:var(--accent-soft);color:var(--accent)}
.lvl.ola{background:var(--good-soft);color:var(--good)}
.lvl.isla{background:var(--deep);color:#fff}
.lvl.none{background:var(--bg);color:var(--muted);font-weight:500}

/* --- 1. Huésped --- */
.split{display:grid;grid-template-columns:minmax(0,380px) minmax(0,1fr);gap:32px;align-items:start}
@media (max-width:820px){.split{grid-template-columns:1fr}}
.phone{background:#061019;border-radius:34px;padding:12px;max-width:380px;width:100%;margin:0 auto}
.screen{background:var(--surface);border-radius:24px;overflow:hidden}
.scan{padding:22px 18px 20px;display:grid;gap:14px;justify-items:center;text-align:center}
.scan h3{font-family:var(--f-display);font-size:21px;margin:0}
.scan p{margin:0;color:var(--muted);font-size:13px;max-width:30ch}
.sticker{background:#fff;border:2px solid #0D2738;border-radius:16px;padding:14px 14px 10px;display:grid;gap:6px;justify-items:center;width:200px}
.sticker svg{width:150px;height:150px}
.sticker span{font-family:var(--f-mono);font-size:12px;color:#0D2738}
.tags{display:flex;flex-wrap:wrap;justify-content:center;gap:6px}
.tags span{font-size:12px;background:var(--accent-soft);color:var(--accent);border-radius:99px;padding:3px 9px;font-weight:600}
.sc-hd{background:var(--accent);color:#fff;padding:16px 18px}
.sc-hd small{opacity:.85;font-size:12px}
.sc-hd h3{font-family:var(--f-display);font-size:19px;margin:2px 0 0;line-height:1.2}
.alert{margin:12px 16px 0;background:var(--warn-soft);border-radius:10px;padding:8px 10px;font-size:12px}
.sc-bd{padding:14px 16px 16px;display:grid;gap:10px}
.opt{border:1px solid var(--line);border-radius:12px;padding:10px 12px;display:grid;gap:6px}
.opt .t{font-weight:600;font-size:14px;display:flex;justify-content:space-between;gap:8px}
.opt .t small{color:var(--accent);font-size:12px;white-space:nowrap}
.opt .d{color:var(--muted);font-size:12px}
.opt .row{display:grid;grid-template-columns:repeat(4,1fr);gap:6px}
.opt .row .chip{padding:6px 2px}
.frow{display:grid;grid-template-columns:118px repeat(4,1fr);gap:4px;align-items:center;font-size:13px;font-weight:600}
.frow .chip{padding:5px 0;font-size:12px;text-align:center}
.duo{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.pill{font:inherit;font-size:13px;font-weight:600;text-align:left;border:1px solid var(--line);background:var(--surface);color:var(--ink);border-radius:12px;padding:9px 10px;cursor:pointer;line-height:1.25}
.pill small{display:block;font-weight:500;font-size:11px;color:var(--accent)}
.pill[aria-pressed="true"]{background:var(--accent);border-color:var(--accent);color:#fff}
.pill[aria-pressed="true"] small{color:#fff}
.saving{background:var(--accent-soft);border-radius:10px;padding:8px 10px;font-size:13px;text-align:center}
.alert{font-size:12px}
.sc-hd{padding:14px 18px}
.sc-hd h3{font-size:18px}
.tiers{border-top:1px dashed var(--line);padding-top:10px;display:grid;gap:8px}
.tiers .h{display:flex;justify-content:space-between;font-size:13px}
.tiers .h b{font-family:var(--f-display);color:var(--accent)}
.prog{height:8px;border-radius:4px;background:var(--bg);overflow:hidden}
.prog i{display:block;height:100%;background:var(--accent);transition:width .3s}
.ladder{display:grid;grid-template-columns:repeat(4,1fr);gap:6px}
.step{border:1px solid var(--line);border-radius:10px;padding:6px 4px;text-align:center;font-size:11px;line-height:1.25;color:var(--muted)}
.step b{display:block;font-size:12px;color:var(--ink)}
.step.on{border-color:var(--accent);background:var(--accent-soft);color:var(--ink)}
.done{background:var(--good-soft);border-radius:12px;padding:10px 12px;font-size:13px}
.explain h3{font-family:var(--f-display);font-size:22px;margin:0 0 8px;line-height:1.2}
.explain p{margin:0 0 12px;color:var(--muted);max-width:60ch}
.explain ul{margin:0;padding:0;list-style:none;display:grid;gap:10px;max-width:60ch}
.explain li{display:grid;grid-template-columns:28px 1fr;gap:10px}
.explain li i{font-style:normal;width:28px;height:28px;border-radius:8px;background:var(--surface);border:1px solid var(--line);display:grid;place-items:center}

/* --- 1b. Premios del huésped --- */
.ptabs{display:grid;grid-template-columns:1fr 1fr;gap:6px;margin:10px 16px 0}
.ptabs button{font:inherit;font-size:13px;font-weight:700;border:1px solid var(--line);background:var(--surface);color:var(--ink);border-radius:10px;padding:8px;cursor:pointer}
.ptabs button[aria-pressed="true"]{background:var(--ink);color:var(--surface);border-color:var(--ink)}
.ptabs span{display:inline-block;margin-left:4px;background:var(--warn);color:#fff;border-radius:99px;padding:0 7px;font-size:11px}
.bal{border-radius:14px;padding:16px;color:#fff;background:linear-gradient(135deg,#0A3A55,#0B7FA8)}
.bal small{opacity:.85;font-size:12px}
.bal b{display:block;font-family:var(--f-display);font-size:34px;line-height:1.1}
.bal .prog{background:rgba(255,255,255,.25);margin-top:8px}
.bal .prog i{background:#fff}
.bal p{margin:6px 0 0;font-size:12px}
.bal p b{display:inline;font-family:inherit;font-size:inherit;line-height:inherit}
.tipbox{background:var(--warn-soft);border-radius:10px;padding:8px 10px;font-size:12px}
.rw{display:grid;grid-template-columns:56px 1fr auto;gap:10px;align-items:center;border:1px solid var(--line);border-radius:12px;padding:10px;position:relative;transition:transform .15s}
.rw:not(.locked):hover{transform:translateY(-2px)}
.rw .em{width:56px;height:56px;border-radius:10px;display:grid;place-items:center;font-size:28px}
.rw h4{margin:0;font-size:14px;line-height:1.2}
.rw p{margin:2px 0 0;font-size:11.5px;color:var(--muted)}
.rw .tag{display:inline-block;margin-top:4px;font-size:10.5px;font-weight:700;border-radius:99px;padding:1px 7px;background:var(--good-soft);color:var(--good)}
.rw button{font:inherit;font-size:12px;font-weight:700;border:0;border-radius:10px;padding:8px 10px;background:var(--accent);color:#fff;cursor:pointer;white-space:nowrap}
.rw.locked{opacity:.72}
.rw.locked button{background:var(--bg);color:var(--muted);cursor:default}
.rw .hot{position:absolute;top:-9px;right:10px;font-size:10.5px;font-weight:800;background:var(--bad);color:#fff;border-radius:99px;padding:2px 8px}
.coupon{border:2px dashed var(--accent);border-radius:14px;padding:16px;display:grid;gap:8px;justify-items:center;text-align:center}
.coupon svg{width:150px;height:150px;background:#fff;border-radius:8px;padding:6px}
.coupon code{font-family:var(--f-mono);font-size:16px;letter-spacing:.08em}
.coupon .d{color:var(--muted);font-size:12px}
.mine{display:grid;gap:6px}
.mine button{font:inherit;font-size:12px;text-align:left;border:1px solid var(--accent);background:var(--accent-soft);color:var(--ink);border-radius:10px;padding:8px 10px;cursor:pointer}
.linkbtn{font:inherit;font-weight:700;color:var(--accent);background:none;border:0;cursor:pointer;padding:0}
.catsel{display:grid;gap:4px}
.catsel label{font-size:12px;font-weight:700;color:var(--muted)}
.catsel select{font:inherit;font-size:14px;font-weight:600;color:var(--ink);background:var(--surface);border:1px solid var(--accent);border-radius:10px;padding:9px 34px 9px 10px;appearance:none;cursor:pointer;
  background-image:linear-gradient(45deg,transparent 50%,var(--accent) 50%),linear-gradient(135deg,var(--accent) 50%,transparent 50%);background-position:calc(100% - 18px) 55%,calc(100% - 12px) 55%;background-size:6px 6px;background-repeat:no-repeat}
.rw .pr{display:flex;gap:6px;align-items:baseline;margin-top:3px;font-size:12px}
.rw .pr s{color:var(--muted)}
.rw .pr b{color:var(--good);font-size:13px}
.rw .pr em{font-style:normal;font-weight:800;font-size:10.5px;background:var(--bad);color:#fff;border-radius:99px;padding:1px 6px}
.empty{font-size:13px;color:var(--muted);border:1px dashed var(--line);border-radius:12px;padding:12px;text-align:center}
.demo{margin-top:16px;background:var(--surface);border:1px solid var(--line);border-radius:14px;padding:12px 14px;display:grid;gap:8px;max-width:60ch}
.demo select{font:inherit;font-size:14px;border:1px solid var(--line);border-radius:10px;padding:8px;background:var(--surface);color:var(--ink)}
.demo .m{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.demo .m div{background:var(--bg);border-radius:10px;padding:8px 10px;font-size:12px;color:var(--muted)}
.demo .m b{display:block;font-family:var(--f-display);font-size:20px;color:var(--ink)}

/* --- 2. Hotel --- */
.actions{display:grid;gap:8px}
.actions label{display:flex;gap:10px;align-items:flex-start;padding:8px 10px;border:1px solid var(--line);border-radius:10px;cursor:pointer;font-size:13px}
.actions input{accent-color:var(--accent);width:18px;height:18px;margin-top:1px;flex:none}
.actions small{display:block;color:var(--muted);font-size:12px}
.slider label{display:flex;justify-content:space-between;font-size:13px;font-weight:600}
.slider output{font-family:var(--f-mono);color:var(--accent)}
.slider input{width:100%;accent-color:var(--accent)}
.compare{display:grid;gap:8px;margin-top:6px}
.cmp{display:grid;grid-template-columns:120px 1fr 70px;gap:10px;align-items:center;font-size:13px}
.cmp .tr{height:14px;border-radius:7px;background:var(--bg);overflow:hidden}
.cmp .tr i{display:block;height:100%;border-radius:7px;background:var(--muted);transition:width .3s}
.cmp.me .tr i{background:var(--accent)}
.cmp span:last-child{font-family:var(--f-mono);font-size:12px;text-align:right}
.chart{overflow-x:auto}
.chart svg{width:100%;min-width:480px;height:auto;display:block}
.legend{display:flex;flex-wrap:wrap;gap:14px;font-size:12px;color:var(--muted);margin-top:6px}
.legend i{display:inline-block;width:12px;height:10px;border-radius:2px;margin-right:6px;vertical-align:middle}
.staff{display:grid;gap:6px;font-size:13px}
.staff div{display:flex;justify-content:space-between;gap:8px;padding:6px 8px;border-radius:8px;background:var(--bg)}
.staff div.new{background:var(--warn-soft)}
.staff b{font-family:var(--f-mono);font-size:12px}
.nudge{margin-top:10px;padding:10px 12px;border-radius:10px;background:var(--accent-soft);font-size:13px}

/* --- 3. Zona --- */
table{width:100%;border-collapse:collapse;font-size:14px}
th,td{text-align:left;padding:9px 10px;border-bottom:1px solid var(--line)}
th{font-size:12px;text-transform:uppercase;letter-spacing:.05em;color:var(--muted);font-weight:600}
td.num{font-family:var(--f-mono);font-variant-numeric:tabular-nums}
tr.me td{background:var(--accent-soft);font-weight:700}
.tablewrap{overflow-x:auto}

/* --- 4. Distribuidor --- */
.bar{display:flex;flex-wrap:wrap;gap:10px;align-items:center;justify-content:space-between;background:var(--surface);border:1px solid var(--line);border-radius:12px;padding:10px 14px;margin-bottom:12px;font-size:13px}
.bar label{display:flex;gap:8px;align-items:center;font-weight:600;cursor:pointer}
.bar input{accent-color:var(--accent);width:16px;height:16px}
.banner{background:var(--bad-soft);border:1px solid var(--bad);border-radius:12px;padding:10px 14px;margin-bottom:12px;font-size:13px}
.hotels{display:grid;gap:10px}
.hotel{display:grid;grid-template-columns:64px minmax(0,1fr) auto;gap:14px;align-items:center;background:var(--surface);border:1px solid var(--line);border-radius:14px;padding:12px}
.hotel .img{width:64px;height:64px;border-radius:10px;background:linear-gradient(135deg,var(--accent-soft),var(--good-soft))}
.hotel h4{margin:0;font-size:15px}
.hotel p{margin:2px 0 6px;color:var(--muted);font-size:12px}
.price{text-align:right;font-family:var(--f-display);font-size:20px;font-variant-numeric:tabular-nums}
.price small{display:block;font-family:var(--f-body);font-size:11px;color:var(--muted)}
@media (max-width:520px){.hotel{grid-template-columns:48px minmax(0,1fr)}.hotel .img{width:48px;height:48px}.price{grid-column:2;text-align:left}}

/* --- 5. Mallorca --- */
.heat{display:grid;grid-template-columns:110px repeat(12,minmax(26px,1fr));gap:3px;font-size:11px;min-width:520px}
.heat .z{font-weight:600;font-size:12px;display:flex;align-items:center}
.heat .m{text-align:center;color:var(--muted);font-family:var(--f-mono)}
.heat .c{height:26px;border-radius:4px}
.c.l1{background:var(--good-soft)} .c.l2{background:var(--warn-soft)} .c.l3{background:var(--bad)}
.c.l2{border:1px solid var(--warn)} .c.l1{border:1px solid var(--good)}
.heatwrap{overflow-x:auto}
.note{margin-top:28px;font-size:12px;color:var(--muted);border-top:1px solid var(--line);padding-top:12px;max-width:85ch}
.toast{position:fixed;left:50%;bottom:20px;transform:translateX(-50%);background:var(--ink);color:var(--surface);padding:10px 16px;border-radius:10px;font-size:14px;font-weight:600;max-width:calc(100% - 32px)}
@media (prefers-reduced-motion:reduce){*{transition:none!important}}
</style>
</head>
<body>
<div class="wrap">
  <header class="top">
    <div>
      <h1>Mallorca <span>Water Score</span></h1>
      <p>Medir, reducir y premiar el agua en los hoteles · Equipo Second Life · Reto HBX Group</p>
    </div>
    <div class="sim">Prototipo · datos simulados</div>
  </header>

  <nav class="steps" aria-label="Flujo de la solución">
    <a href="#huesped" data-view="huesped"><b>1</b><span>Huésped<small>Modo agua con QR</small></span></a>
    <a href="#hotel" data-view="hotel"><b>2</b><span>Hotel<small>Mide y reduce</small></span></a>
    <a href="#zona" data-view="zona"><b>3</b><span>Ranking<small>Compárate con tu zona</small></span></a>
    <a href="#distribuidor" data-view="distribuidor"><b>4</b><span>Distribuidor<small>Vende hoteles que ahorran</small></span></a>
    <a href="#mallorca" data-view="mallorca"><b>5</b><span>Mallorca<small>Impacto en la isla</small></span></a>
  </nav>

  <!-- ============ 1. HUÉSPED ============ -->
  <section data-v="huesped">
    <div class="split">
      <div class="phone"><div class="screen">
        <div class="scan" id="scanView">
          <h3>Escanea el QR de tu habitación</h3>
          <p>Está en la mesita. Sin registrarte, sin contraseña y sin descargar nada.</p>
          <div class="sticker"><svg id="qr" viewBox="0 0 25 25" shape-rendering="crispEdges" aria-label="Código QR de ejemplo"></svg><span>HAB. 214 · CALA SERENA</span></div>
          <div class="tags"><span>Sin registro</span><span>Sin app</span><span>30 segundos</span></div>
          <button class="btn" type="button" id="scanBtn">📷 Simular escaneo del QR</button>
        </div>

        <div id="roomApp" hidden>
          <div class="sc-hd"><small>Hotel Cala Serena (ficticio) · Hab. 214 · 5 noches</small><h3>Mallorca tiene poca agua. ¿Nos ayudas?</h3></div>
          <div class="alert">💧 Esta semana la zona de Alcúdia está en <b>presión hídrica alta</b>. Cada litro cuenta.</div>
          <div class="ptabs" role="group" aria-label="Secciones">
            <button type="button" id="tabOpts" aria-pressed="true">Mis opciones</button>
            <button type="button" id="tabRew" aria-pressed="false">🎁 Mis puntos<span id="tabPts">0</span></button>
          </div>
          <form class="sc-bd" id="guestForm">
            <div class="opt">
              <span class="t">Cambio de ropa · cada cuántos días <small id="linenPts"></small></span>
              <span class="d">1 punto por cada cambio que te ahorras.</span>
              <div class="frow freq" data-key="towel" data-l="15" data-def="3"><span>🛁 Toallas</span></div>
              <div class="frow freq" data-key="sheet" data-l="20" data-def="3"><span>🛏️ Sábanas</span></div>
              <div class="frow freq" data-key="pool" data-l="6" data-def="1"><span>🏖️ Toallas piscina</span></div>
              <span class="d">¿Necesitas algo antes? Pídelo sin coste.</span>
            </div>
            <button type="button" class="pill" id="optClean" aria-pressed="false">🧽 Limpieza ligera (sin fregar a fondo cada día)<small>+2 pts</small></button>
            <div class="tiers">
              <div class="h"><span id="tierNow">—</span><b id="pts">0 pts</b></div>
              <div class="prog"><i id="progBar"></i></div>
              <div class="d" id="tierTip" style="color:var(--muted);font-size:12px"></div>
            </div>
            <div class="saving">💧 Ahorras <b id="guestL">—</b></div>
            <button class="btn" type="submit" id="sendBtn">Confirmar mis opciones</button>
            <div class="done" id="done" hidden></div>
          </form>
          <div class="sc-bd" id="rewView" hidden></div>
        </div>
      </div></div>

      <div class="explain">
        <h3>Reducir: el huésped decide y gana premios</h3>
        <p>Cada habitación tiene su QR. El huésped elige cada cuánto quiere el cambio de toallas y sábanas y se apunta a retos de ahorro. Nadie le impone nada.</p>
        <ul>
          <li><i>💧</i><span><b>Alerta de presión hídrica.</b> El mensaje cambia según la semana: en las de presión alta se pide más ayuda.</span></li>
          <li><i>🏷️</i><span><b>Puntos = descuentos en el propio hotel.</b> Bebidas, spa, masajes, pádel y actividades, siempre en horas con huecos. El hotel vende lo que tenía vacío.</span></li>
          <li><i>🛍️</i><span><b>¿Hotel sin spa ni actividades?</b> Canjea por merchandising del hotel: botella reutilizable, bolsa o toalla de playa.</span></li>
          <li><i>📏</i><span><b>Litros, no palabras.</b> El huésped ve cuántos litros ahorra y a qué equivalen.</span></li>
          <li><i>🧹</i><span><b>Al personal le llega la lista exacta.</b> Sabe qué cambiar en cada habitación (pantalla 2).</span></li>
        </ul>
        <div class="demo">
          <label for="hotelType" style="font-size:13px;font-weight:700">Simular tipo de hotel</label>
          <select id="hotelType">
            <option value="resort">Resort con spa, pádel y actividades</option>
            <option value="basic">Hotel sin spa ni actividades</option>
          </select>
          <div class="m">
            <div>Ventas extra para el hotel<b id="dSales">0 €</b></div>
            <div>HBX (10% de los servicios)<b id="dHbx">0 €</b></div>
          </div>
          <span style="font-size:12px;color:var(--muted)">Se actualiza con cada canje del huésped. El merchandising no genera venta: es un regalo del hotel que además le hace publicidad.</span>
        </div>
        <a class="next" href="#hotel">Ver el panel del hotel →</a>
      </div>
    </div>
  </section>

  <!-- ============ 2. HOTEL ============ -->
  <section data-v="hotel" hidden>
    <div class="head">
      <div><h2>Panel del hotel · Cala Serena</h2><p>300 habitaciones · Alcúdia · temporada de mayo a octubre · cada mes se compara con el mismo mes de 2025</p></div>
      <span class="lvl" id="myLvl">—</span>
    </div>
    <div class="kpis">
      <div class="kpi hero"><small>Consumo de septiembre 2026</small><b id="kNow">—</b><em id="kNowSub">—</em></div>
      <div class="kpi"><small>Septiembre 2025</small><b>5.810 m³</b><em>lectura del contador y factura</em></div>
      <div class="kpi"><small>Agua ahorrada / temporada</small><b id="kM3">—</b><em id="kM3sub">mayo a octubre</em></div>
      <div class="kpi"><small>Ahorro neto / temporada</small><b id="kEur">—</b><em id="kEurSub">lavandería + energía + agua − costes</em></div>
    </div>
    <div class="grid2">
      <div class="card">
        <h3>Consumo total por mes (m³)</h3>
        <p class="sub">2025 frente a 2026 con Water Score</p>
        <div class="chart" id="chart"></div>
        <div class="legend"><span><i style="background:var(--line)"></i>2025</span><span><i style="background:var(--accent)"></i>2026 con Water Score</span></div>
        <div class="nudge" id="nudge">—</div>
      </div>
      <div class="card">
        <h3>Acciones del hotel</h3>
        <p class="sub">Activa medidas y mira cómo cambian tu consumo y tu nivel</p>
        <div class="actions">
          <label for="aAir"><input type="checkbox" id="aAir"><span>Aireadores en duchas y grifos<small>−7% · 3.000 €, una vez</small></span></label>
          <label for="aLeak"><input type="checkbox" id="aLeak"><span>Contador inteligente con aviso de fugas<small>−3% · 1.500 €</small></span></label>
          <label for="aGarden"><input type="checkbox" id="aGarden"><span>Riego por goteo nocturno<small>−2% · 2.000 €</small></span></label>
          <label for="aPool"><input type="checkbox" id="aPool"><span>Cubierta nocturna de piscina<small>−1% de evaporación · 2.500 €</small></span></label>
        </div>
        <div class="slider" style="margin-top:14px">
          <label for="part">Huéspedes en el modo agua <output id="partOut">20%</output></label>
          <input type="range" id="part" min="0" max="80" step="5" value="20">
        </div>
        <h3 style="margin-top:14px">Lista de limpieza de hoy · planta 2</h3>
        <div class="staff" id="staff"></div>
      </div>
    </div>
    <a class="next" href="#zona">Ver el ranking de la zona →</a>
  </section>

  <!-- ============ 3. ZONA ============ -->
  <section data-v="zona" hidden>
    <div class="head"><div><h2>Ranking de agua · Alcúdia · septiembre</h2><p>Cada hotel se compara consigo mismo: cuánto ha reducido su consumo frente al mismo mes del año anterior. Así vale igual para un hotel grande que para uno pequeño. Los demás hoteles son ficticios.</p></div></div>
    <div class="grid3" style="margin-bottom:12px">
      <div class="card"><span class="lvl gota">💧 Gota</span><p class="sub" style="margin-top:8px">Registra su consumo cada mes.</p><b>Panel de seguimiento + etiqueta "Mide su agua"</b></div>
      <div class="card"><span class="lvl ola">🌊 Ola</span><p class="sub" style="margin-top:8px">Reduce al menos un 5% frente al año anterior.</p><b>Etiqueta visible + mejor posición en HBX</b></div>
      <div class="card"><span class="lvl isla">🏝️ Isla</span><p class="sub" style="margin-top:8px">Reduce un 15% o más frente al año anterior.</p><b>Prioridad en semanas de presión + campañas de HBX</b></div>
    </div>
    <div class="card tablewrap">
      <table>
        <thead><tr><th>#</th><th>Hotel</th><th>Sept. 2025</th><th>Sept. 2026</th><th>Reducción</th><th>Nivel</th></tr></thead>
        <tbody id="rankBody"></tbody>
      </table>
    </div>
    <a class="next" href="#distribuidor">Ver qué ve el distribuidor →</a>
  </section>

  <!-- ============ 4. DISTRIBUIDOR ============ -->
  <section data-v="distribuidor" hidden>
    <div class="head"><div><h2>Búsqueda de una agencia de viajes</h2><p>Alcúdia · 2 adultos · 7 noches · hoteles ficticios</p></div></div>
    <div class="bar">
      <label for="pressure"><input type="checkbox" id="pressure"> Simular semana de presión hídrica alta (agosto)</label>
      <label for="onlyWater"><input type="checkbox" id="onlyWater"> Solo hoteles Ola o Isla</label>
    </div>
    <div class="banner" id="pBanner" hidden>🔴 <b>Semana de presión hídrica alta en Alcúdia.</b> HBX da prioridad a los hoteles que menos agua consumen por huésped.</div>
    <div class="hotels" id="hotelList"></div>
    <a class="next" href="#mallorca">Ver el impacto en Mallorca →</a>
  </section>

  <!-- ============ 5. MALLORCA ============ -->
  <section data-v="mallorca" hidden>
    <div class="head">
      <div><h2>Impacto en Mallorca</h2><p>Si muchos hoteles hicieran lo mismo que Cala Serena</p></div>
      <div class="slider card" style="min-width:min(100%,300px);padding:10px 14px">
        <label for="nHotels">Hoteles en el programa <output id="nOut">20</output></label>
        <input type="range" id="nHotels" min="5" max="200" step="5" value="20">
      </div>
    </div>
    <div class="kpis">
      <div class="kpi hero"><small>Agua ahorrada / temporada</small><b id="iM3">—</b><em>menos extracción de acuíferos</em></div>
      <div class="kpi"><small>Por cada hotel</small><b id="iPer">—</b><em>ahorrados de mayo a octubre</em></div>
      <div class="kpi"><small>Camiones cisterna evitados</small><b id="iTruck">—</b><em>de 25 m³ cada uno</em></div>
      <div class="kpi"><small>Ahorro neto de los hoteles</small><b id="iEur">—</b><em>por temporada</em></div>
    </div>
    <div class="card">
      <h3>Índice de presión hídrica por zona y mes</h3>
      <p class="sub">Calculado con la previsión de reservas de HBX y datos públicos de agua. En rojo, los meses donde el Water Score da más visibilidad.</p>
      <div class="heatwrap"><div class="heat" id="heat"></div></div>
      <div class="legend"><span><i style="background:var(--good-soft);border:1px solid var(--good)"></i>Baja</span><span><i style="background:var(--warn-soft);border:1px solid var(--warn)"></i>Media</span><span><i style="background:var(--bad)"></i>Alta</span></div>
    </div>
  </section>

  <p class="note"><b>Supuestos del prototipo (datos simulados):</b> hotel de 300 habitaciones con un consumo de 34.390 m³ de mayo a octubre de 2025 (4.950, 5.810, 6.720, 6.860, 5.810 y 4.240 m³ al mes). Precio del agua para hoteles en Palma: ≈0,60 €/m³ (dato real, Ara Balears, agosto de 2026); se usa 0,63 €/m³. Energía para calentar agua: 4 €/m³ sobre el 35% del agua ahorrada. Lavandería: 45.246 habitaciones ocupadas en la temporada, 4 € por cambio evitado y 2 de cada 3 cambios evitados por cada huésped que participa. Premios: 25.000 € × % de participación. QR y formación: 800 €. Camión cisterna de 25 m³. Lavado de 10 L por kg de ropa en el cálculo del huésped.</p>
</div>

<div class="toast" id="toast" hidden></div>

<script>
const $ = id => document.getElementById(id);
const fmt = n => Math.round(n).toLocaleString('es-ES');
const NIGHTS = 5;
const MONTHS = ['May', 'Jun', 'Jul', 'Ago', 'Sep', 'Oct'];
const M2025 = [4950, 5810, 6720, 6860, 5810, 4240];   // m³ por mes en 2025 (simulado)
const TOTAL25 = M2025.reduce((a, b) => a + b, 0);       // 34.390 m³
const SEPT = 4;                                         // índice de septiembre
const ROOM_NIGHTS = 45246, WATER_EUR = 0.63, HOT_SHARE = 0.35, HOT_EUR = 4, CHANGE_EUR = 4;
const ACTIONS = { aAir: { r: 0.07, c: 3000 }, aLeak: { r: 0.03, c: 1500 }, aGarden: { r: 0.02, c: 2000 }, aPool: { r: 0.01, c: 2500 } };
let guestSent = false;

/* ---------- 1. HUÉSPED ---------- */
const FREQS = [{ f: 1, l: '1' }, { f: 2, l: '2' }, { f: 3, l: '3' }, { f: 4, l: '4' }];
const freq = {};
const on = id => $(id).getAttribute('aria-pressed') === 'true';
document.querySelectorAll('.freq').forEach(row => {
  const k = row.dataset.key; freq[k] = +row.dataset.def;
  row.setAttribute('role', 'group');
  row.insertAdjacentHTML('beforeend', FREQS.map(o => `<button type="button" class="chip" data-f="${o.f}" aria-label="Cada ${o.l} días">${o.l}</button>`).join(''));
  const paint = () => row.querySelectorAll('.chip').forEach(b => b.setAttribute('aria-pressed', +b.dataset.f === freq[k] ? 'true' : 'false'));
  row.addEventListener('click', e => { const b = e.target.closest('.chip'); if (!b) return; freq[k] = +b.dataset.f; paint(); renderGuest(); });
  paint();
});
['optClean'].forEach(id => $(id).addEventListener('click', () => {
  $(id).setAttribute('aria-pressed', on(id) ? 'false' : 'true'); renderGuest();
}));
const avoided = f => NIGHTS - Math.ceil(NIGHTS / f);
function guestLiters() {
  let l = 0;
  document.querySelectorAll('.freq').forEach(b => l += avoided(freq[b.dataset.key]) * (+b.dataset.l));
  if (on('optClean')) l += NIGHTS * 0.6 * 12;
  return l;
}
const TIERS = [
  { n: 'Gota', min: 2, r: 'descuentos en bebidas' },
  { n: 'Arroyo', min: 3, r: 'pádel y descuentos en spa' },
  { n: 'Río', min: 6, r: 'masaje con −30%' },
  { n: 'Mar', min: 9, r: 'todo el catálogo' }
];
/* 1 punto por cada cambio de ropa evitado + 2 por limpieza ligera */
function guestPoints() {
  let p = 0; Object.values(freq).forEach(f => p += avoided(f));
  if (on('optClean')) p += 2;
  return p;
}
function renderGuest() {
  const p = guestPoints(), l = guestLiters();
  const cur = TIERS.filter(t => p >= t.min).pop(), next = TIERS.find(t => p < t.min);
  let linen = 0; Object.values(freq).forEach(f => linen += avoided(f));
  $('linenPts').textContent = '+' + linen + ' pts';
  $('pts').textContent = p + ' pts';
  $('tierNow').innerHTML = cur ? `Nivel <b>${cur.n}</b> · ${cur.r}` : 'Aún sin premio';
  $('progBar').style.width = Math.min(100, p / 11 * 100) + '%';
  $('tierTip').textContent = next ? `${next.min - p} pts más para nivel ${next.n}: ${next.r}` : '¡Nivel máximo! Todo el catálogo desbloqueado';
  $('guestL').textContent = fmt(l) + ' litros · ' + fmt(l / 130) + ' días de agua de un residente';
  if (typeof spent !== 'undefined') {
    $('tabPts').textContent = Math.max(0, p - spent);
    if (!$('rewView').hidden) renderRewards();
  }
}

function qrInner(seed) {
  const N = 25; let s = seed, cells = '';
  const rnd = () => { s = (s * 9301 + 49297) % 233280; return s / 233280; };
  const finder = (x, y) => `<rect x="${x}" y="${y}" width="7" height="7" fill="#0D2738"/><rect x="${x + 1}" y="${y + 1}" width="5" height="5" fill="#fff"/><rect x="${x + 2}" y="${y + 2}" width="3" height="3" fill="#0D2738"/>`;
  const inF = (x, y) => (x < 8 && y < 8) || (x > N - 9 && y < 8) || (x < 8 && y > N - 9);
  for (let y = 0; y < N; y++) for (let x = 0; x < N; x++) if (!inF(x, y) && rnd() > .52) cells += `<rect x="${x}" y="${y}" width="1" height="1" fill="#0D2738"/>`;
  return '<rect width="25" height="25" fill="#fff"/>' + cells + finder(0, 0) + finder(N - 7, 0) + finder(0, N - 7);
}
$('qr').innerHTML = qrInner(214);

/* ---------- 1b. PUNTOS = DESCUENTOS EN EL PROPIO HOTEL ---------- */
/* need: qué instalación hace falta. null = lo tiene cualquier hotel (bar, tienda). */
const CATS = [
  { id: 'all', n: '✨ Todo' },
  { id: 'drink', n: '🍹 Bebidas' },
  { id: 'spa', n: '💆 Spa y masajes', need: 'spa' },
  { id: 'sport', n: '🎾 Pádel y deporte', need: 'sport' },
  { id: 'act', n: '🧭 Actividades del hotel', need: 'act' },
  { id: 'merch', n: '🛍️ Merchandising del hotel' }
];
const REWARDS = [
  { id: 'zumo', cat: 'drink', e: '🍊', n: 'Zumo natural o café con hielo', p: 'Bar de la piscina · de 16 a 18 h', c: 2, was: 4.5, now: 2.25, bg: 'linear-gradient(135deg,#FFE3B8,#F29F38)' },
  { id: 'coctel', cat: 'drink', e: '🍹', n: 'Cóctel de la casa', p: 'Lobby bar · antes de las 20 h', c: 3, was: 10, now: 7, bg: 'linear-gradient(135deg,#FFD1E3,#D6006F)' },
  { id: 'vino', cat: 'drink', e: '🍷', n: 'Botella de vino de Mallorca', p: 'Restaurante · cenas de lunes a jueves', c: 4, was: 24, now: 18, bg: 'linear-gradient(135deg,#E9D3F0,#8E4AA6)' },
  { id: 'circuito', cat: 'spa', need: 'spa', e: '♨️', n: 'Circuito de spa (90 min)', p: 'Spa · de 10 a 13 h', c: 4, was: 25, now: 15, bg: 'linear-gradient(135deg,#D5ECF4,#2EB4E6)' },
  { id: 'masaje', cat: 'spa', need: 'spa', e: '💆', n: 'Masaje relajante (60 min)', p: 'Spa · de 10 a 13 h, con el spa vacío', c: 6, was: 60, now: 42, bg: 'linear-gradient(135deg,#CFE6FA,#0098DA)', hot: '🔥 El más elegido' },
  { id: 'padel', cat: 'sport', need: 'sport', e: '🎾', n: 'Pista de pádel (1 hora)', p: 'Pistas del hotel · de 13 a 17 h · palas incluidas', c: 3, was: 20, now: 10, bg: 'linear-gradient(135deg,#E4F7C8,#6BBF3A)' },
  { id: 'bici', cat: 'sport', need: 'sport', e: '🚲', n: 'Bici eléctrica (medio día)', p: 'Recepción · salida antes de las 10 h', c: 4, was: 30, now: 21, bg: 'linear-gradient(135deg,#D6F0DF,#2E9A63)' },
  { id: 'yoga', cat: 'act', need: 'act', e: '🧘', n: 'Yoga al amanecer', p: 'Jardín del hotel · 8:00 h', c: 2, was: 12, now: 6, bg: 'linear-gradient(135deg,#FCE9D9,#E58B5A)' },
  { id: 'kayak', cat: 'act', need: 'act', e: '🛶', n: 'Kayak o paddle surf (1 h)', p: 'Club de playa del hotel · por la mañana', c: 5, was: 35, now: 24.5, bg: 'linear-gradient(135deg,#D3EEF9,#0B6FA8)' },
  { id: 'bolsa', cat: 'merch', e: '👜', n: 'Bolsa de algodón reciclado del hotel', p: 'Recogida en recepción', c: 4, value: 8, bg: 'linear-gradient(135deg,#F0EDE6,#B9A98A)' },
  { id: 'botella', cat: 'merch', e: '🧴', n: 'Botella reutilizable del hotel', p: 'Recepción · rellénala gratis en las fuentes del hotel', c: 5, value: 12, bg: 'linear-gradient(135deg,#D5ECF4,#13305A)', tag: 'Adiós al plástico' },
  { id: 'toalla', cat: 'merch', e: '🏖️', n: 'Toalla de playa del hotel', p: 'Recepción · para llevártela a casa', c: 8, value: 25, bg: 'linear-gradient(135deg,#FFE0EE,#2EB4E6)' },
  { id: 'peluche', cat: 'merch', e: '🧸', n: 'Peluche Gota, la mascota del hotel', p: 'Recepción · el favorito de los niños', c: 6, value: 15, bg: 'linear-gradient(135deg,#E3F1F9,#7FC8EC)', tag: 'Ideal para familias' },
  { id: 'pelucheXL', cat: 'merch', e: '🐢', n: 'Peluche tortuga marina (grande)', p: 'Recepción · edición Mallorca', c: 9, value: 22, bg: 'linear-gradient(135deg,#D6F0DF,#2E9A63)' }
];
const HOTEL_HAS = { resort: ['spa', 'sport', 'act'], basic: [] };
let hotelType = 'resort', cat = 'all', spent = 0, coupons = [], extraSales = 0;
const eur = n => n.toLocaleString('es-ES', { minimumFractionDigits: n % 1 ? 2 : 0, maximumFractionDigits: 2 }) + ' €';
const hasIt = r => !r.need || HOTEL_HAS[hotelType].includes(r.need);
const catalog = () => REWARDS.filter(hasIt);
const available = () => Math.max(0, guestPoints() - spent);
function showTab(which) {
  const rew = which === 'rew';
  $('guestForm').hidden = rew; $('rewView').hidden = !rew;
  $('tabOpts').setAttribute('aria-pressed', rew ? 'false' : 'true');
  $('tabRew').setAttribute('aria-pressed', rew ? 'true' : 'false');
  if (rew) renderRewards();
}
function nextTip() {
  const k = Object.keys(freq).find(x => freq[x] < 4 && avoided(freq[x] + 1) > avoided(freq[x]));
  if (k) return `💡 Cambia las ${k === 'towel' ? 'toallas' : k === 'sheet' ? 'sábanas' : 'toallas de piscina'} cada ${freq[k] + 1} días y gana +${avoided(freq[k] + 1) - avoided(freq[k])} pts.`;
  if (!on('optClean')) return '💡 Elige limpieza ligera y gana +2 pts.';
  return '🌟 ¡Lo estás haciendo genial!';
}
function rewardPrice(r) {
  if (r.cat === 'merch') return `<div class="pr"><b>Gratis</b><span style="color:var(--muted)">valor ${eur(r.value)}</span></div>`;
  const off = Math.round((1 - r.now / r.was) * 100);
  return `<div class="pr"><s>${eur(r.was)}</s><b>${eur(r.now)}</b><em>−${off}%</em></div>`;
}
function renderRewards() {
  const list = catalog(), avail = available();
  const next = list.filter(r => r.c > avail).sort((a, b) => a.c - b.c)[0];
  const pct = next ? Math.min(100, avail / next.c * 100) : 100;
  const cats = CATS.filter(c => !c.need || HOTEL_HAS[hotelType].includes(c.need));
  if (!cats.some(c => c.id === cat)) cat = 'all';
  let h = `<div class="bal"><small>${guestSent ? 'Tus puntos para gastar en el hotel' : 'Puntos que vas a ganar'}</small><b>${avail} pts</b>
    <div class="prog"><i style="width:${pct}%"></i></div>
    <p>${next ? `Te faltan <b>${next.c - avail} pts</b> para ${next.e} ${next.n.toLowerCase()}` : '¡Puedes canjear cualquier premio!'}</p></div>`;
  if (!guestSent) h += `<div class="tipbox">Confirma tus opciones para activar tus puntos. <button type="button" class="linkbtn" data-go="opts">Ir a mis opciones →</button></div>`;
  else h += `<div class="tipbox">${nextTip()} <button type="button" class="linkbtn" data-go="opts">Cambiar opciones</button></div>`;
  if (coupons.length) h += `<div class="mine"><b style="font-size:13px">Mis cupones</b>${coupons.map((c, i) => `<button type="button" data-coupon="${i}">${c.r.e} ${c.r.n} · <code>${c.code}</code></button>`).join('')}</div>`;
  h += `<div class="catsel"><label for="catSel">¿En qué quieres usar tus puntos?</label><select id="catSel">${cats.map(c => {
    const n = c.id === 'all' ? list.length : list.filter(r => r.cat === c.id).length;
    return `<option value="${c.id}"${c.id === cat ? ' selected' : ''}>${c.n} (${n})</option>`;
  }).join('')}</select></div>`;
  const shown = list.filter(r => cat === 'all' || r.cat === cat).sort((a, b) => cat === 'all' ? 0 : a.c - b.c);
  h += shown.length ? shown.map(r => {
    const locked = r.c > avail;
    return `<div class="rw${locked ? ' locked' : ''}">${r.hot ? `<span class="hot">${r.hot}</span>` : ''}
      <div class="em" style="background:${r.bg}">${r.e}</div>
      <div><h4>${r.n}</h4><p>${r.p}</p>${rewardPrice(r)}${r.tag ? `<span class="tag">${r.tag}</span>` : ''}</div>
      <button type="button" data-redeem="${r.id}"${locked ? ' aria-disabled="true"' : ''}>${locked ? `🔒 Faltan ${r.c - avail}` : `Canjear · ${r.c} pts`}</button></div>`;
  }).join('') : `<div class="empty">Este hotel no tiene esta categoría.</div>`;
  if (hotelType === 'basic') h += `<div class="tipbox">🛍️ Este hotel no tiene spa ni actividades: tus puntos valen para bebidas y merchandising del hotel.</div>`;
  h += `<p style="margin:0;font-size:11px;color:var(--muted)">Descuentos en servicios del propio hotel, en las horas con menos gente. Un canje por estancia y categoría. Datos simulados.</p>`;
  $('rewView').innerHTML = h;
}
function showCoupon(c) {
  const r = c.r, merch = r.cat === 'merch';
  $('rewView').innerHTML = `<div class="coupon">
    <div style="font-size:38px">${r.e}</div><b>${r.n}</b><span class="d">${r.p}</span>
    <span style="font-size:15px">${merch ? `<b>Gratis</b> · valor ${eur(r.value)}` : `Pagas <b>${eur(r.now)}</b> en lugar de <s>${eur(r.was)}</s>`}</span>
    <svg viewBox="0 0 25 25" shape-rendering="crispEdges" aria-label="Código QR del cupón">${qrInner(c.seed)}</svg>
    <code>${c.code}</code>
    <span class="d">${merch ? 'Enséñalo en recepción y te lo entregan.' : 'Enséñalo al pagar y te aplican el descuento. Se puede cargar a la habitación.'} Un solo uso · válido hasta tu check-out.</span>
    <button type="button" class="linkbtn" data-go="rew">← Volver a mis puntos</button></div>`;
}
function renderDemo() {
  $('dSales').textContent = eur(extraSales);
  $('dHbx').textContent = eur(Math.round(extraSales * 10) / 100);
}
document.addEventListener('change', e => {
  if (e.target.id === 'catSel') { cat = e.target.value; renderRewards(); }
});
$('hotelType').addEventListener('change', e => {
  hotelType = e.target.value; cat = 'all';
  toast(hotelType === 'basic' ? 'Hotel sin actividades: bebidas y merchandising' : 'Resort: todo el catálogo');
  if (!$('rewView').hidden) renderRewards();
});
$('tabOpts').addEventListener('click', () => showTab('opts'));
$('tabRew').addEventListener('click', () => showTab('rew'));
document.addEventListener('click', e => {
  const go = e.target.closest('[data-go]');
  if (go) { showTab(go.dataset.go); return; }
  const cp = e.target.closest('[data-coupon]');
  if (cp) { showCoupon(coupons[+cp.dataset.coupon]); return; }
  const b = e.target.closest('[data-redeem]');
  if (!b) return;
  const r = REWARDS.find(x => x.id === b.dataset.redeem);
  if (!guestSent) { toast('Primero confirma tus opciones para activar los puntos'); return; }
  if (r.c > available()) { toast(`Te faltan ${r.c - available()} pts. ¡Ahorra un poco más!`); return; }
  spent += r.c;
  if (r.now) extraSales += r.now;
  const c = { r, seed: 1000 + coupons.length * 77 + r.c, code: 'WS-214-' + (4821 + coupons.length * 137) };
  coupons.push(c);
  $('tabPts').textContent = available();
  renderDemo(); showCoupon(c); toast(r.now ? `🎉 Descuento canjeado · el hotel vende ${eur(r.now)}` : '🎁 Regalo del hotel canjeado');
});
$('scanBtn').addEventListener('click', () => { $('scanView').hidden = true; $('roomApp').hidden = false; toast('QR leído · Habitación 214'); });
$('guestForm').addEventListener('submit', e => {
  e.preventDefault();
  const l = guestLiters();
  $('done').hidden = false;
  $('done').innerHTML = `✅ Listo. Ahorrarás <b>${fmt(l)} litros</b>, lo que consume un residente de Mallorca en <b>${fmt(l / 130)} días</b>. Tus opciones ya están en la lista de limpieza del hotel.<br><br>Tienes <b>${guestPoints()} puntos</b> para descuentos en el hotel: bebidas, spa, pádel, actividades o regalos del hotel. <button type="button" class="linkbtn" data-go="rew">🎁 Usar mis puntos →</button>`;
  $('sendBtn').textContent = 'Opciones confirmadas';
  guestSent = true; renderHotel(); toast('Enviado a la lista de limpieza del hotel');
});

/* ---------- 2. HOTEL ---------- */
/* Reducción frente a 2025: acciones del hotel + huéspedes que participan */
const part = () => $('part').value / 100;
function reduction() {
  let r = 0;
  Object.keys(ACTIONS).forEach(id => { if ($(id).checked) r += ACTIONS[id].r; });
  return r + part() * 0.20;
}
function levelOf(r) {
  if (r >= 0.15) return { k: 'isla', n: '🏝️ Isla' };
  if (r >= 0.05) return { k: 'ola', n: '🌊 Ola' };
  return { k: 'gota', n: '💧 Gota' };
}
function economics() {
  const r = reduction(), saved = TOTAL25 * r;
  const water = saved * WATER_EUR, energy = saved * HOT_SHARE * HOT_EUR;
  const laundry = ROOM_NIGHTS * part() * (2 / 3) * CHANGE_EUR;
  let costs = 800 + 25000 * part();
  Object.keys(ACTIONS).forEach(id => { if ($(id).checked) costs += ACTIONS[id].c; });
  return { r, saved, water, energy, laundry, costs, net: water + energy + laundry - costs };
}
function drawChart(r) {
  const W = 560, H = 230, L = 50, R = 12, T = 14, B = 30, max = 8000;
  const y = v => T + (H - T - B) * (1 - v / max), slot = (W - L - R) / MONTHS.length, bw = slot * 0.3;
  let g = '';
  [0, 2000, 4000, 6000, 8000].forEach(v => {
    g += `<line x1="${L}" x2="${W - R}" y1="${y(v)}" y2="${y(v)}" stroke="var(--line)"/><text x="${L - 6}" y="${y(v) + 4}" text-anchor="end" font-size="11" fill="var(--muted)">${fmt(v)}</text>`;
  });
  MONTHS.forEach((m, i) => {
    const x0 = L + i * slot + slot / 2, before = M2025[i], after = before * (1 - r);
    g += `<rect x="${x0 - bw - 2}" y="${y(before)}" width="${bw}" height="${y(0) - y(before)}" rx="3" fill="var(--line)"/>`;
    g += `<rect x="${x0 + 2}" y="${y(after)}" width="${bw}" height="${y(0) - y(after)}" rx="3" fill="var(--accent)"/>`;
    g += `<text x="${x0}" y="${H - 10}" text-anchor="middle" font-size="12" fill="var(--muted)">${m}</text>`;
  });
  $('chart').innerHTML = `<svg viewBox="0 0 ${W} ${H}" role="img" aria-label="Consumo total por mes en 2025 y en 2026">${g}</svg>`;
}
function renderHotel() {
  $('partOut').textContent = $('part').value + '%';
  const e = economics(), lv = levelOf(e.r), pct = Math.round(e.r * 100);
  const septNow = M2025[SEPT] * (1 - e.r);
  $('kNow').textContent = fmt(septNow) + ' m³';
  $('kNowSub').textContent = `${pct}% menos que en septiembre de 2025`;
  $('kM3').textContent = fmt(e.saved) + ' m³';
  $('kM3sub').textContent = `de ${fmt(TOTAL25)} m³ en 2025`;
  $('kEur').textContent = (e.net >= 0 ? '+' : '') + fmt(e.net) + ' €';
  $('kEurSub').textContent = `lavandería ${fmt(e.laundry)} € · energía ${fmt(e.energy)} € · agua ${fmt(e.water)} €`;
  $('myLvl').className = 'lvl ' + lv.k; $('myLvl').textContent = 'Nivel ' + lv.n;
  drawChart(e.r);
  const toNext = lv.k === 'gota' ? 5 - pct : lv.k === 'ola' ? 15 - pct : 0;
  $('nudge').innerHTML = lv.k === 'isla'
    ? `🏝️ Has reducido un <b>${pct}%</b> frente a 2025: <b>nivel Isla</b>. Tienes prioridad en las semanas de presión hídrica.`
    : `💧 Has reducido un <b>${pct}%</b> frente a 2025. Te falta <b>${toNext}%</b> para el nivel ${lv.k === 'gota' ? 'Ola' : 'Isla'}. Activa más acciones o anima a más huéspedes.`;
  const fq = k => freq[k] === 1 ? 'diario' : 'cada ' + freq[k] + ' días';
  const rows = [
    ['201', 'Cambio completo (salida)'], ['205', 'No cambiar toallas'], ['209', 'Limpieza ligera'],
    ['212', 'No cambiar sábanas']
  ];
  $('staff').innerHTML = (guestSent ? `<div class="new"><span>214 · QR nuevo: toallas ${fq('towel')}, sábanas ${fq('sheet')}${on('optClean') ? ', limpieza ligera' : ''}</span><b>214</b></div>` : '')
    + rows.map(r => `<div><span>${r[1]}</span><b>${r[0]}</b></div>`).join('');
  renderRank(); renderHotels(); renderIsland();
}
['aAir', 'aLeak', 'aGarden', 'aPool'].forEach(id => $(id).addEventListener('change', renderHotel));
$('part').addEventListener('input', renderHotel);

/* ---------- 3. ZONA ---------- */
/* Hoteles ficticios: consumo de septiembre 2025 (m³) y reducción en 2026 */
const OTHERS = [
  { n: 'Hotel Port Blau', b: 4300, r: 0.19 }, { n: 'Hotel Es Pinar', b: 6100, r: 0.16 }, { n: 'Aparthotel Sa Marina', b: 2900, r: 0.12 },
  { n: 'Hotel Bellresguard', b: 5200, r: 0.09 }, { n: 'Hotel Cap des Pinar', b: 3700, r: 0.07 }, { n: 'Hotel Sol de Muro', b: 7400, r: 0.06 },
  { n: 'Hotel Albufera Park', b: 6800, r: 0.04 }, { n: 'Hotel Mar Blava', b: 3100, r: 0.03 }, { n: 'Hotel Can Picafort Beach', b: 5600, r: 0.01 },
  { n: 'Hotel Badia Nord', b: 4900, r: -0.02 }, { n: 'Hotel Torre Alcanada', b: 3400, r: -0.05 }
];
function renderRank() {
  const me = { n: 'Hotel Cala Serena (tú)', b: M2025[SEPT], r: reduction(), me: true };
  const all = OTHERS.concat([me]).sort((a, b) => b.r - a.r);
  $('rankBody').innerHTML = all.map((h, i) => {
    const lv = levelOf(h.r), d = Math.round(h.r * 100);
    return `<tr class="${h.me ? 'me' : ''}"><td class="num">${i + 1}</td><td>${h.n}</td><td class="num">${fmt(h.b)} m³</td><td class="num">${fmt(h.b * (1 - h.r))} m³</td><td class="num" style="color:${d > 0 ? 'var(--good)' : 'var(--bad)'}">${d > 0 ? '−' + d : '+' + Math.abs(d)}%</td><td><span class="lvl ${lv.k}">${lv.n}</span></td></tr>`;
  }).join('');
}

/* ---------- 4. DISTRIBUIDOR ---------- */
const LIST = [
  { n: 'Hotel Badia Nord', z: 'Port d\'Alcúdia · 4★', pr: 152, b: 4900, r: -0.02 },
  { n: 'Hotel Port Blau', z: 'Port d\'Alcúdia · 4★', pr: 158, b: 4300, r: 0.19 },
  { n: 'Hotel Mar Blava', z: 'Platja d\'Alcúdia · 3★', pr: 121, b: 3100, r: 0.03 },
  { n: 'Aparthotel Sa Marina', z: 'Platja d\'Alcúdia · 3★', pr: 118, b: 2900, r: 0.12 }
];
function renderHotels() {
  const press = $('pressure').checked, only = $('onlyWater').checked;
  $('pBanner').hidden = !press;
  let list = LIST.concat([{ n: 'Hotel Cala Serena', z: 'Alcúdia · 4★ · piloto Water Score', pr: 149, b: M2025[SEPT], r: reduction(), me: true }])
    .map(h => ({ ...h, lv: levelOf(h.r) }));
  if (only) list = list.filter(h => h.lv.k !== 'gota');
  const order = { isla: 0, ola: 1, gota: 2 };
  if (press) list.sort((a, b) => order[a.lv.k] - order[b.lv.k] || b.r - a.r);
  const ch = r => r > 0 ? `${Math.round(r * 100)}% menos que en sept. 2025` : `${Math.abs(Math.round(r * 100))}% más que en sept. 2025`;
  $('hotelList').innerHTML = list.map(h => `
    <article class="hotel">
      <div class="img" aria-hidden="true"></div>
      <div><h4>${h.n}</h4><p>${h.z} · ${fmt(h.b * (1 - h.r))} m³ en septiembre · ${ch(h.r)}</p><span class="lvl ${h.lv.k}">${h.lv.n}${h.lv.k === 'gota' ? ' · mide su agua' : ' · consumo de agua verificado'}</span></div>
      <div class="price">${h.pr} €<small>por noche, neto</small></div>
    </article>`).join('') || '<p>No hay hoteles con este filtro.</p>';
}
['pressure', 'onlyWater'].forEach(id => $(id).addEventListener('change', renderHotels));

/* ---------- 5. MALLORCA ---------- */
function renderIsland() {
  const n = +$('nHotels').value; $('nOut').textContent = n;
  const e = economics(), m3 = e.saved * n;
  $('iM3').textContent = fmt(m3) + ' m³';
  $('iPer').textContent = fmt(e.saved) + ' m³';
  $('iTruck').textContent = fmt(m3 / 25);
  $('iEur').textContent = fmt(e.net * n) + ' €';
}
$('nHotels').addEventListener('input', renderIsland);
(function heat() {
  const zones = [['Alcúdia', [1,1,1,1,2,2,3,3,2,1,1,1]], ['Calvià', [1,1,1,2,2,3,3,3,3,2,1,1]], ['Palma', [1,1,2,2,2,2,3,3,2,2,1,1]],
                 ['Llevant', [1,1,1,1,2,3,3,3,2,1,1,1]], ['Platja de Palma', [1,1,1,2,2,3,3,3,3,2,1,1]], ['Pla de Mallorca', [1,1,1,1,1,2,3,3,2,1,1,1]]];
  const m = ['E', 'F', 'M', 'A', 'M', 'J', 'J', 'A', 'S', 'O', 'N', 'D'];
  let h = '<div></div>' + m.map(x => `<div class="m">${x}</div>`).join('');
  zones.forEach(z => { h += `<div class="z">${z[0]}</div>` + z[1].map((v, i) => `<div class="c l${v}" title="${z[0]} · ${m[i]}"></div>`).join(''); });
  $('heat').innerHTML = h;
})();

/* ---------- NAVEGACIÓN ---------- */
let tt;
function toast(msg) { const t = $('toast'); t.textContent = msg; t.hidden = false; clearTimeout(tt); tt = setTimeout(() => t.hidden = true, 2400); }
const VIEWS = ['huesped', 'hotel', 'zona', 'distribuidor', 'mallorca'];
function route() {
  const v = VIEWS.includes(location.hash.slice(1)) ? location.hash.slice(1) : 'huesped';
  document.querySelectorAll('[data-v]').forEach(s => s.hidden = s.dataset.v !== v);
  document.querySelectorAll('nav.steps a').forEach(a => { if (a.dataset.view === v) a.setAttribute('aria-current', 'page'); else a.removeAttribute('aria-current'); });
  window.scrollTo(0, 0);
}
window.addEventListener('hashchange', route);
renderGuest(); renderHotel(); route();
</script>
</body>
</html>
