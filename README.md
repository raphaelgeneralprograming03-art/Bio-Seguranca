
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Projeto Matriz de Biossegurança e Escudo Síncrono</title>
    <style>
        :root {
            --bg-color: #050b14;
            --panel-bg: rgba(10, 25, 45, 0.85);
            --border-color: #00ffcc;
            --accent-green: #00ff66;
            --accent-red: #ff3333;
            --accent-cyan: #00e5ff;
            --text-main: #c0d8ef;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Courier New', Courier, monospace;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            height: 100vh;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        header {
            background: linear-gradient(90deg, #021226, #0a2540, #021226);
            border-bottom: 2px solid var(--border-color);
            padding: 10px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        header h1 {
            font-size: 1.1rem;
            color: var(--accent-cyan);
            letter-spacing: 2px;
        }

        .classification {
            background: var(--accent-red);
            color: #fff;
            padding: 4px 10px;
            font-size: 0.75rem;
            font-weight: bold;
            border-radius: 3px;
            letter-spacing: 1px;
            animation: pulse-red 2s infinite;
        }

        .main-container {
            display: flex;
            flex: 1;
            gap: 15px;
            padding: 15px;
            overflow: hidden;
        }

        /* Painel de Controle Esquerdo */
        .control-panel {
            width: 340px;
            background: var(--panel-bg);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            padding: 15px;
            display: flex;
            flex-direction: column;
            gap: 15px;
            box-shadow: 0 0 15px rgba(0, 255, 204, 0.1);
        }

        .panel-section h3 {
            font-size: 0.85rem;
            color: var(--accent-cyan);
            margin-bottom: 8px;
            border-bottom: 1px solid rgba(0, 229, 255, 0.3);
            padding-bottom: 4px;
            letter-spacing: 1px;
        }

        .btn-group {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        button {
            background: rgba(0, 229, 255, 0.1);
            border: 1px solid var(--border-color);
            color: var(--text-main);
            padding: 8px 12px;
            text-align: left;
            font-size: 0.8rem;
            cursor: pointer;
            border-radius: 4px;
            transition: all 0.3s ease;
        }

        button:hover {
            background: rgba(0, 229, 255, 0.3);
            color: #fff;
            box-shadow: 0 0 8px var(--border-color);
        }

        button.active {
            background: var(--border-color);
            color: var(--bg-color);
            font-weight: bold;
        }

        button.alert-btn {
            border-color: var(--accent-red);
            background: rgba(255, 51, 51, 0.1);
            color: #ff9999;
        }

        button.alert-btn.active {
            background: var(--accent-red);
            color: #fff;
        }

        /* Área do Canvas Central */
        .viewport-container {
            flex: 1;
            background: #02060d;
            border: 1px solid var(--border-color);
            border-radius: 6px;
            display: flex;
            flex-direction: column;
            position: relative;
            overflow: hidden;
        }

        .viewport-header {
            background: rgba(0, 229, 255, 0.05);
            padding: 8px 15px;
            font-size: 0.75rem;
            display: flex;
            justify-content: space-between;
            border-bottom: 1px solid rgba(0, 229, 255, 0.2);
        }

        canvas {
            flex: 1;
            display: block;
            width: 100%;
            height: 100%;
        }

        /* Painel de Telemetria Direito */
        .telemetry-panel {
            width: 300px;
            background: var(--panel-bg);
            border: 1px solid var(--border-color);
            border-radius: 6px;
            padding: 15px;
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .metric-box {
            background: rgba(2, 12, 38, 0.6);
            border: 1px solid rgba(0, 229, 255, 0.3);
            border-radius: 4px;
            padding: 10px;
        }

        .metric-title {
            font-size: 0.7rem;
            color: var(--accent-cyan);
            margin-bottom: 4px;
        }

        .metric-value {
            font-size: 1.1rem;
            font-weight: bold;
            color: #fff;
        }

        .status-ok { color: var(--accent-green); }
        .status-alert { color: var(--accent-red); }

        @keyframes pulse-red {
            0% { opacity: 1; }
            50% { opacity: 0.4; }
            100% { opacity: 1; }
        }
    </style>
</head>
<body>

    <header>
        <h1>PROJETO MATRIZ DE BIOSSEGURANÇA E ESCUDO SÍNCRONO</h1>
        <div class="classification">SIGILO DE DEFESA NACIONAL</div>
    </header>

    <div class="main-container">
        <!-- Controles -->
        <div class="control-panel">
            <div class="panel-section">
                <h3>1. ENGENHARIA QUÍMICA</h3>
                <div class="btn-group">
                    <button id="btn-chonps" class="active" onclick="toggleFeature('chonps')">Filtragem Exclusão CHONPS</button>
                </div>
            </div>

            <div class="panel-section">
                <h3>2. FUSÃO BIOMÉTRICA</h3>
                <div class="btn-group">
                    <button id="btn-lwir" class="active" onclick="toggleFeature('lwir')">Sensores LWIR & rPPG</button>
                </div>
            </div>

            <div class="panel-section">
                <h3>3. TRANSMISSÃO NPU</h3>
                <div class="btn-group">
                    <button id="btn-npu" class="active" onclick="toggleFeature('npu')">Distribuição Paralela NPU</button>
                </div>
            </div>

            <div class="panel-section">
                <h3>4. AUTONOMIA & MESH</h3>
                <div class="btn-group">
                    <button id="btn-mesh" class="active" onclick="toggleFeature('mesh')">Malha Tática Síncrona (Mesh)</button>
                    <button id="btn-auto" class="alert-btn" onclick="toggleEmergencyMode()">Modo Automático de Emergência</button>
                </div>
            </div>

            <div class="panel-section">
                <h3>CONTROLE DE SIMULAÇÃO</h3>
                <div class="btn-group">
                    <button onclick="injectCrisis()">Simular Surto de Bioaerossol</button>
                    <button onclick="resetSimulation()">Reiniciar Sistema</button>
                </div>
            </div>
        </div>

        <!-- Visualizador Canvas -->
        <div class="viewport-container">
            <div class="viewport-header">
                <span id="view-status">STATUS: OPERAÇÃO ESTÁVEL [BLINDADO]</span>
                <span id="latency-display">LATÊNCIA SÍNCRONA: 0.4 ms</span>
            </div>
            <canvas id="simCanvas"></canvas>
        </div>

        <!-- Telemetria -->
        <div class="telemetry-panel">
            <div class="panel-section">
                <h3>TELEMETRIA EM TEMPO REAL</h3>
            </div>
            <div class="metric-box">
                <div class="metric-title">PARTÍCULAS ANALISADAS</div>
                <div class="metric-value" id="stat-particles">0 /s</div>
            </div>
            <div class="metric-box">
                <div class="metric-title">EXCLUSÕES INERTES (CHONPS)</div>
                <div class="metric-value status-ok" id="stat-excluded">0</div>
            </div>
            <div class="metric-box">
                <div class="metric-title">ESTRESSE IMUNOLÓGICO</div>
                <div class="metric-value status-ok" id="stat-stress">ESTÁVEL</div>
            </div>
            <div class="metric-box">
                <div class="metric-title">ECLUSAS / CONTRAÇÃO FROTAS</div>
                <div class="metric-value status-ok" id="stat-locks">DESBLOQUEADAS</div>
            </div>
            <div class="metric-box">
                <div class="metric-title">ESTADO DO REDE MESH</div>
                <div class="metric-value status-ok" id="stat-mesh">CONECTADO (12 NÓS)</div>
            </div>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('simCanvas');
        const ctx = canvas.getContext('2d');

        // Estados das Features
        let features = {
            chonps: true,
            lwir: true,
            npu: true,
            mesh: true,
            emergency: false
        };

        // Métricas
        let stats = {
            particlesScanned: 0,
            inertExcluded: 0,
            stressDetected: false,
            locksActive: false
        };

        // Redimensionar Canvas
        function resizeCanvas() {
            canvas.width = canvas.parentElement.clientWidth;
            canvas.height = canvas.parentElement.clientHeight - 30;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        // Partículas (Bioaerossóis & Assinaturas)
        let particles = [];
        let meshNodes = [
            { x: 100, y: 100, label: 'NÓ A-1' },
            { x: 300, y: 80, label: 'NÓ A-2' },
            { x: 500, y: 150, label: 'NÓ B-1' },
            { x: 200, y: 300, label: 'NÓ B-2' },
            { x: 400, y: 350, label: 'NÓ C-1' },
            { x: 600, y: 280, label: 'NÓ C-2' }
        ];

        function spawnParticle(isCrisis = false) {
            let isOrganic = Math.random() > 0.4;
            let isThreat = isCrisis || (isOrganic && Math.random() > 0.7);
            
            particles.push({
                x: Math.random() * canvas.width,
                y: -10,
                vx: (Math.random() - 0.5) * 2,
                vy: 2 + Math.random() * 3,
                isOrganic: isOrganic,
                isThreat: isThreat,
                radius: 3 + Math.random() * 2,
                alpha: 1
            });
        }

        function toggleFeature(featureKey) {
            features[featureKey] = !features[featureKey];
            let btn = document.getElementById(`btn-${featureKey}`);
            if (features[featureKey]) {
                btn.classList.add('active');
            } else {
                btn.classList.remove('active');
            }
        }

        function toggleEmergencyMode() {
            features.emergency = !features.emergency;
            let btn = document.getElementById('btn-auto');
            stats.locksActive = features.emergency;
            
            if (features.emergency) {
                btn.classList.add('active');
                document.getElementById('view-status').innerText = 'STATUS: MODO DE EMERGÊNCIA ATIVO [ECLUSAS TRAVADAS]';
                document.getElementById('view-status').style.color = 'var(--accent-red)';
                document.getElementById('stat-locks').innerText = 'TRAVADAS / ISOLADAS';
                document.getElementById('stat-locks').className = 'metric-value status-alert';
            } else {
                btn.classList.remove('active');
                document.getElementById('view-status').innerText = 'STATUS: OPERAÇÃO ESTÁVEL [BLINDADO]';
                document.getElementById('view-status').style.color = 'var(--text-main)';
                document.getElementById('stat-locks').innerText = 'DESBLOQUEADAS';
                document.getElementById('stat-locks').className = 'metric-value status-ok';
            }
        }

        function injectCrisis() {
            for (let i = 0; i < 40; i++) {
                spawnParticle(true);
            }
            stats.stressDetected = true;
            document.getElementById('stat-stress').innerText = 'ALERTA: FEBRE+TAQUICARDIA';
            document.getElementById('stat-stress').className = 'metric-value status-alert';
            
            setTimeout(() => {
                if (!features.emergency) {
                    stats.stressDetected = false;
                    document.getElementById('stat-stress').innerText = 'ESTÁVEL';
                    document.getElementById('stat-stress').className = 'metric-value status-ok';
                }
            }, 5000);
        }

        function resetSimulation() {
            particles = [];
            stats.particlesScanned = 0;
            stats.inertExcluded = 0;
            if (features.emergency) toggleEmergencyMode();
        }

        // Loop Principal de Renderização Canvas 2D
        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Gerar partículas continuamente
            if (Math.random() < 0.3) {
                spawnParticle();
            }

            // 1. Renderizar Malha Tática Mesh (Se ativa)
            if (features.mesh) {
                ctx.strokeStyle = 'rgba(0, 229, 255, 0.15)';
                ctx.lineWidth = 1;
                for (let i = 0; i < meshNodes.length; i++) {
                    for (let j = i + 1; j < meshNodes.length; j++) {
                        let dx = meshNodes[i].x - meshNodes[j].x;
                        let dy = meshNodes[i].y - meshNodes[j].y;
                        let dist = Math.sqrt(dx * dx + dy * dy);
                        if (dist < 250) {
                            ctx.beginPath();
                            ctx.moveTo(meshNodes[i].x, meshNodes[i].y);
                            ctx.lineTo(meshNodes[j].x, meshNodes[j].y);
                            ctx.stroke();
                        }
                    }
                }

                // Desenhar nós
                meshNodes.forEach(node => {
                    ctx.fillStyle = features.emergency ? '#ff3333' : '#00ffcc';
                    ctx.beginPath();
                    ctx.arc(node.x, node.y, 4, 0, Math.PI * 2);
                    ctx.fill();

                    ctx.fillStyle = 'rgba(0, 229, 255, 0.7)';
                    ctx.font = '9px Courier New';
                    ctx.fillText(node.label, node.x + 8, node.y + 3);
                });
            }

            // 2. Processar e Renderizar Partículas (Bioaerossóis / CHONPS)
            for (let i = particles.length - 1; i >= 0; i--) {
                let p = particles[i];
                p.x += p.vx;
                p.y += p.vy;
                stats.particlesScanned++;

                // Filtragem por Exclusão CHONPS
                if (features.chonps && !p.isOrganic) {
                    stats.inertExcluded++;
                    particles.splice(i, 1);
                    continue;
                }

                // Remover se sair da tela
                if (p.y > canvas.height) {
                    particles.splice(i, 1);
                    continue;
                }

                // Desenhar partícula
                ctx.beginPath();
                ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
                
                if (p.isThreat) {
                    ctx.fillStyle = '#ff3333';
                    ctx.shadowBlur = features.lwir ? 10 : 0;
                    ctx.shadowColor = '#ff3333';
                } else if (p.isOrganic) {
                    ctx.fillStyle = '#00ff66';
                    ctx.shadowBlur = features.lwir ? 6 : 0;
                    ctx.shadowColor = '#00ff66';
                } else {
                    ctx.fillStyle = '#888888';
                    ctx.shadowBlur = 0;
                }
                
                ctx.fill();
                ctx.shadowBlur = 0; // Reset sombra
            }

            // 3. Atualizar Telemetria Textual na UI
            document.getElementById('stat-particles').innerText = `${particles.length * 15} /s`;
            document.getElementById('stat-excluded').innerText = stats.inertExcluded;

            requestAnimationFrame(animate);
        }

        // Iniciar loop
        animate();
    </script>
</body>
</html>
