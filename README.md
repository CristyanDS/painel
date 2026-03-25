<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Painel Digital Automotivo</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: Arial, sans-serif;
    }

    body {
      background: linear-gradient(135deg, #05070c, #101722);
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      color: white;
    }

    .painel {
      width: 1000px;
      height: 560px;
      background: radial-gradient(circle at top, #111827, #05070c 70%);
      border: 3px solid #1f2937;
      border-radius: 28px;
      overflow: hidden;
      position: relative;
      box-shadow:
        0 0 25px rgba(0, 255, 120, 0.08),
        0 0 80px rgba(0, 140, 255, 0.08);
    }

    .topo-luz {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 5px;
      background: linear-gradient(to right, #00ff88, #00b7ff, #8b5cf6);
    }

    .tela {
      display: none;
      width: 100%;
      height: 100%;
      padding: 28px;
    }

    .ativa {
      display: block;
    }

    h1, h2 {
      color: #e5faff;
      margin-bottom: 14px;
      font-weight: bold;
      letter-spacing: 1px;
    }

    .subtitulo {
      color: #7dd3fc;
      font-size: 18px;
      margin-bottom: 20px;
    }

    .centro {
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
    }

    .titulo-inicial {
      font-size: 46px;
      color: #ffffff;
      margin-bottom: 18px;
      text-shadow: 0 0 20px rgba(0,255,136,0.15);
    }

    .texto-inicial {
      font-size: 22px;
      color: #cbd5e1;
      margin-bottom: 12px;
    }

    .texto-menor {
      font-size: 18px;
      color: #7dd3fc;
      margin-bottom: 30px;
    }

    .botao {
      background: linear-gradient(90deg, #00a86b, #00c896);
      color: white;
      border: none;
      padding: 12px 24px;
      border-radius: 12px;
      cursor: pointer;
      font-size: 17px;
      margin: 6px;
      transition: 0.3s;
      box-shadow: 0 0 14px rgba(0, 200, 150, 0.18);
    }

    .botao:hover {
      transform: scale(1.03);
      filter: brightness(1.1);
    }

    .cabecalho {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 18px;
    }

    .status-topo {
      display: flex;
      gap: 12px;
      font-size: 14px;
      color: #93c5fd;
    }

    .grid-principal {
      display: grid;
      grid-template-columns: 2fr 1fr;
      gap: 20px;
      margin-top: 10px;
    }

    .bloco {
      background: rgba(15, 23, 42, 0.85);
      border: 1px solid #1e293b;
      border-radius: 20px;
      padding: 20px;
      box-shadow: inset 0 0 15px rgba(255,255,255,0.02);
    }

    .velocidade-box {
      height: 230px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }

    .velocidade {
      font-size: 110px;
      font-weight: bold;
      color: #ffffff;
      text-shadow: 0 0 18px rgba(255,255,255,0.08);
      line-height: 1;
    }

    .kmh {
      font-size: 26px;
      color: #7dd3fc;
      margin-top: 10px;
    }

    .rpm-valor {
      font-size: 28px;
      color: #ffffff;
      margin-bottom: 12px;
    }

    .barra {
      width: 100%;
      height: 26px;
      background: #111827;
      border-radius: 20px;
      overflow: hidden;
      border: 1px solid #374151;
    }

    .barra-rpm {
      width: 62%;
      height: 100%;
      background: linear-gradient(to right, #00ff66, #ffee00, #ff2d2d);
      border-radius: 20px;
    }

    .blocos-info {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 18px;
      margin-top: 18px;
    }

    .mini-card {
      background: rgba(2, 6, 23, 0.85);
      border: 1px solid #1f2937;
      border-radius: 18px;
      padding: 18px;
      text-align: center;
    }

    .mini-titulo {
      font-size: 17px;
      color: #7dd3fc;
      margin-bottom: 12px;
    }

    .mini-valor {
      font-size: 34px;
      font-weight: bold;
      color: #fff;
    }

    .alertas-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
      margin-top: 20px;
    }

    .alerta {
      padding: 18px;
      border-radius: 16px;
      font-size: 20px;
      font-weight: bold;
      text-align: center;
      border: 1px solid rgba(255,255,255,0.08);
    }

    .alerta-vermelho {
      background: rgba(127, 29, 29, 0.9);
      color: #fff;
    }

    .alerta-amarelo {
      background: rgba(161, 98, 7, 0.9);
      color: #fff;
    }

    .alerta-verde {
      background: rgba(20, 83, 45, 0.9);
      color: #fff;
    }

    .alerta-azul {
      background: rgba(30, 64, 175, 0.9);
      color: #fff;
    }

    .diag-box {
      margin-top: 18px;
      background: rgba(2, 6, 23, 0.85);
      border: 1px solid #14532d;
      border-radius: 18px;
      padding: 20px;
      line-height: 2;
      font-size: 20px;
    }

    .ok {
      color: #4ade80;
      font-weight: bold;
    }

    .rodape-botoes {
      position: absolute;
      right: 25px;
      bottom: 20px;
    }

    .relogio-box {
      margin-top: 16px;
      text-align: right;
      color: #93c5fd;
      font-size: 18px;
    }
  </style>
</head>
<body>

  <div class="painel">
    <div class="topo-luz"></div>

    <!-- TELA 1 -->
    <div class="tela ativa" id="tela1">
      <div class="centro">
        <div class="titulo-inicial">PAINEL DIGITAL AUTOMOTIVO</div>
        <div class="texto-inicial">Projeto de Interface para Fiat Prêmio</div>
        <div class="texto-menor">ESP32-S3 + Display 800x480 + Sensores Automotivos</div>
        <button class="botao" onclick="mostrarTela(2)">Entrar no Painel</button>
      </div>
    </div>

    <!-- TELA 2 -->
    <div class="tela" id="tela2">
      <div class="cabecalho">
        <div>
          <h2>Tela Principal</h2>
          <div class="subtitulo">Velocidade, RPM, temperatura e combustível</div>
        </div>
        <div class="status-topo">
          <span>Wi-Fi</span>
          <span>Bluetooth</span>
          <span>Sistema ON</span>
        </div>
      </div>

      <div class="grid-principal">
        <div>
          <div class="bloco velocidade-box">
            <div class="velocidade">094</div>
            <div class="kmh">km/h</div>
          </div>

          <div class="bloco" style="margin-top:18px;">
            <div class="mini-titulo">RPM</div>
            <div class="rpm-valor">3.500 rpm</div>
            <div class="barra">
              <div class="barra-rpm"></div>
            </div>
          </div>
        </div>

        <div class="bloco">
          <div class="mini-titulo">Dados rápidos</div>

          <div class="blocos-info">
            <div class="mini-card">
              <div class="mini-titulo">Temperatura</div>
              <div class="mini-valor">91°C</div>
            </div>

            <div class="mini-card">
              <div class="mini-titulo">Combustível</div>
              <div class="mini-valor">64%</div>
            </div>

            <div class="mini-card">
              <div class="mini-titulo">Bateria</div>
              <div class="mini-valor">13.8V</div>
            </div>

            <div class="mini-card">
              <div class="mini-titulo">Hodômetro</div>
              <div class="mini-valor" style="font-size:24px;">154230 km</div>
            </div>
          </div>

          <div class="relogio-box">
            Hora: <span id="relogio">00:00:00</span>
          </div>
        </div>
      </div>

      <div class="rodape-botoes">
        <button class="botao" onclick="mostrarTela(1)">Voltar</button>
        <button class="botao" onclick="mostrarTela(3)">Próxima</button>
      </div>
    </div>

    <!-- TELA 3 -->
    <div class="tela" id="tela3">
      <div class="cabecalho">
        <div>
          <h2>Tela de Alertas</h2>
          <div class="subtitulo">Status visual dos principais avisos do carro</div>
        </div>
      </div>

      <div class="alertas-grid">
        <div class="alerta alerta-vermelho">ÓLEO — NORMAL</div>
        <div class="alerta alerta-vermelho">BATERIA — 13.8V</div>
        <div class="alerta alerta-amarelo">TEMPERATURA — ATENÇÃO</div>
        <div class="alerta alerta-azul">FAROL ALTO — DESLIGADO</div>
        <div class="alerta alerta-verde">SETA ESQUERDA — OK</div>
        <div class="alerta alerta-verde">SETA DIREITA — OK</div>
      </div>

      <div class="rodape-botoes">
        <button class="botao" onclick="mostrarTela(2)">Voltar</button>
        <button class="botao" onclick="mostrarTela(4)">Próxima</button>
      </div>
    </div>

    <!-- TELA 4 -->
    <div class="tela" id="tela4">
      <div class="cabecalho">
        <div>
          <h2>Informações Extras</h2>
          <div class="subtitulo">Detalhes complementares do sistema</div>
        </div>
      </div>

      <div class="blocos-info" style="grid-template-columns:1fr 1fr; margin-top:25px;">
        <div class="mini-card">
          <div class="mini-titulo">Modo de condução</div>
          <div class="mini-valor" style="font-size:28px;">Normal</div>
        </div>

        <div class="mini-card">
          <div class="mini-titulo">Rede</div>
          <div class="mini-valor" style="font-size:28px;">Conectada</div>
        </div>

        <div class="mini-card">
          <div class="mini-titulo">Processador</div>
          <div class="mini-valor" style="font-size:28px;">ESP32-S3</div>
        </div>

        <div class="mini-card">
          <div class="mini-titulo">Resolução</div>
          <div class="mini-valor" style="font-size:28px;">800x480</div>
        </div>
      </div>

      <div class="rodape-botoes">
        <button class="botao" onclick="mostrarTela(3)">Voltar</button>
        <button class="botao" onclick="mostrarTela(5)">Próxima</button>
      </div>
    </div>

    <!-- TELA 5 -->
    <div class="tela" id="tela5">
      <div class="cabecalho">
        <div>
          <h2>Tela de Diagnóstico</h2>
          <div class="subtitulo">Verificação geral do sistema</div>
        </div>
      </div>

      <div class="diag-box">
        <p><strong>Status do sistema:</strong> <span class="ok">FUNCIONANDO</span></p>
        <p><strong>Display:</strong> <span class="ok">OK</span></p>
        <p><strong>Backlight:</strong> <span class="ok">OK</span></p>
        <p><strong>Leitura de RPM:</strong> <span class="ok">OK</span></p>
        <p><strong>Leitura de temperatura:</strong> <span class="ok">OK</span></p>
        <p><strong>Leitura de combustível:</strong> <span class="ok">OK</span></p>
        <p><strong>Comunicação com sensores:</strong> <span class="ok">OK</span></p>
      </div>

      <div class="rodape-botoes">
        <button class="botao" onclick="mostrarTela(4)">Voltar</button>
        <button class="botao" onclick="mostrarTela(1)">Voltar ao Início</button>
      </div>
    </div>
  </div>

  <script>
    function mostrarTela(numero) {
      const telas = document.querySelectorAll(".tela");
      telas.forEach(tela => tela.classList.remove("ativa"));
      document.getElementById("tela" + numero).classList.add("ativa");
    }

    function atualizarRelogio() {
      const agora = new Date();
      const horas = String(agora.getHours()).padStart(2, "0");
      const minutos = String(agora.getMinutes()).padStart(2, "0");
      const segundos = String(agora.getSeconds()).padStart(2, "0");

      const relogio = document.getElementById("relogio");
      if (relogio) {
        relogio.textContent = `${horas}:${minutos}:${segundos}`;
      }
    }

    setInterval(atualizarRelogio, 1000);
    atualizarRelogio();
  </script>

</body>
</html>
