<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Studio Pro - Painel Digital Automotivo</title>
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@400;600;700&family=Share+Tech+Mono&display=swap" rel="stylesheet">
  <style>
    *{box-sizing:border-box;margin:0;padding:0}
 
    :root {
      --green: #00d19a;
      --green-dark: #00a86b;
      --blue: #7dd3fc;
      --panel: rgba(8,14,24,.97);
      --border: #1e3148;
      --bg: #040b14;
      --text: #dbeafe;
      --muted: #5a7a9a;
    }
 
    body{
      font-family:'Rajdhani',sans-serif;
      background:var(--bg);
      color:var(--text);
      background-image:radial-gradient(ellipse at top left,#0c1f36 0%,#040b14 60%);
      min-height:100vh;
    }
 
    .app{
      display:grid;
      grid-template-columns:300px 1fr 320px;
      min-height:100vh;
    }
 
    .panel{
      background:var(--panel);
      border-right:1px solid var(--border);
      padding:14px;
      overflow-y:auto;
      overflow-x:hidden;
    }
    .panel.right{border-right:none;border-left:1px solid var(--border)}
 
    .logo{
      display:flex;align-items:center;gap:8px;
      margin-bottom:14px;padding-bottom:12px;
      border-bottom:1px solid var(--border);
    }
    .logo-icon{
      width:36px;height:36px;border-radius:10px;
      background:linear-gradient(135deg,#00a86b,#0077cc);
      display:flex;align-items:center;justify-content:center;
      font-family:'Orbitron',monospace;font-size:14px;font-weight:900;color:#fff;
    }
    .logo-text{font-family:'Orbitron',monospace;font-size:14px;font-weight:700;color:#fff}
    .logo-sub{font-size:11px;color:var(--muted);margin-top:1px}
 
    h2{font-family:'Rajdhani',sans-serif;font-size:13px;font-weight:700;color:var(--blue);
       text-transform:uppercase;letter-spacing:1px;margin-bottom:10px}
 
    .group{
      background:#060e1a;
      border:1px solid var(--border);
      border-radius:12px;
      padding:12px;
      margin-bottom:12px;
    }
 
    .field{margin-bottom:9px}
    .field label{display:block;font-size:12px;color:#7a9ab8;margin-bottom:4px;text-transform:uppercase;letter-spacing:.5px}
 
    input[type="text"],input[type="number"],input[type="color"],select,textarea{
      width:100%;padding:8px 10px;
      border-radius:8px;border:1px solid #1e3148;
      background:#040b14;color:var(--text);
      font-family:'Rajdhani',sans-serif;font-size:14px;
    }
    input[type="color"]{padding:4px;height:36px;cursor:pointer}
    textarea{min-height:140px;resize:vertical;font-family:'Share Tech Mono',monospace;font-size:11px}
 
    .row{display:grid;grid-template-columns:1fr 1fr;gap:8px}
    .row3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:6px}
 
    .btns{display:flex;gap:6px;flex-wrap:wrap}
    button{
      border:0;border-radius:8px;padding:8px 12px;
      cursor:pointer;font-weight:700;font-size:13px;
      font-family:'Rajdhani',sans-serif;letter-spacing:.5px;
      background:linear-gradient(135deg,#00a86b,#00d19a);color:#fff;
      transition:opacity .2s,transform .1s;
    }
    button:hover{opacity:.9;transform:translateY(-1px)}
    button:active{transform:translateY(0)}
    button.secondary{background:#142032}
    button.danger{background:#7f1d1d}
    button.blue-btn{background:linear-gradient(135deg,#1d4ed8,#3b82f6)}
 
    .workspace{padding:14px;display:flex;flex-direction:column;gap:10px}
 
    .toolbar{display:flex;justify-content:space-between;align-items:center;
             padding:10px 14px;background:#06101c;border:1px solid var(--border);
             border-radius:12px;}
 
    .tabs{display:flex;gap:6px;flex-wrap:wrap}
    .tab{padding:6px 12px;border-radius:999px;background:#0d1f32;
         border:1px solid #1e3a52;color:#8cb8d8;cursor:pointer;
         font-size:12px;font-weight:700;letter-spacing:.5px;
         font-family:'Rajdhani',sans-serif;transition:all .2s}
    .tab:hover{border-color:var(--green);color:#fff}
    .tab.active{background:linear-gradient(135deg,#00a86b,#00d19a);border-color:transparent;color:#fff}
 
    .frame-wrap{
      flex:1;display:flex;justify-content:center;align-items:center;
      background:linear-gradient(180deg,#070e1a,#030810);
      border:1px solid var(--border);border-radius:18px;padding:16px;min-height:540px;
    }
    .display-frame{
      border-radius:24px;padding:10px;
      background:#060b12;
      border:3px solid #0f2035;
      box-shadow:0 0 60px rgba(0,0,0,.6),0 0 30px rgba(0,200,140,.06),inset 0 1px 0 rgba(255,255,255,.04);
    }
    .display{
      width:800px;height:480px;position:relative;overflow:hidden;
      border-radius:16px;border:1px solid rgba(255,255,255,.06);
      transform-origin:center center;background:#05070c;
      box-shadow:inset 0 0 80px rgba(0,0,0,.5);
    }
 
    .screen{position:absolute;inset:0;display:none}
    .screen.active{display:block}
 
    /* SHARED SCREEN ELEMENTS */
    .top-glow{position:absolute;top:0;left:0;width:100%;height:3px;
      background:linear-gradient(90deg,#00ff88,#00b7ff,#7c3aed,#ff0088,#00ff88);
      background-size:200% 100%;animation:glowScroll 4s linear infinite;}
    @keyframes glowScroll{0%{background-position:0% 0%}100%{background-position:200% 0%}}
 
    .status-bar{position:absolute;top:10px;right:14px;display:flex;gap:12px;
      font-family:'Share Tech Mono',monospace;font-size:11px;color:#4a7a9a;}
    .status-dot{width:6px;height:6px;border-radius:50%;background:var(--green);
      display:inline-block;margin-right:4px;animation:pulse 2s infinite;}
    @keyframes pulse{0%,100%{opacity:1}50%{opacity:.3}}
 
    /* === TELA 1: SPLASH === */
    .s1-bg{position:absolute;inset:0;background:radial-gradient(ellipse at 50% 40%,#0d2240 0%,#050c18 70%)}
    .s1-grid{position:absolute;inset:0;
      background-image:linear-gradient(rgba(0,180,120,.05) 1px,transparent 1px),
                       linear-gradient(90deg,rgba(0,180,120,.05) 1px,transparent 1px);
      background-size:40px 40px;}
    .s1-logo-wrap{position:absolute;top:70px;left:0;right:0;text-align:center}
    .s1-logo{font-family:'Orbitron',monospace;font-size:42px;font-weight:900;color:#fff;
      text-shadow:0 0 30px rgba(0,200,140,.6),0 0 60px rgba(0,200,140,.3);letter-spacing:4px}
    .s1-tagline{font-family:'Rajdhani',sans-serif;font-size:18px;color:#7dd3fc;
      letter-spacing:6px;text-transform:uppercase;margin-top:6px}
    .s1-car{position:absolute;bottom:130px;left:50%;transform:translateX(-50%);
      font-size:11px;color:#2a5070;font-family:'Share Tech Mono',monospace;letter-spacing:2px}
    .s1-btn{position:absolute;bottom:60px;left:50%;transform:translateX(-50%);
      background:linear-gradient(135deg,#00a86b,#00d19a);border:none;
      color:#fff;padding:14px 48px;border-radius:40px;cursor:pointer;
      font-family:'Orbitron',monospace;font-size:14px;font-weight:700;letter-spacing:2px;
      box-shadow:0 0 30px rgba(0,200,140,.4);text-align:center;width:220px}
    .s1-rings{position:absolute;top:50%;left:50%;transform:translate(-50%,-50%);pointer-events:none}
    .ring{position:absolute;border-radius:50%;border:1px solid rgba(0,200,140,.1);transform:translate(-50%,-50%)}
 
    /* === TELA 2: PRINCIPAL === */
    .s2-bg{position:absolute;inset:0;background:radial-gradient(ellipse at 30% 50%,#091828 0%,#030608 70%)}
    .big-speed{position:absolute;top:40px;left:50px;
      font-family:'Orbitron',monospace;font-size:160px;font-weight:900;
      color:#ffffff;line-height:1;
      text-shadow:0 0 40px rgba(255,255,255,.2);letter-spacing:-4px}
    .speed-unit{position:absolute;top:185px;left:235px;
      font-family:'Rajdhani',sans-serif;font-size:26px;color:#7dd3fc;letter-spacing:4px}
    .rpm-bar-wrap{position:absolute;top:60px;right:30px;height:360px;width:28px;display:flex;flex-direction:column-reverse}
    .rpm-fill{background:linear-gradient(0deg,#00d19a,#0077ff,#ff4400);width:100%;border-radius:4px;transition:height .4s}
    .rpm-bg{position:absolute;top:60px;right:30px;height:360px;width:28px;
      background:#0a1520;border-radius:4px;border:1px solid #1a3050}
    .gauges-row{position:absolute;bottom:20px;left:20px;right:70px;
      display:flex;gap:10px;align-items:flex-end}
    .gauge-item{flex:1;background:#080e18;border:1px solid #1a3050;border-radius:10px;padding:10px;text-align:center}
    .gauge-label{font-size:10px;color:#4a7a9a;letter-spacing:1px;text-transform:uppercase;font-family:'Rajdhani',sans-serif}
    .gauge-val{font-family:'Share Tech Mono',monospace;font-size:18px;color:#fff;margin-top:3px}
    .gauge-val.green{color:#00d19a}
    .gauge-val.orange{color:#f97316}
    .gauge-val.blue{color:#7dd3fc}
 
    /* === TELA 3: NAVEGAÇÃO/GPS === */
    .s3-bg{position:absolute;inset:0;background:#040c18}
    .map-area{position:absolute;inset:0;overflow:hidden}
    .map-road-h{position:absolute;background:rgba(30,70,120,.5);left:0;right:0}
    .map-road-v{position:absolute;background:rgba(30,70,120,.5);top:0;bottom:0}
    .map-block{position:absolute;background:rgba(10,25,45,.8);border:1px solid #0e2035}
    .map-overlay{position:absolute;inset:0;
      background:linear-gradient(to right,rgba(4,12,24,.95) 0%,rgba(4,12,24,.4) 50%,rgba(4,12,24,.1) 100%)}
    .nav-panel{position:absolute;top:0;left:0;bottom:0;width:260px;padding:16px;display:flex;flex-direction:column;gap:10px}
    .nav-street{font-family:'Orbitron',monospace;font-size:17px;color:#fff;font-weight:700;line-height:1.2}
    .nav-dist{font-family:'Share Tech Mono',monospace;font-size:42px;color:#00d19a;line-height:1}
    .nav-dist-unit{font-size:16px;color:#5a9a7a}
    .nav-next{background:#080f1c;border:1px solid #1a3050;border-radius:10px;padding:10px}
    .nav-arrow{font-size:32px;color:#7dd3fc}
    .nav-step{font-size:13px;color:#7a9ab8;margin-top:4px}
    .nav-step strong{color:#fff}
    .eta-row{display:flex;gap:8px;margin-top:auto}
    .eta-box{flex:1;background:#080f1c;border:1px solid #1a3050;border-radius:8px;padding:8px;text-align:center}
    .eta-val{font-family:'Share Tech Mono',monospace;font-size:18px;color:#fff}
    .eta-lbl{font-size:10px;color:#4a7a9a;text-transform:uppercase;letter-spacing:1px}
    .map-pin{position:absolute;width:14px;height:14px;background:#00d19a;border-radius:50%;border:2px solid #fff;
      box-shadow:0 0 12px rgba(0,200,140,.8)}
    .map-route{position:absolute;border-top:3px solid #0077ff;opacity:.7}
 
    /* === TELA 4: DIAGNÓSTICO === */
    .s4-bg{position:absolute;inset:0;background:#040c14}
    .diag-title{position:absolute;top:18px;left:20px;
      font-family:'Orbitron',monospace;font-size:18px;color:#7dd3fc;font-weight:700;letter-spacing:2px}
    .diag-grid{position:absolute;top:60px;left:16px;right:16px;bottom:16px;
      display:grid;grid-template-columns:1fr 1fr 1fr;grid-template-rows:1fr 1fr;gap:10px}
    .diag-card{background:#060e1c;border:1px solid #1a3050;border-radius:12px;padding:12px;
      display:flex;flex-direction:column;gap:4px;position:relative;overflow:hidden}
    .diag-card::after{content:'';position:absolute;top:0;left:0;right:0;height:2px}
    .diag-card.ok::after{background:linear-gradient(90deg,#00d19a,#00a86b)}
    .diag-card.warn::after{background:linear-gradient(90deg,#f97316,#fbbf24)}
    .diag-card.crit::after{background:linear-gradient(90deg,#ef4444,#dc2626)}
    .diag-icon{font-size:22px}
    .diag-name{font-size:11px;color:#4a7a9a;letter-spacing:1px;text-transform:uppercase;font-family:'Rajdhani',sans-serif}
    .diag-val{font-family:'Share Tech Mono',monospace;font-size:22px;color:#fff}
    .diag-bar{height:4px;background:#0d2035;border-radius:2px;margin-top:4px}
    .diag-bar-fill{height:100%;border-radius:2px;background:var(--green)}
    .diag-status{font-size:10px;font-weight:700;letter-spacing:1px;text-transform:uppercase;margin-top:2px}
    .diag-status.ok{color:#00d19a}
    .diag-status.warn{color:#f97316}
    .diag-status.crit{color:#ef4444}
 
    /* === TELA 5: CONFIGURAÇÕES === */
    .s5-bg{position:absolute;inset:0;background:#040c14}
    .s5-header{position:absolute;top:0;left:0;right:0;height:56px;
      background:#060f1e;border-bottom:1px solid #1a3050;display:flex;align-items:center;padding:0 20px;gap:12px}
    .s5-header-title{font-family:'Orbitron',monospace;font-size:16px;color:#fff;font-weight:700}
    .s5-tabs{display:flex;gap:0;margin-left:auto}
    .s5-tab{padding:6px 14px;font-size:12px;font-family:'Rajdhani',sans-serif;font-weight:700;
      color:#4a7a9a;cursor:pointer;border-bottom:2px solid transparent;letter-spacing:.5px}
    .s5-tab.active{color:var(--green);border-bottom-color:var(--green)}
    .s5-body{position:absolute;top:56px;left:0;right:0;bottom:0;display:flex}
    .s5-sidebar{width:180px;background:#06101e;border-right:1px solid #1a3050;padding:10px}
    .s5-menu-item{display:flex;align-items:center;gap:8px;padding:9px 10px;border-radius:8px;
      font-size:13px;font-weight:600;color:#5a7a9a;cursor:pointer;margin-bottom:2px;letter-spacing:.3px}
    .s5-menu-item.active{background:#0d2035;color:#fff}
    .s5-menu-item .icon{font-size:15px}
    .s5-content{flex:1;padding:16px;display:flex;flex-direction:column;gap:10px;overflow:auto}
    .s5-row{display:flex;align-items:center;justify-content:space-between;
      background:#060e1c;border:1px solid #1a3050;border-radius:10px;padding:12px 14px}
    .s5-row-label{font-size:13px;font-weight:600;color:#c0d8f0}
    .s5-row-sub{font-size:11px;color:#4a7a9a;margin-top:2px}
    .toggle{width:42px;height:22px;background:#0d2035;border-radius:999px;cursor:pointer;position:relative;border:1px solid #1a4060}
    .toggle.on{background:var(--green-dark)}
    .toggle::after{content:'';position:absolute;top:2px;left:3px;width:16px;height:16px;
      border-radius:50%;background:#fff;transition:left .2s}
    .toggle.on::after{left:21px}
    .s5-slider{-webkit-appearance:none;appearance:none;height:4px;background:#0d2035;
      border-radius:2px;outline:none;cursor:pointer;border:none;width:120px}
    .s5-slider::-webkit-slider-thumb{-webkit-appearance:none;width:14px;height:14px;
      border-radius:50%;background:var(--green);cursor:pointer}
 
    .help{font-size:12px;color:#4a7a9a;line-height:1.5;font-family:'Rajdhani',sans-serif}
    .badge{display:inline-block;background:#0c1e30;border:1px solid #1e3a52;
      color:#7dd3fc;border-radius:999px;padding:3px 8px;font-size:11px;margin:2px;font-weight:700}
  </style>
</head>
<body>
  <div class="app">
 
    <!-- PAINEL ESQUERDO -->
    <aside class="panel">
      <div class="logo">
        <div class="logo-icon">SP</div>
        <div>
          <div class="logo-text">Studio Pro</div>
          <div class="logo-sub">Painel Digital Automotivo</div>
        </div>
      </div>
 
      <div class="group">
        <h2>Tela atual</h2>
        <div class="field"><label>Escolher tela</label><select id="screenSelect"></select></div>
        <div class="row">
          <div class="field"><label>Fundo</label><input type="color" id="bgColor" /></div>
          <div class="field"><label>Zoom %</label><input type="number" id="zoom" min="40" max="120" value="85"/></div>
        </div>
      </div>
 
      <div class="group">
        <h2>Elemento selecionado</h2>
        <div class="field"><label>ID</label><input type="text" id="elId" readonly/></div>
        <div class="field"><label>Texto</label><input type="text" id="elText"/></div>
        <div class="row">
          <div class="field"><label>X</label><input type="number" id="elX"/></div>
          <div class="field"><label>Y</label><input type="number" id="elY"/></div>
        </div>
        <div class="row">
          <div class="field"><label>Largura</label><input type="number" id="elW"/></div>
          <div class="field"><label>Altura</label><input type="number" id="elH"/></div>
        </div>
        <div class="row">
          <div class="field"><label>Cor texto</label><input type="color" id="elColor"/></div>
          <div class="field"><label>Cor fundo</label><input type="color" id="elBg"/></div>
        </div>
        <div class="row">
          <div class="field"><label>Fonte</label><input type="number" id="elFont" min="10" max="120"/></div>
          <div class="field"><label>Raio</label><input type="number" id="elRadius" min="0" max="50"/></div>
        </div>
        <div class="btns"><button id="applyElement">✓ Aplicar</button></div>
      </div>
 
      <div class="group">
        <h2>Dados — Tela Principal</h2>
        <div class="row">
          <div class="field"><label>Velocidade</label><input type="number" id="speedInput" value="94"/></div>
          <div class="field"><label>RPM</label><input type="number" id="rpmInput" value="3500"/></div>
        </div>
        <div class="row">
          <div class="field"><label>Temperatura</label><input type="text" id="tempInput" value="91°C"/></div>
          <div class="field"><label>Combustível</label><input type="text" id="fuelInput" value="64%"/></div>
        </div>
        <div class="row">
          <div class="field"><label>Bateria</label><input type="text" id="batteryInput" value="13.8V"/></div>
          <div class="field"><label>Odômetro</label><input type="text" id="odoInput" value="154230 km"/></div>
        </div>
        <div class="btns"><button id="applyData">↻ Atualizar</button></div>
      </div>
    </aside>
 
    <!-- CENTRO -->
    <main class="workspace">
      <div class="toolbar">
        <div>
          <div style="font-family:'Orbitron',monospace;font-size:15px;font-weight:700;color:#fff">Display 800×480</div>
          <div style="font-size:11px;color:var(--muted);margin-top:2px">Fiat Prêmio ESP32-S3</div>
        </div>
        <div class="tabs" id="tabs"></div>
      </div>
 
      <div class="frame-wrap">
        <div class="display-frame">
          <div class="display" id="display"></div>
        </div>
      </div>
    </main>
 
    <!-- PAINEL DIREITO -->
    <aside class="panel right">
      <div class="group">
        <h2>Exportação</h2>
        <div class="btns" style="margin-bottom:10px">
          <button id="saveJson">Gerar JSON</button>
          <button class="secondary" id="copyJson">Copiar</button>
          <button class="secondary" id="downloadJson">⬇ Baixar</button>
          <button class="danger" id="resetAll">Reset</button>
        </div>
        <div class="field">
          <label>Configuração JSON</label>
          <textarea id="jsonOut" readonly></textarea>
        </div>
      </div>
 
      <div class="group">
        <h2>Informações das telas</h2>
        <div class="help">
          <span class="badge">Tela 1</span> Splash de inicialização<br>
          <span class="badge">Tela 2</span> Velocímetro principal<br>
          <span class="badge">Tela 3</span> Navegação GPS<br>
          <span class="badge">Tela 4</span> Diagnóstico OBD-II<br>
          <span class="badge">Tela 5</span> Configurações<br><br>
          Clique nas abas para navegar. Clique em elementos para selecioná-los e editar no painel esquerdo.
        </div>
      </div>
    </aside>
  </div>
 
  <script>
    /* =============================================
       CONFIGURAÇÃO PADRÃO COM 5 TELAS COMPLETAS
    ============================================= */
    const defaultConfig = {
      activeScreen: 1,
      zoom: 85,
      screens: [
        {
          name: "Splash",
          bg: "#040b14",
          elements: [
            {id:"s1_title", type:"text", text:"STUDIO PRO", x:180, y:120, w:440, h:70, color:"#ffffff", bg:"transparent", font:54, radius:0},
            {id:"s1_sub",   type:"text", text:"PAINEL DIGITAL AUTOMOTIVO", x:175, y:195, w:450, h:28, color:"#7dd3fc", bg:"transparent", font:18, radius:0},
            {id:"s1_proj",  type:"text", text:"Fiat Prêmio • ESP32-S3", x:260, y:235, w:280, h:22, color:"#2a5070", bg:"transparent", font:14, radius:0},
            {id:"s1_btn",   type:"box",  text:"INICIAR", x:310, y:310, w:180, h:52, color:"#ffffff", bg:"#00a86b", font:18, radius:26}
          ]
        },
        {
          name: "Principal",
          bg: "#040608",
          elements: [
            {id:"s2_label", type:"text", text:"VELOCIDADE", x:50, y:55, w:180, h:22, color:"#4a7a9a", bg:"transparent", font:14, radius:0},
            {id:"s2_speed", type:"text", text:"094", x:30, y:75, w:280, h:160, color:"#ffffff", bg:"transparent", font:160, radius:0},
            {id:"s2_unit",  type:"text", text:"km/h", x:120, y:232, w:100, h:24, color:"#7dd3fc", bg:"transparent", font:20, radius:0},
            {id:"s2_rpm_l", type:"text", text:"RPM", x:510, y:55, w:80, h:20, color:"#4a7a9a", bg:"transparent", font:13, radius:0},
            {id:"s2_rpm",   type:"text", text:"3500", x:490, y:75, w:150, h:50, color:"#00d19a", bg:"transparent", font:40, radius:0},
            {id:"s2_g1",    type:"box",  text:"TEMP\n91°C", x:16, y:380, w:120, h:68, color:"#f97316", bg:"#060e1c", font:16, radius:10},
            {id:"s2_g2",    type:"box",  text:"COMB\n64%", x:148, y:380, w:120, h:68, color:"#00d19a", bg:"#060e1c", font:16, radius:10},
            {id:"s2_g3",    type:"box",  text:"BATT\n13.8V", x:280, y:380, w:120, h:68, color:"#7dd3fc", bg:"#060e1c", font:16, radius:10},
            {id:"s2_g4",    type:"box",  text:"ODO\n154230", x:412, y:380, w:140, h:68, color:"#c084fc", bg:"#060e1c", font:14, radius:10},
            {id:"s2_g5",    type:"box",  text:"TURNO\n02:34", x:564, y:380, w:110, h:68, color:"#fbbf24", bg:"#060e1c", font:16, radius:10}
          ]
        },
        {
          name: "Navegação",
          bg: "#040c18",
          elements: [
            {id:"s3_street", type:"text", text:"Av. Paulista", x:16, y:70, w:240, h:40, color:"#ffffff", bg:"transparent", font:26, radius:0},
            {id:"s3_dist",   type:"text", text:"320 m", x:16, y:112, w:220, h:60, color:"#00d19a", bg:"transparent", font:48, radius:0},
            {id:"s3_arrow",  type:"box",  text:"↑", x:20, y:180, w:60, h:60, color:"#7dd3fc", bg:"#060e1c", font:34, radius:10},
            {id:"s3_next",   type:"text", text:"Vire à direita em\nRua Augusta", x:90, y:185, w:160, h:50, color:"#8cb8d8", bg:"transparent", font:14, radius:0},
            {id:"s3_eta",    type:"box",  text:"ETA\n18 min", x:16, y:360, w:100, h:68, color:"#fff", bg:"#060e1c", font:18, radius:10},
            {id:"s3_dest",   type:"box",  text:"DIST\n4,2 km", x:128, y:360, w:110, h:68, color:"#7dd3fc", bg:"#060e1c", font:16, radius:10},
            {id:"s3_spd",    type:"box",  text:"LIM\n60 km/h", x:250, y:360, w:110, h:68, color:"#fbbf24", bg:"#060e1c", font:16, radius:10}
          ]
        },
        {
          name: "Diagnóstico",
          bg: "#040c14",
          elements: [
            {id:"s4_title", type:"text", text:"DIAGNÓSTICO OBD-II", x:20, y:15, w:300, h:30, color:"#7dd3fc", bg:"transparent", font:20, radius:0},
            {id:"s4_c1",    type:"box",  text:"MOTOR\n✔ OK\n91°C", x:16, y:60, w:240, h:110, color:"#00d19a", bg:"#060e1c", font:16, radius:12},
            {id:"s4_c2",    type:"box",  text:"TRANSMISSÃO\n✔ OK\n72°C", x:268, y:60, w:240, h:110, color:"#00d19a", bg:"#060e1c", font:15, radius:12},
            {id:"s4_c3",    type:"box",  text:"FREIOS\n⚠ ATENÇÃO\nDianteiro baixo", x:520, y:60, w:264, h:110, color:"#f97316", bg:"#060e1c", font:14, radius:12},
            {id:"s4_c4",    type:"box",  text:"BATERIA\n✔ OK\n13.8V", x:16, y:182, w:240, h:110, color:"#7dd3fc", bg:"#060e1c", font:16, radius:12},
            {id:"s4_c5",    type:"box",  text:"COMBUSTÍVEL\n✔ OK\n64%", x:268, y:182, w:240, h:110, color:"#00d19a", bg:"#060e1c", font:15, radius:12},
            {id:"s4_c6",    type:"box",  text:"O2 / LAMBDA\n✔ Normal\n0.97λ", x:520, y:182, w:264, h:110, color:"#00d19a", bg:"#060e1c", font:14, radius:12},
            {id:"s4_dtc",   type:"box",  text:"DTC: P0171 — Mistura pobre (Banco 1)", x:16, y:310, w:768, h:40, color:"#f97316", bg:"#0c1a0a", font:14, radius:8},
            {id:"s4_bar1",  type:"box",  text:"Carga do motor: ████████░░ 78%", x:16, y:362, w:380, h:32, color:"#c084fc", bg:"#060e1c", font:13, radius:8},
            {id:"s4_bar2",  type:"box",  text:"Avanço de ignição: ████░░░░░░ 14°", x:404, y:362, w:380, h:32, color:"#fbbf24", bg:"#060e1c", font:13, radius:8},
            {id:"s4_bar3",  type:"box",  text:"MAP: 98 kPa  |  IAT: 34°C  |  MAF: 8.4 g/s  |  TPS: 22%", x:16, y:405, w:768, h:32, color:"#7dd3fc", bg:"#060e1c", font:13, radius:8}
          ]
        },
        {
          name: "Config",
          bg: "#040c14",
          elements: [
            {id:"s5_header", type:"box",  text:"CONFIGURAÇÕES", x:0, y:0, w:800, h:52, color:"#ffffff", bg:"#060f1e", font:18, radius:0},
            {id:"s5_menu1",  type:"box",  text:"🎨 Display", x:0, y:52, w:170, h:40, color:"#00d19a", bg:"#0a1e30", font:14, radius:0},
            {id:"s5_menu2",  type:"box",  text:"📡 Sensores", x:0, y:92, w:170, h:40, color:"#7a9ab8", bg:"transparent", font:14, radius:0},
            {id:"s5_menu3",  type:"box",  text:"🔔 Alertas", x:0, y:132, w:170, h:40, color:"#7a9ab8", bg:"transparent", font:14, radius:0},
            {id:"s5_menu4",  type:"box",  text:"📶 Conexão", x:0, y:172, w:170, h:40, color:"#7a9ab8", bg:"transparent", font:14, radius:0},
            {id:"s5_menu5",  type:"box",  text:"ℹ️ Sistema", x:0, y:212, w:170, h:40, color:"#7a9ab8", bg:"transparent", font:14, radius:0},
            {id:"s5_r1",     type:"box",  text:"Brilho da tela          ████████░░ 80%", x:182, y:62, w:600, h:42, color:"#c0d8f0", bg:"#060e1c", font:14, radius:10},
            {id:"s5_r2",     type:"box",  text:"Modo noturno automático            ✔ ON", x:182, y:114, w:600, h:42, color:"#c0d8f0", bg:"#060e1c", font:14, radius:10},
            {id:"s5_r3",     type:"box",  text:"Tema de cor                          Verde", x:182, y:166, w:600, h:42, color:"#c0d8f0", bg:"#060e1c", font:14, radius:10},
            {id:"s5_r4",     type:"box",  text:"Unidade de velocidade               km/h", x:182, y:218, w:600, h:42, color:"#c0d8f0", bg:"#060e1c", font:14, radius:10},
            {id:"s5_r5",     type:"box",  text:"Bluetooth OBD-II             Conectado ✔", x:182, y:270, w:600, h:42, color:"#00d19a", bg:"#060e1c", font:14, radius:10},
            {id:"s5_r6",     type:"box",  text:"Wi-Fi                              Desligado", x:182, y:322, w:600, h:42, color:"#c0d8f0", bg:"#060e1c", font:14, radius:10},
            {id:"s5_ver",    type:"text", text:"Firmware v2.4.1  |  ESP32-S3  |  © 2025 Studio Pro", x:182, y:420, w:600, h:22, color:"#2a4060", bg:"transparent", font:12, radius:0}
          ]
        }
      ]
    };
 
    /* =============================================
       ESTADO DA APLICAÇÃO
    ============================================= */
    let config = JSON.parse(localStorage.getItem("studio-pro-config") || "null") || structuredClone(defaultConfig);
    if(config.screens.length < 5) config = structuredClone(defaultConfig);
 
    let currentScreen = config.activeScreen || 1;
    let selectedElementId = null;
    let dragState = null;
 
    const display = document.getElementById("display");
    const tabs = document.getElementById("tabs");
    const screenSelect = document.getElementById("screenSelect");
    const bgColor = document.getElementById("bgColor");
    const zoom = document.getElementById("zoom");
    const jsonOut = document.getElementById("jsonOut");
 
    function saveConfig(){
      config.activeScreen = currentScreen;
      config.zoom = Number(zoom.value);
      localStorage.setItem("studio-pro-config", JSON.stringify(config));
      jsonOut.value = JSON.stringify(config, null, 2);
    }
 
    function getCurrentScreenObj(){ return config.screens[currentScreen - 1]; }
 
    function getEl(id){ return getCurrentScreenObj().elements.find(e => e.id === id); }
 
    /* Preenche os campos do painel com dados do elemento selecionado */
    function fillFields(el){
      if(!el) return;
      document.getElementById("elId").value = el.id;
      document.getElementById("elText").value = el.text;
      document.getElementById("elX").value = el.x;
      document.getElementById("elY").value = el.y;
      document.getElementById("elW").value = el.w;
      document.getElementById("elH").value = el.h;
      document.getElementById("elColor").value = el.color.startsWith("#") ? el.color : "#ffffff";
      document.getElementById("elBg").value = (!el.bg || el.bg === "transparent") ? "#000000" : el.bg;
      document.getElementById("elFont").value = el.font;
      document.getElementById("elRadius").value = el.radius;
    }
 
    /* =============================================
       RENDERIZAÇÃO PRINCIPAL
    ============================================= */
    function render(){
      tabs.innerHTML = "";
      screenSelect.innerHTML = "";
      display.innerHTML = '<div class="top-glow"></div>';
      display.style.transform = `scale(${Number(zoom.value || config.zoom || 85)/100})`;
 
      config.screens.forEach((scr, idx) => {
        const id = idx + 1;
 
        /* Abas */
        const tab = document.createElement("div");
        tab.className = "tab" + (currentScreen === id ? " active" : "");
        tab.textContent = scr.name;
        tab.onclick = () => { currentScreen = id; selectedElementId = null; render(); };
        tabs.appendChild(tab);
 
        /* Select */
        const opt = document.createElement("option");
        opt.value = id;
        opt.textContent = scr.name;
        if(currentScreen === id) opt.selected = true;
        screenSelect.appendChild(opt);
 
        /* Tela */
        const screen = document.createElement("div");
        screen.className = "screen" + (currentScreen === id ? " active" : "");
        screen.style.background = scr.bg;
 
        /* Elementos */
        scr.elements.forEach(el => {
          const node = document.createElement("div");
          node.className = "element" + (selectedElementId === el.id ? " selected" : "");
          node.dataset.id = el.id;
          node.style.cssText = `
            left:${el.x}px; top:${el.y}px;
            width:${el.w}px; height:${el.h}px;
            color:${el.color};
            background:${(el.type==="text"||el.bg==="transparent") ? "transparent" : el.bg};
            font-size:${el.font}px;
            border-radius:${el.radius}px;
            white-space:pre-line;
            text-align:center;
            display:flex;align-items:center;justify-content:center;
            position:absolute;cursor:move;user-select:none;
            border:1px dashed ${selectedElementId===el.id?"#38bdf8":"transparent"};
            padding:4px;
          `;
          node.textContent = el.text;
 
          /* Clique para selecionar */
          node.addEventListener("mousedown", e => {
            e.stopPropagation();
            selectedElementId = el.id;
            fillFields(el);
 
            /* Iniciar drag */
            const startX = e.clientX - el.x;
            const startY = e.clientY - el.y;
            dragState = { id: el.id, startX, startY, screenIdx: idx };
            render();
          });
 
          screen.appendChild(node);
        });
 
        display.appendChild(screen);
      });
 
      bgColor.value = getCurrentScreenObj().bg;
      screenSelect.value = currentScreen;
      saveConfig();
    }
 
    /* =============================================
       DRAG & DROP
    ============================================= */
    document.addEventListener("mousemove", e => {
      if(!dragState) return;
      const scr = config.screens[dragState.screenIdx];
      const el = scr.elements.find(x => x.id === dragState.id);
      if(!el) return;
      const scale = Number(zoom.value || 85) / 100;
      el.x = Math.round(e.clientX - dragState.startX);
      el.y = Math.round(e.clientY - dragState.startY);
      fillFields(el);
      render();
    });
 
    document.addEventListener("mouseup", () => { dragState = null; });
 
    /* =============================================
       EVENTOS DOS PAINÉIS
    ============================================= */
    bgColor.addEventListener("input", () => { getCurrentScreenObj().bg = bgColor.value; render(); });
    zoom.value = config.zoom || 85;
    zoom.addEventListener("input", render);
    screenSelect.addEventListener("change", () => { currentScreen = Number(screenSelect.value); render(); });
 
    document.getElementById("applyElement").onclick = () => {
      const el = getEl(document.getElementById("elId").value);
      if(!el) return;
      el.text   = document.getElementById("elText").value;
      el.x      = Number(document.getElementById("elX").value);
      el.y      = Number(document.getElementById("elY").value);
      el.w      = Number(document.getElementById("elW").value);
      el.h      = Number(document.getElementById("elH").value);
      el.color  = document.getElementById("elColor").value;
      el.bg     = document.getElementById("elBg").value;
      el.font   = Number(document.getElementById("elFont").value);
      el.radius = Number(document.getElementById("elRadius").value);
      render();
    };
 
    document.getElementById("applyData").onclick = () => {
      const s = config.screens[1]; // Tela Principal
      const map = {
        s2_speed: document.getElementById("speedInput").value.toString().padStart(3,"0"),
        s2_rpm:   document.getElementById("rpmInput").value,
        s2_g1:    `TEMP\n${document.getElementById("tempInput").value}`,
        s2_g2:    `COMB\n${document.getElementById("fuelInput").value}`,
        s2_g3:    `BATT\n${document.getElementById("batteryInput").value}`,
        s2_g4:    `ODO\n${document.getElementById("odoInput").value}`,
      };
      s.elements.forEach(el => { if(map[el.id] !== undefined) el.text = map[el.id]; });
      render();
    };
 
    document.getElementById("saveJson").onclick = saveConfig;
    document.getElementById("copyJson").onclick = async () => {
      saveConfig(); await navigator.clipboard.writeText(jsonOut.value); alert("JSON copiado!");
    };
    document.getElementById("downloadJson").onclick = () => {
      saveConfig();
      const a = Object.assign(document.createElement("a"), {
        href: URL.createObjectURL(new Blob([jsonOut.value],{type:"application/json"})),
        download: "painel_config.json"
      });
      a.click(); URL.revokeObjectURL(a.href);
    };
    document.getElementById("resetAll").onclick = () => {
      if(!confirm("Resetar para o layout padrão?")) return;
      config = structuredClone(defaultConfig); currentScreen = 1; render();
    };
 
    /* INIT */
    render();
  </script>
</body>
</html>
