<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mision: Salvar la Tierra con Notacion Cientifica</title>
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

        .stat span { color: var(--accent-gold); }
        .stat-lives span { color: var(--accent-red); }
        .stat-time span { color: var(--accent-blue); }
        .stat-player { color: var(--accent-green); }

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

        .button-secondary {
            background: linear-gradient(135deg, #4caf50, #2e7d32);
            margin-top: 20px;
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

        .tutorial-content p { line-height: 1.6; }
        .tutorial-content ul { list-style-type: none; padding-left: 0; }
        .tutorial-content li { margin-bottom: 12px; padding-left: 15px; border-left: 3px solid var(--accent-blue); }
        .victory-screen { text-align: center; }
        .victory-screen h1 { color: var(--accent-green); font-size: 2.5rem; }
    </style>
</head>
<body>

<div class="container">
    
    <!-- BARRA DE ESTADO (HUD) -->
    <div id="hud">
        <div class="stat stat-player" id="hud-player">Jugador 1</div>
        <div class="stat">Puntos: <span id="hud-score">0</span></div>
        <div class="stat stat-lives">Vidas: <span id="hud-lives">3</span></div>
        <div class="stat stat-time">Tiempo: <span id="hud-time">60</span>s</div>
    </div>

    <!-- PANTALLA: TUTORIAL -->
    <div id="tutorial" class="screen" style="display: block;">
        <h2>MISION: SALVAR LA TIERRA</h2>
        <div class="tutorial-content">
            <p><strong>Manual de Operaciones Espaciales</strong></p>
            <p>Para completar esta mision, deberas resolver 4 retos utilizando tus conocimientos en Notacion Cientifica. El sistema validara tanto tus respuestas numericas como tus justificaciones.</p>
            <ul>
                <li><strong>Requisitos de conocimiento:</strong> Debes saber convertir numeros decimales a notacion cientifica, conocer la regla del coeficiente (debe ser mayor o igual a 1 y menor que 10) y aplicar las leyes de los exponentes.</li>
                <li><strong>Tiempo y Penalizaciones:</strong> Cada reto tiene un limite de tiempo y cuentas con 3 vidas. Si pierdes las 3 vidas, seras devuelto al reto anterior.</li>
                <li><strong>Como escribir las respuestas:</strong> Usa la letra "x" minuscula para indicar multiplicacion. Para escribir el exponente, puedes presionar (Alt + 94) para obtener el simbolo ^, o simplemente escribir los numeros seguidos. El sistema entendera ambas formas.</li>
                <li><strong>Ejemplo de escritura:</strong> Para escribir 8.5 multiplicado por 10 a la potencia de 4, puedes escribir <strong>8.5x10^4</strong> o simplemente <strong>8.5x104</strong>.</li>
            </ul>
            <button onclick="startGame(1)">MODO 1 JUGADOR</button>
            <button class="button-secondary" onclick="startGame(2)">MODO 2 JUGADORES (COMPETENCIA POR TURNOS)</button>
        </div>
    </div>

    <!-- PANTALLA: TRANSICION JUGADOR 2 -->
    <div id="turn-transition" class="screen victory-screen">
        <h2>Turno del Jugador 2</h2>
        <p>El Jugador 1 ha finalizado su mision.</p>
        <p>Jugador 2, preparate para iniciar tu recorrido y superar la puntuacion.</p>
        <button onclick="startPlayer2()">INICIAR TURNO JUGADOR 2</button>
    </div>

    <!-- RETO 1: CONVERSION -->
    <div id="reto1" class="screen">
        <h2>Reto 1: Conversion de Datos <span class="points-badge">100 pts</span></h2>
        <p>Convierte las siguientes magnitudes a notacion cientifica estandar.</p>
        
        <div class="question">
            <label><strong>1. Distancia de la Tierra al Sol:</strong> 149.600.000 km</label>
            <input type="text" id="r1_1" placeholder="Ejemplo: 9.1x10^5 o 9.1x105">
            <span class="help-text">Asegurate de posicionar correctamente la coma decimal y definir el exponente positivo.</span>
        </div>

        <div class="question">
            <label><strong>2. Tamano de una particula de polvo:</strong> 0,000002 m</label>
            <input type="text" id="r1_2" placeholder="Ejemplo: 4.8x10^-3 o 4.8x10-3">
            <span class="help-text">Recuerda la direccion del exponente para cantidades microscopicas.</span>
        </div>

        <button onclick="validarReto1()">Validar Reto 1</button>
        <div id="fb1" class="feedback"></div>
    </div>

    <!-- RETO 2: COMPARACION -->
    <div id="reto2" class="screen">
        <h2>Reto 2: Analisis de Magnitudes <span class="points-badge">150 pts</span></h2>
        <p>Determina la relacion de orden y fundamenta tu respuesta.</p>

        <div class="question">
            <label><strong>Compara las siguientes cantidades:</strong> 3.2 x 10^5 km  [ ? ]  1.8 x 10^6 km</label>
            <select id="r2_1">
                <option value="">-- Selecciona el simbolo --</option>
                <option value="<">Menor que (<)</option>
                <option value=">">Mayor que (>)</option>
                <option value="=">Igual a (=)</option>
            </select>
        </div>

        <div class="question">
            <label><strong>Justificacion Matematica:</strong></label>
            <textarea id="r2_just" rows="3" placeholder="Explica detalladamente en que aspecto te fijaste para determinar el orden de las magnitudes..."></textarea>
            <span class="help-text">La computadora requiere un minimo de 15 caracteres para validar tu justificacion.</span>
        </div>

        <button onclick="validarReto2()">Validar Reto 2</button>
        <div id="fb2" class="feedback"></div>
    </div>

    <!-- RETO 3: DETECTOR DE ERRORES -->
    <div id="reto3" class="screen">
        <h2>Reto 3: Detector de Errores <span class="points-badge">300 pts</span></h2>
        <p>La computadora de navegacion arrojo un error de calculo. Encuentra el fallo conceptual y corrigelo.</p>

        <div class="question">
            <p><strong>Reporte defectuoso:</strong> "0,0000045 = 45 x 10^-6"</p>
            <label><strong>1. Escribe la expresion en Notacion Cientifica estandar:</strong></label>
            <input type="text" id="r3_1" placeholder="Ejemplo: 1.2x10^-4 o 1.2x10-4">
        </div>

        <div class="question">
            <label><strong>2. Sustentacion del error detectado:</strong></label>
            <textarea id="r3_just" rows="3" placeholder="Explica matematicamente por que el coeficiente 45 viola la estructura normativa..."></textarea>
        </div>

        <button onclick="validarReto3()">Validar Reto 3</button>
        <div id="fb3" class="feedback"></div>
    </div>

    <!-- RETO 4: OPERACIONES -->
    <div id="reto4" class="screen">
        <h2>Reto 4: Aritmetica Espacial <span class="points-badge">200 pts</span></h2>
        <p>Realiza la operacion matematica para ajustar la trayectoria final.</p>

        <div class="question">
            <label><strong>Calcula el producto de las trayectorias:</strong> (3 x 10^5) x (2 x 10^3)</label>
            <input type="text" id="r4_1" placeholder="Ejemplo: 5.5x10^7 o 5.5x107">
            <span class="help-text">Procede multiplicando los coeficientes y aplicando la ley de exponentes para bases iguales.</span>
        </div>

        <button onclick="validarReto4()">Validar Reto Final</button>
        <div id="fb4" class="feedback"></div>
    </div>

    <!-- PANTALLA: VICTORIA / RESULTADOS -->
    <div id="victory" class="screen victory-screen">
        <h1>MISION FINALIZADA</h1>
        <p>Los reportes han sido enviados a la base.</p>
        <div id="single-player-result" style="display:none;">
            <h2 style="border:none; font-size: 2rem;">Puntuacion Final: <span id="final-score-text" style="color:var(--accent-gold)">0</span> pts</h2>
        </div>
        <div id="multiplayer-result" style="display:none; text-align: left; background: rgba(0,0,0,0.2); padding: 20px; border-radius: 10px; margin-bottom: 20px;">
            <h3 style="color: var(--accent-blue);">Resultados de la Competencia</h3>
            <p><strong>Jugador 1:</strong> <span id="p1-final-score">0</span> pts</p>
            <p><strong>Jugador 2:</strong> <span id="p2-final-score">0</span> pts</p>
            <h2 id="winner-text" style="color: var(--accent-green); text-align: center; border:none; margin-top: 20px;"></h2>
        </div>
        <button onclick="location.reload()" style="max-width: 300px;">Jugar de nuevo</button>
    </div>

</div>

<script>
    // ESTADO DEL JUEGO
    let currentLevel = 1;
    let numPlayers = 1;
    let currentPlayer = 1;
    
    let scores = { 1: 0, 2: 0 };
    let lives = 3;
    let time = 0;
    let timerId = null;

    // CONFIGURACION DE NIVELES
    const levelData = {
        1: { time: 60, points: 100 },
        2: { time: 60, points: 150 },
        3: { time: 120, points: 300 },
        4: { time: 90, points: 200 }
    };

    function startGame(players) {
        numPlayers = players;
        currentPlayer = 1;
        document.getElementById('tutorial').style.display = 'none';
        document.getElementById('hud').style.display = 'flex';
        
        if (numPlayers === 1) {
            document.getElementById('hud-player').style.display = 'none';
        } else {
            document.getElementById('hud-player').style.display = 'block';
            document.getElementById('hud-player').innerText = 'Jugador 1';
        }
        
        loadLevel(1);
    }

    function startPlayer2() {
        currentPlayer = 2;
        lives = 3;
        document.getElementById('turn-transition').style.display = 'none';
        document.getElementById('hud').style.display = 'flex';
        document.getElementById('hud-player').innerText = 'Jugador 2';
        
        // Limpiar inputs
        document.querySelectorAll('input[type="text"], textarea').forEach(input => input.value = '');
        document.querySelectorAll('select').forEach(select => select.value = '');
        
        loadLevel(1);
    }

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

    function updateHUD() {
        document.getElementById('hud-time').innerText = time;
        document.getElementById('hud-lives').innerText = lives;
        document.getElementById('hud-score').innerText = scores[currentPlayer];
    }

    function startTimer() {
        clearInterval(timerId);
        timerId = setInterval(() => {
            time--;
            updateHUD();
            if (time <= 0) {
                clearInterval(timerId);
                processMistake("Se agoto el tiempo.");
            }
        }, 1000);
    }

    function cleanInput(str) {
        return str.toLowerCase().replace(/\s+/g, '').replace(',', '.').replace('^', '');
    }

    function processMistake(mensajeError) {
        lives--;
        updateHUD();
        const fb = document.getElementById(`fb${currentLevel}`);
        
        if (lives > 0) {
            fb.className = 'feedback incorrect';
            fb.innerHTML = `Respuesta incorrecta o incompleta. ${mensajeError}<br>Te quedan ${lives} vidas.`;
            fb.style.display = 'block';
            
            if(time <= 0) {
                time = levelData[currentLevel].time;
                startTimer();
            }
        } else {
            clearInterval(timerId);
            alert(`SISTEMA BLOQUEADO. Te quedaste sin vidas.\nPenalizacion: Regresas al nivel anterior.`);
            
            lives = 3;
            let prevLevel = Math.max(1, currentLevel - 1);
            
            // Limpiar inputs del nivel actual
            document.getElementById(`fb${currentLevel}`).style.display = 'none';
            loadLevel(prevLevel);
        }
    }

    function processSuccess() {
        clearInterval(timerId);
        const fb = document.getElementById(`fb${currentLevel}`);
        const gainedPoints = levelData[currentLevel].points;
        scores[currentPlayer] += gainedPoints;
        updateHUD();

        fb.className = 'feedback correct';
        fb.innerHTML = `Procedimiento validado. Has ganado ${gainedPoints} puntos. Avanzando a la siguiente fase...`;
        fb.style.display = 'block';

        setTimeout(() => {
            if (currentLevel < 4) {
                loadLevel(currentLevel + 1);
            } else {
                endPlayerTurn();
            }
        }, 2500);
    }

    function endPlayerTurn() {
        document.querySelectorAll('.screen').forEach(s => s.style.display = 'none');
        document.getElementById('hud').style.display = 'none';

        if (numPlayers === 2 && currentPlayer === 1) {
            document.getElementById('turn-transition').style.display = 'block';
        } else {
            showVictory();
        }
    }

    // VALIDACIONES
    function validarReto1() {
        const r1 = cleanInput(document.getElementById('r1_1').value);
        const r2 = cleanInput(document.getElementById('r1_2').value);
        
        const isOk1 = r1 === '1.496x108' || r1 === '1.496*108';
        const isOk2 = r2 === '2x10-6' || r2 === '2*10-6';

        if (isOk1 && isOk2) {
            processSuccess();
        } else {
            processMistake("Revisa el desplazamiento de la coma y los signos de los exponentes.");
        }
    }

    function validarReto2() {
        const sim = document.getElementById('r2_1').value;
        const just = document.getElementById('r2_just').value.trim();
        
        if (sim === '<' && just.length >= 15) {
            processSuccess();
        } else {
            processMistake("Verifica el simbolo de comparacion o asegurate de escribir una justificacion matematica valida.");
        }
    }

    function validarReto3() {
        const val = cleanInput(document.getElementById('r3_1').value);
        const just = document.getElementById('r3_just').value.trim();
        
        const isOk = val === '4.5x10-6' || val === '4.5*10-6';

        if (isOk && just.length >= 15) {
            processSuccess();
        } else {
            processMistake("El numero corregido es incorrecto o te falta argumentar detalladamente la regla del coeficiente.");
        }
    }

    function validarReto4() {
        const val = cleanInput(document.getElementById('r4_1').value);
        const isOk = val === '6x108' || val === '6*108';

        if (isOk) {
            processSuccess();
        } else {
            processMistake("Revisa la multiplicacion de los coeficientes y la suma de los exponentes.");
        }
    }

    function showVictory() {
        document.getElementById('victory').style.display = 'block';
        
        if (numPlayers === 1) {
            document.getElementById('single-player-result').style.display = 'block';
            document.getElementById('final-score-text').innerText = scores[1];
        } else {
            document.getElementById('multiplayer-result').style.display = 'block';
            document.getElementById('p1-final-score').innerText = scores[1];
            document.getElementById('p2-final-score').innerText = scores[2];
            
            const winnerText = document.getElementById('winner-text');
            if (scores[1] > scores[2]) {
                winnerText.innerText = "¡El Jugador 1 es el ganador!";
            } else if (scores[2] > scores[1]) {
                winnerText.innerText = "¡El Jugador 2 es el ganador!";
            } else {
                winnerText.innerText = "¡La competencia ha terminado en empate!";
            }
        }
    }
</script>

</body>
</html>
