<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Misión Espacial: Notación Científica</title>
    <style>
        :root {
            --bg-color: #0b0d1b;
            --card-bg: #161b33;
            --accent-blue: #00d2ff;
            --accent-green: #00e676;
            --accent-red: #ff5252;
            --accent-gold: #ffd700;
            --text-color: #e0e6ed;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }

        .container {
            max-width: 800px;
            width: 100%;
        }

        #hud {
            display: none;
            justify-content: space-between;
            background-color: rgba(0, 210, 255, 0.1);
            border: 1px solid var(--accent-blue);
            padding: 15px 25px;
            border-radius: 10px;
            margin-bottom: 20px;
            font-size: 1.2rem;
            font-weight: bold;
        }

        .stat span {
            color: var(--accent-gold);
        }

        .stat-lives span {
            color: var(--accent-red);
        }

        .stat-time span {
            color: var(--accent-blue);
        }

        .screen {
            display: none;
            background-color: var(--card-bg);
            border-radius: 12px;
            padding: 30px;
            box-shadow: 0 4px 20px rgba(0, 210, 255, 0.15);
            border: 1px solid rgba(0, 210, 255, 0.3);
            animation: fadeIn 0.5s ease-in-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .screen h2 {
            color: var(--accent-blue);
            margin-top: 0;
            border-bottom: 2px solid rgba(0, 210, 255, 0.3);
            padding-bottom: 10px;
        }

        .points-badge {
            float: right;
            background: rgba(255, 215, 0, 0.2);
            color: var(--accent-gold);
            padding: 5px 10px;
            border-radius: 5px;
            font-size: 0.9rem;
            border: 1px solid var(--accent-gold);
        }

        .question {
            margin-bottom: 20px;
            background-color: rgba(255, 255, 255, 0.05);
            padding: 15px;
            border-radius: 8px;
        }

        input[type="text"], select, textarea {
            width: 100%;
            padding: 12px;
            margin-top: 10px;
            border-radius: 6px;
            border: 1px solid #2d3748;
            background-color: #0d1117;
            color: #fff;
            box-sizing: border-box;
            font-size: 1rem;
        }

        .help-text {
            font-size: 0.85rem;
            color: #a0aec0;
            margin-top: 8px;
            display: block;
            line-height: 1.4;
        }

        button {
            background: linear-gradient(135deg, #00d2ff, #3a7bd5);
            color: white;
            border: none;
            padding: 15px 20px;
            border-radius: 6px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
            transition: transform 0.2s, box-shadow 0.2s;
            margin-top: 10px;
        }

        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 210, 255, 0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 6px;
            display: none;
            font-weight: bold;
            text-align: center;
        }

        .feedback.correct {
            background-color: rgba(0, 230, 118, 0.2);
            color: var(--accent-green);
            border: 1px solid var(--accent-green);
        }

        .feedback.incorrect {
            background-color: rgba(255, 82, 82, 0.2);
            color: var(--accent-red);
            border: 1px solid var(--accent-red);
        }

        .tutorial-content p {
            line-height: 1.6;
        }

        .tutorial-content ul {
            list-style-type: none;
            padding-left: 0;
        }

        .tutorial-content li {
            margin-bottom: 12px;
            padding-left: 15px;
            border-left: 3px solid var(--accent-blue);
        }

        .victory-screen {
            text-align: center;
        }

        .victory-screen h1 {
            color: var(--accent-green);
            font-size: 2.5rem;
        }
    </style>
</head>
<body>

<div class="container">
    
    <!-- BARRA DE ESTADO (HUD) -->
    <div id="hud">
        <div class="stat">Puntos: <span id="hud-score">0</span></div>
        <div class="stat stat-lives">Vidas: <span id="hud-lives">3</span></div>
        <div class="stat stat-time">Tiempo: <span id="hud-time">60</span>s</div>
    </div>

    <!-- PANTALLA: TUTORIAL -->
    <div id="tutorial" class="screen" style="display: block;">
        <h2>MISIÓN: SALVAR LA TIERRA</h2>
        <div class="tutorial-content">
            <p><strong>Bienvenido a bordo, Cadete Espacial</strong></p>
            <p>Para completar esta misión y salvar la Tierra, deberás atravesar 4 retos utilizando tu dominio de la <strong>Notación Científica</strong>.</p>
            <ul>
                <li><strong>Tiempo:</strong> Cada reto tiene un límite de tiempo. Si llega a 0, pierdes una vida.</li>
                <li><strong>Vidas:</strong> Tienes 3 vidas por nivel. Si pierdes las 3 vidas, serás penalizado y devuelto al reto anterior.</li>
                <li><strong>Puntos:</strong> Obtendrás más puntos en los retos de mayor dificultad.</li>
                <li><strong>Escritura del exponente:</strong> Usa la letra "x" para multiplicar. Para el exponente elevado puedes usar el símbolo "^" presionando las teclas (Alt + 94) en tu teclado. Si se te dificulta, puedes escribir los números seguidos sin el símbolo. El sistema aceptará ambas formas. Ejemplo: 3.5x10^4 o 3.5x104.</li>
            </ul>
            <button onclick="startGame()">INICIAR MISIÓN</button>
        </div>
    </div>

    <!-- RETO 1: CONVERSIÓN -->
    <div id="reto1" class="screen">
        <h2>Reto 1: Conversión <span class="points-badge">100 pts</span></h2>
        <p>Convierte las siguientes magnitudes a notación científica estándar.</p>
        
        <div class="question">
            <label><strong>1. Distancia de la Tierra al Sol:</strong> 149.600.000 km</label>
            <input type="text" id="r1_1" placeholder="Ejemplo: 1.496x10^8 o 1.496x108">
            <span class="help-text">Recuerda: El coeficiente debe estar entre 1 y 9.99... Puedes usar (Alt + 94) para el símbolo ^ o escribirlo de corrido.</span>
        </div>

        <div class="question">
            <label><strong>2. Tamaño de una partícula de polvo:</strong> 0,000002 m</label>
            <input type="text" id="r1_2" placeholder="Ejemplo: 2x10^-6 o 2x10-6">
        </div>

        <button onclick="validarReto1()">Validar Reto 1</button>
        <div id="fb1" class="feedback"></div>
    </div>

    <!-- RETO 2: COMPARACIÓN -->
    <div id="reto2" class="screen">
        <h2>Reto 2: Comparación de Magnitudes <span class="points-badge">150 pts</span></h2>
        <p>Determina la relación de orden y fundamenta tu respuesta.</p>

        <div class="question">
            <label><strong>Compara:</strong> 3.2 x 10^5 km  [ ? ]  1.8 x 10^6 km</label>
            <select id="r2_1">
                <option value="">-- Selecciona el símbolo --</option>
                <option value="<">Menor que (<)</option>
                <option value=">">Mayor que (>)</option>
                <option value="=">Igual a (=)</option>
            </select>
        </div>

        <div class="question">
            <label><strong>Justificación Matemática:</strong></label>
            <textarea id="r2_just" rows="3" placeholder="Explica por qué... (Pista: habla de los exponentes)."></textarea>
            <span class="help-text">Debes escribir al menos 15 caracteres para que el sistema apruebe tu justificación.</span>
        </div>

        <button onclick="validarReto2()">Validar Reto 2</button>
        <div id="fb2" class="feedback"></div>
    </div>

    <!-- RETO 3: DETECTOR DE ERRORES -->
    <div id="reto3" class="screen">
        <h2>Reto 3: Detector de Errores <span class="points-badge">300 pts</span></h2>
        <p>La computadora de la nave falló. Encuentra el error y corrígelo.</p>

        <div class="question">
            <p><strong>Reporte con error:</strong> "0,0000045 = 45 x 10^-6"</p>
            <label><strong>1. Escribe la respuesta corregida:</strong></label>
            <input type="text" id="r3_1" placeholder="Ejemplo: 4.5x10^-6 o 4.5x10-6">
        </div>

        <div class="question">
            <label><strong>2. Sustentación (¿Por qué 45 está mal?):</strong></label>
            <textarea id="r3_just" rows="3" placeholder="Explica la regla del coeficiente (a)..."></textarea>
        </div>

        <button onclick="validarReto3()">Validar Reto 3</button>
        <div id="fb3" class="feedback"></div>
    </div>

    <!-- RETO 4: OPERACIONES -->
    <div id="reto4" class="screen">
        <h2>Reto 4: Aritmética Espacial <span class="points-badge">200 pts</span></h2>
        <p>Realiza la operación matemática para ajustar la trayectoria final.</p>

        <div class="question">
            <label><strong>Calcula el producto:</strong> (3 x 10^5) x (2 x 10^3)</label>
            <input type="text" id="r4_1" placeholder="Ejemplo: 6x10^8 o 6x108">
            <span class="help-text">Opera los coeficientes y suma los exponentes.</span>
        </div>

        <button onclick="validarReto4()">Validar Reto Final</button>
        <div id="fb4" class="feedback"></div>
    </div>

    <!-- PANTALLA: VICTORIA -->
    <div id="victory" class="screen victory-screen">
        <h1>¡MISIÓN CUMPLIDA!</h1>
        <p>Felicidades Cadete. Has salvado la Tierra aplicando exitosamente la Notación Científica.</p>
        <h2 style="border:none; font-size: 2rem;">Puntuación Final: <span id="final-score-text" style="color:var(--accent-gold)">0</span> pts</h2>
        <p>Has demostrado que dominas los Resultados de Aprendizaje (RAA1 y RAA3).</p>
        <button onclick="location.reload()" style="max-width: 300px;">Jugar de nuevo</button>
    </div>

</div>

<script>
    // ESTADO DEL JUEGO
    let currentLevel = 1;
    let lives = 3;
    let score = 0;
    let time = 0;
    let timerId = null;

    // CONFIGURACIÓN DE NIVELES (Tiempo y Puntos según dificultad)
    const levelData = {
        1: { time: 60, points: 100 },
        2: { time: 60, points: 150 },
        3: { time: 120, points: 300 },
        4: { time: 90, points: 200 }
    };

    // INICIAR JUEGO
    function startGame() {
        document.getElementById('tutorial').style.display = 'none';
        document.getElementById('hud').style.display = 'flex';
        loadLevel(1);
    }

    // CARGAR NIVEL
    function loadLevel(level) {
        currentLevel = level;
        lives = 3;
        time = levelData[level].time;
        
        document.querySelectorAll('.screen').forEach(s => s.style.display = 'none');
        document.getElementById(`reto${level}`).style.display = 'block';
        
        document.getElementById(`fb${level}`).style.display = 'none';
        
        updateHUD();
        startTimer();
    }

    // ACTUALIZAR INTERFAZ (HUD)
    function updateHUD() {
        document.getElementById('hud-time').innerText = time;
        document.getElementById('hud-lives').innerText = lives;
        document.getElementById('hud-score').innerText = score;
    }

    // TEMPORIZADOR
    function startTimer() {
        clearInterval(timerId);
        timerId = setInterval(() => {
            time--;
            updateHUD();
            if (time <= 0) {
                clearInterval(timerId);
                processMistake("Se agotó el tiempo.");
            }
        }, 1000);
    }

    // LIMPIAR ENTRADAS: Pone en minúscula, quita espacios, cambia coma por punto y ELIMINA el símbolo ^ para validar fácilmente
    function cleanInput(str) {
        return str.toLowerCase().replace(/\s+/g, '').replace(',', '.').replace('^', '');
    }

    // PROCESAR RESPUESTA INCORRECTA O TIEMPO AGOTADO
    function processMistake(mensajeError) {
        lives--;
        updateHUD();
        const fb = document.getElementById(`fb${currentLevel}`);
        
        if (lives > 0) {
            fb.className = 'feedback incorrect';
            fb.innerHTML = `Incorrecto. ${mensajeError}<br>Te quedan ${lives} vidas.`;
            fb.style.display = 'block';
            
            if(time <= 0) {
                time = levelData[currentLevel].time;
                startTimer();
            }
        } else {
            clearInterval(timerId);
            alert(`TE QUEDASTE SIN VIDAS. \nPenalización: Regresas al nivel anterior.`);
            
            let prevLevel = Math.max(1, currentLevel - 1);
            loadLevel(prevLevel);
        }
    }

    // PROCESAR RESPUESTA CORRECTA
    function processSuccess() {
        clearInterval(timerId);
        const fb = document.getElementById(`fb${currentLevel}`);
        const gainedPoints = levelData[currentLevel].points;
        score += gainedPoints;
        updateHUD();

        fb.className = 'feedback correct';
        fb.innerHTML = `Correcto. Has ganado ${gainedPoints} puntos. Preparando salto espacial...`;
        fb.style.display = 'block';

        setTimeout(() => {
            if (currentLevel < 4) {
                loadLevel(currentLevel + 1);
            } else {
                showVictory();
            }
        }, 2500);
    }

    // ------------- VALIDACIONES DE CADA RETO -------------

    function validarReto1() {
        const r1 = cleanInput(document.getElementById('r1_1').value);
        const r2 = cleanInput(document.getElementById('r1_2').value);
        
        // Al quitar el símbolo ^ en la función cleanInput, solo necesitamos validar el texto de corrido
        const isOk1 = r1 === '1.496x108' || r1 === '1.496*108';
        const isOk2 = r2 === '2x10-6' || r2 === '2*10-6';

        if (isOk1 && isOk2) {
            processSuccess();
        } else {
            processMistake("Valores incorrectos. Revisa el desplazamiento de la coma y el signo del exponente.");
        }
    }

    function validarReto2() {
        const sim = document.getElementById('r2_1').value;
        const just = document.getElementById('r2_just').value.trim();
        
        if (sim === '<' && just.length >= 15) {
            processSuccess();
        } else {
            processMistake("Revisa el símbolo de comparación o asegúrate de escribir una justificación válida.");
        }
    }

    function validarReto3() {
        const val = cleanInput(document.getElementById('r3_1').value);
        const just = document.getElementById('r3_just').value.trim();
        
        const isOk = val === '4.5x10-6' || val === '4.5*10-6';

        if (isOk && just.length >= 15) {
            processSuccess();
        } else {
            processMistake("El número corregido es incorrecto o te falta argumentar por qué el 45 incumple la regla.");
        }
    }

    function validarReto4() {
        const val = cleanInput(document.getElementById('r4_1').value);
        const isOk = val === '6x108' || val === '6*108';

        if (isOk) {
            processSuccess();
        } else {
            processMistake("Revisa tu multiplicación. Opera los coeficientes (3 por 2) y suma los exponentes (5+3).");
        }
    }

    // PANTALLA FINAL
    function showVictory() {
        document.querySelectorAll('.screen').forEach(s => s.style.display = 'none');
        document.getElementById('hud').style.display = 'none';
        document.getElementById('victory').style.display = 'block';
        document.getElementById('final-score-text').innerText = score;
    }
</script>

</body>
</html>
