<html lang="es">
<head>
<meta charset="UTF-8" />
<title>Evolet – Sombras y Juramentos</title>
<meta name="viewport" content="width=device-width, initial-scale=1" />
<!-- Fuentes -->
<link href="https://fonts.googleapis.com/css2?family=IM+Fell+English&family=UnifrakturCook:wght@700&family=Inter:wght@400;600&display=swap" rel="stylesheet">
<style>
    :root {
        --bg:#1f1a23;
        --paper:#2f2a34;
        --text:#e8e3e9;
        --muted:#8a8291;
        --accent:#b575d1;
        --accent-dark:#8f47a9;
        --card:#2b2533;
        --radius:14px;
        --transition:.35s cubic-bezier(.25,.8,.5,1);
        --shadow:0 18px 50px -10px rgba(0,0,0,.5);
    }
    * {box-sizing:border-box;}
    body {
        background: radial-gradient(circle at 40% 40%, #2c2636 0%, #1f1a23 70%);
        color: var(--text);
        font-family: 'Inter', system-ui,-apple-system,sans-serif;
        margin:0;
        padding:24px 12px;
        min-height:100vh;
    }
    h1 {
        font-family: 'UnifrakturCook', cursive;
        font-size: 2.75rem;
        margin-bottom:4px;
        text-align:center;
        letter-spacing:1px;
    }
    h2 {
        font-family: 'IM Fell English', serif;
        font-size:1.5rem;
        margin:0;
        text-align:center;
        font-weight:400;
        color:#c9bfd0;
    }
    .container {
        max-width: 1080px;
        margin: auto;
        padding: 0 16px;
    }
    .intro {
        background: linear-gradient(135deg, rgba(181,117,209,0.08), rgba(84,46,144,0.1));
        border: 1px solid rgba(181,117,209,0.2);
        padding:14px 18px;
        border-radius:10px;
        margin:18px 0 28px;
        position: relative;
        display:flex;
        gap:12px;
        align-items:flex-start;
        font-size:0.95rem;
    }
    .intro::before {
        content: "⚜";
        font-size:1.6rem;
        margin-right:8px;
        color: var(--accent);
        flex-shrink:0;
    }
    .progress-wrapper {
        margin: 16px 0 6px;
        position: relative;
        height: 10px;
        background: rgba(255,255,255,0.04);
        border-radius: 6px;
        overflow:hidden;
    }
    .progress-bar {
        height:100%;
        width:0%;
        background: linear-gradient(90deg,var(--accent), var(--accent-dark));
        border-radius:6px;
        transition: width .4s ease;
    }
    .scoreboard {
        margin: 12px 0 18px;
        padding:12px;
        background: rgba(255,255,255,0.03);
        border:1px solid rgba(255,255,255,0.05);
        border-radius:10px;
        display:flex;
        gap:16px;
        flex-wrap:wrap;
        position:relative;
    }
    .score-cell {
        flex:1 1 110px;
        min-width:100px;
        background: var(--card);
        padding:10px 14px;
        border-radius:10px;
        position:relative;
        overflow:hidden;
        display:flex;
        flex-direction:column;
        align-items:center;
        gap:4px;
        border:1px solid rgba(255,255,255,0.08);
        
    }
    .score-cell.active {
        box-shadow: 0 18px 60px -8px rgba(181,117,209,.6);
        transform: scale(1.06);
    }
    .score-label {
        font-size:0.55rem;
        text-transform: uppercase;
        letter-spacing:1px;
        margin-bottom:4px;
        display:flex;
        gap:6px;
        align-items:center;
        justify-content:center;
    }
    .score-number {
        font-size:1.55rem;
        font-weight:700;
        line-height:1;
        position: relative;
        display:inline-block;
        min-width:28px;
    }
    .questions {
        display:grid;
        gap:18px;
    }
    .question {
        background: #2b2538;
        padding:18px 22px;
        border-radius:12px;
        position: relative;
        border:1px solid rgba(255,255,255,0.06);
        box-shadow: 0 22px 60px -8px rgba(0,0,0,.35);
        transition: transform var(--transition), box-shadow var(--transition);
    }
    .question.completed {
        opacity:.95;
    }
    .question-title {
        font-weight:600;
        margin-bottom:12px;
        display:flex;
        gap:8px;
        align-items:center;
    }
    .question-count {
        background: var(--accent);
        padding:6px 12px;
        border-radius:999px;
        font-size:0.65rem;
        color:#fff;
        margin-right:6px;
        flex-shrink:0;
    }
    .options {
        display:grid;
        gap:8px;
    }
    .option {
        background: rgba(255,255,255,0.03);
        border:2px solid rgba(255,255,255,0.06);
        border-radius:10px;
        padding:10px 14px;
        display:flex;
        align-items:center;
        gap:12px;
        position: relative;
        cursor:pointer;
        transition: all var(--transition);
        font-size:0.95rem;
    }
    .option input {
        display:none;
    }
    .option .radio {
        width:18px;
        height:18px;
        border:2px solid rgba(255,255,255,0.6);
        border-radius:50%;
        position: relative;
        flex-shrink:0;
        display:flex;
        align-items:center;
        justify-content:center;
        transition: all .25s ease;
    }
    .option .radio::after {
        content: "";
        width:10px;
        height:10px;
        background: var(--accent);
        border-radius:50%;
        transform: scale(0);
        transition: transform .25s ease;
    }
    .option.selected {
        border-color: var(--accent);
        background: rgba(181,117,209,0.09);
    }
    .option.selected .radio {
        border-color:#fff;
    }
    .option.selected .radio::after {
        transform: scale(1);
    }
    .option:hover {
        background: rgba(255,255,255,0.06);
    }
    .controls {
        display:flex;
        justify-content:center;
        gap:12px;
        flex-wrap:wrap;
        margin:26px 0 10px;
    }
    .btn {
        background: linear-gradient(135deg,var(--accent), var(--accent-dark));
        color:#fff;
        padding:14px 26px;
        border:none;
        cursor:pointer;
        font-weight:600;
        border-radius:50px;
        font-size:0.95rem;
        letter-spacing:1px;
        display:inline-flex;
        align-items:center;
        gap:8px;
        transition: filter .25s ease;
        position:relative;
        overflow:hidden;
    }
    .btn:active { filter:brightness(.9); }
    .btn.reset {
        background: rgba(255,255,255,0.08);
        color:#c9bfd0;
    }
    .result {
        margin-top:28px;
        padding:24px 24px 18px;
        background: linear-gradient(135deg,#3b2f53 0%, #2b2538 70%);
        border-radius:16px;
        position: relative;
        overflow:hidden;
        border:2px solid rgba(181,117,209,0.8);
        box-shadow: var(--shadow);
        display:flex;
        gap:24px;
        flex-wrap:wrap;
    }
    .badge {
        display:inline-block;
        background: #fff;
        color: #3b2f53;
        padding:8px 16px;
        border-radius:999px;
        font-weight:700;
        font-size:0.9rem;
        letter-spacing:1px;
        margin-bottom:10px;
        position: relative;
        overflow:hidden;
    }
    .profile-desc {
        font-size:1rem;
        line-height:1.5;
        margin-top:6px;
        background: rgba(255,255,255,0.04);
        padding:14px 16px;
        border-radius:10px;
    }
    .tie-notice {
        background: rgba(255,235,214,0.2);
        border-left:4px solid #d47b1f;
        padding:14px 16px;
        border-radius:8px;
        margin-bottom:12px;
        font-size:0.95rem;
    }
    .tie-buttons {
        display:flex;
        flex-wrap:wrap;
        gap:8px;
        margin-top:8px;
    }
    .tie-buttons button {
        flex:1 1 140px;
        background: rgba(255,255,255,0.08);
        border:1px solid rgba(255,255,255,0.1);
        color:#fff;
        padding:10px 12px;
        border-radius:8px;
        cursor:pointer;
        font-size:0.75rem;
        position:relative;
        transition: all .25s ease;
    }
    .tie-buttons button.selected {
        background: var(--accent);
        border-color: var(--accent-dark);
        box-shadow: 0 16px 48px -4px rgba(181,117,209,.7);
    }
    .final-tagline {
        margin-top:8px;
        font-size:0.75rem;
        color:#c9bfd0;
        font-style:italic;
    }
    .footer {
        margin:48px 0 18px;
        font-size:0.65rem;
        text-align:center;
        color:rgba(255,255,255,0.35);
    }
    .hidden { display:none !important; }
</style>
</head>
<body>

<div class="container">
    <h1>Evolet</h1>
    <h2>Sombras y Juramentos</h2>

    <div class="intro">
        <div>
            Responde con honestidad. No hay bien ni mal absoluto aquí: solo destellos de quién eres en la red de la noche, la luz y el destino. Si hay empate al final, se te presentará una pregunta de desempate para definir tu esencia.
        </div>
    </div>

    <div class="progress-wrapper" aria-label="Barra de avance">
        <div class="progress-bar" id="progress-bar"></div>
    </div>

    <div class="scoreboard" aria-label="Marcador de facciones">
        <div class="score-cell" data-key="VA">
            <div class="score-label">Inmortal ancestral</div>
            <div class="score-number" id="score-VA">0</div>
        </div>
        <div class="score-cell" data-key="CF">
            <div class="score-label">Miembro de la orden</div>
            <div class="score-number" id="score-CF">0</div>
        </div>
        <div class="score-cell" data-key="VC">
            <div class="score-label">Sanador de almas</div>
            <div class="score-number" id="score-VC">0</div>
        </div>
        <div class="score-cell" data-key="VN">
            <div class="score-label">Realeza bendita</div>
            <div class="score-number" id="score-VN">0</div>
        </div>
        <div class="score-cell" data-key="HC">
            <div class="score-label">El último eslabón</div>
            <div class="score-number" id="score-HC">0</div>
        </div>
        <div class="score-cell" data-key="MT">
            <div class="score-label">Comerciante de vidas</div>
            <div class="score-number" id="score-MT">0</div>
        </div>
        <div class="score-cell" data-key="VV">
            <div class="score-label">Tejedor de destinos</div>
            <div class="score-number" id="score-VV">0</div>
        </div>
        <div class="score-cell" data-key="VD">
            <div class="score-label">Hijo del sol</div>
            <div class="score-number" id="score-VD">0</div>
        </div>
    </div>

    <form id="test-form" autocomplete="off">
        <div class="questions">
            <!-- Pregunta 1 -->
            <div class="question" data-q="1">
                <div class="question-title">
                    <div class="question-count">1</div>
                    <div>Sueñas cómo entras en una ciudad desconocida al anochecer. Sabes que estás soñando, así que lo primero que buscas es…</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Las calles con menos personas a la vista. <strong>(VA)</strong></div>
                        <input type="radio" name="q1" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. La iglesia principal. <strong>(CF)</strong></div>
                        <input type="radio" name="q1" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Personas que ofrezcan refugio. <strong>(VC)</strong></div>
                        <input type="radio" name="q1" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. El edificio mejor iluminado. <strong>(VN)</strong></div>
                        <input type="radio" name="q1" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Cualquier alojamiento seguro y limpio. <strong>(HC)</strong></div>
                        <input type="radio" name="q1" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Los lugares donde parezca haber una celebración. <strong>(MT)</strong></div>
                        <input type="radio" name="q1" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Un lugar alto. <strong>(VV)</strong></div>
                        <input type="radio" name="q1" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. La calle principal, o un espacio concurrido bien iluminado. <strong>(VD)</strong></div>
                        <input type="radio" name="q1" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 2 -->
            <div class="question" data-q="2">
                <div class="question-title">
                    <div class="question-count">2</div>
                    <div>Una figura encapuchada te ofrece un pergamino sellado con cera roja. Lo tomas y…</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Reconoces de inmediato el símbolo de un pacto antiguo. <strong>(VA)</strong></div>
                        <input type="radio" name="q2" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Lo examinas buscando pistas de un objetivo. <strong>(CF)</strong></div>
                        <input type="radio" name="q2" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Lo llevas con cuidado a un sanador para comprobar si está maldito. <strong>(VC)</strong></div>
                        <input type="radio" name="q2" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Lo abres solo en presencia de otros de tu estatus. <strong>(VN)</strong></div>
                        <input type="radio" name="q2" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Lo vendes o intercambias, no quieres problemas. <strong>(HC)</strong></div>
                        <input type="radio" name="q2" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Lo usas para negociar un favor a cambio. <strong>(MT)</strong></div>
                        <input type="radio" name="q2" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Lo estudias buscando visiones o señales ocultas. <strong>(VV)</strong></div>
                        <input type="radio" name="q2" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. Lo guardas para revisarlo con calma a plena luz del día. <strong>(VD)</strong></div>
                        <input type="radio" name="q2" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 3 -->
            <div class="question" data-q="3">
                <div class="question-title">
                    <div class="question-count">3</div>
                    <div>¿Qué bebida aceptarías de un extraño?</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Vino añejo con aroma a roble y sangre. <strong>(VA)</strong></div>
                        <input type="radio" name="q3" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Agua pura y fría. <strong>(CF)</strong></div>
                        <input type="radio" name="q3" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Infusión de hierbas curativas. <strong>(VC)</strong></div>
                        <input type="radio" name="q3" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Champán espumoso en copa de cristal fino. <strong>(VN)</strong></div>
                        <input type="radio" name="q3" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Sidra casera. <strong>(HC)</strong></div>
                        <input type="radio" name="q3" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Licor fuerte servido en vaso metálico. <strong>(MT)</strong></div>
                        <input type="radio" name="q3" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Té oscuro con hojas que favorecen la clarividencia. <strong>(VV)</strong></div>
                        <input type="radio" name="q3" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. Café fuerte para resistir la vigilia diurna. <strong>(VD)</strong></div>
                        <input type="radio" name="q3" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 4 -->
            <div class="question" data-q="4">
                <div class="question-title">
                    <div class="question-count">4</div>
                    <div>Encuentras un amuleto roto en un callejón. ¿Qué haces?</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Lo reconoces como una reliquia de siglos atrás y lo guardas. <strong>(VA)</strong></div>
                        <input type="radio" name="q4" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Lo llevas al arsenal de tu orden para investigarlo. <strong>(CF)</strong></div>
                        <input type="radio" name="q4" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Intentas repararlo para devolverle su poder protector. <strong>(VC)</strong></div>
                        <input type="radio" name="q4" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Lo haces restaurar por un artesano de confianza. <strong>(VN)</strong></div>
                        <input type="radio" name="q4" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Lo dejas donde está, no es asunto tuyo. <strong>(HC)</strong></div>
                        <input type="radio" name="q4" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Lo vendes al mejor postor. <strong>(MT)</strong></div>
                        <input type="radio" name="q4" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Lo usas como catalizador para un ritual de visión. <strong>(VV)</strong></div>
                        <input type="radio" name="q4" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. Lo expones al sol para purificarlo. <strong>(VD)</strong></div>
                        <input type="radio" name="q4" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 5 -->
            <div class="question" data-q="5">
                <div class="question-title">
                    <div class="question-count">5</div>
                    <div>Una criatura herida aparece frente a ti.</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. La ayudas, pero solo si su linaje merece tu respeto. <strong>(VA)</strong></div>
                        <input type="radio" name="q5" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. La eliminas si representa peligro para inocentes. <strong>(CF)</strong></div>
                        <input type="radio" name="q5" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. La curas sin importar quién sea. <strong>(VC)</strong></div>
                        <input type="radio" name="q5" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. La proteges y ofreces refugio. <strong>(VN)</strong></div>
                        <input type="radio" name="q5" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Llamas a alguien más para que se encargue. <strong>(HC)</strong></div>
                        <input type="radio" name="q5" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. La capturas y la llevas a un comprador. <strong>(MT)</strong></div>
                        <input type="radio" name="q5" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Lees su herida para comprender el origen del ataque. <strong>(VV)</strong></div>
                        <input type="radio" name="q5" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. La trasladas a un lugar seguro durante el día. <strong>(VD)</strong></div>
                        <input type="radio" name="q5" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 6 -->
            <div class="question" data-q="6">
                <div class="question-title">
                    <div class="question-count">6</div>
                    <div>¿Qué elemento prefieres dominar?</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Sombras. <strong>(VA)</strong></div>
                        <input type="radio" name="q6" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Acero. <strong>(CF)</strong></div>
                        <input type="radio" name="q6" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Agua. <strong>(VC)</strong></div>
                        <input type="radio" name="q6" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Fuego. <strong>(VN)</strong></div>
                        <input type="radio" name="q6" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Tierra. <strong>(HC)</strong></div>
                        <input type="radio" name="q6" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Humo. <strong>(MT)</strong></div>
                        <input type="radio" name="q6" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Niebla. <strong>(VV)</strong></div>
                        <input type="radio" name="q6" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. Luz. <strong>(VD)</strong></div>
                        <input type="radio" name="q6" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 7 -->
            <div class="question" data-q="7">
                <div class="question-title">
                    <div class="question-count">7</div>
                    <div>Un oráculo te ofrece una visión. ¿Qué pides ver?</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. El inicio de tu linaje. <strong>(VA)</strong></div>
                        <input type="radio" name="q7" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. El rostro de tu próximo objetivo. <strong>(CF)</strong></div>
                        <input type="radio" name="q7" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. El destino de un ser querido. <strong>(VC)</strong></div>
                        <input type="radio" name="q7" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. El futuro de tu familia. <strong>(VN)</strong></div>
                        <input type="radio" name="q7" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Tu vida dentro de diez años. <strong>(HC)</strong></div>
                        <input type="radio" name="q7" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. El momento de tu mayor ganancia. <strong>(MT)</strong></div>
                        <input type="radio" name="q7" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. El punto exacto donde tu camino se bifurcará. <strong>(VV)</strong></div>
                        <input type="radio" name="q7" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. El instante más brillante de tu vida futura. <strong>(VD)</strong></div>
                        <input type="radio" name="q7" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 8 -->
            <div class="question" data-q="8">
                <div class="question-title">
                    <div class="question-count">8</div>
                    <div>Tu relación con la luz del sol es…</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Un recuerdo lejano, sin importancia. <strong>(VA)</strong></div>
                        <input type="radio" name="q8" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Una amenaza a evitar. <strong>(CF)</strong></div>
                        <input type="radio" name="q8" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Una debilidad que aceptas con calma. <strong>(VC)</strong></div>
                        <input type="radio" name="q8" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Un lujo prohibido. <strong>(VN)</strong></div>
                        <input type="radio" name="q8" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Parte natural de tu vida. <strong>(HC)</strong></div>
                        <input type="radio" name="q8" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Una herramienta para ocultarte entre humanos. <strong>(MT)</strong></div>
                        <input type="radio" name="q8" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Un velo que te revela presagios en las sombras que proyecta. <strong>(VV)</strong></div>
                        <input type="radio" name="q8" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. Tu territorio de ventaja frente a otros vampiros. <strong>(VD)</strong></div>
                        <input type="radio" name="q8" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 9 -->
            <div class="question" data-q="9">
                <div class="question-title">
                    <div class="question-count">9</div>
                    <div>Elige un arma.</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Espada forjada con plata antigua. <strong>(VA)</strong></div>
                        <input type="radio" name="q9" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Ballesta precisa y silenciosa. <strong>(CF)</strong></div>
                        <input type="radio" name="q9" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Bastón con gemas sanadoras. <strong>(VC)</strong></div>
                        <input type="radio" name="q9" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Daga ornamentada con escudo familiar. <strong>(VN)</strong></div>
                        <input type="radio" name="q9" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Ninguna, prefieres evitar conflictos. <strong>(HC)</strong></div>
                        <input type="radio" name="q9" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Red de acero para capturas. <strong>(MT)</strong></div>
                        <input type="radio" name="q9" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Orbe de cristal para canalizar visiones. <strong>(VV)</strong></div>
                        <input type="radio" name="q9" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. Lanza corta de madera clara para maniobrar al sol. <strong>(VD)</strong></div>
                        <input type="radio" name="q9" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 10 -->
            <div class="question" data-q="10">
                <div class="question-title">
                    <div class="question-count">10</div>
                    <div>Un cazador rival te reta en público.</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Ignoras el desafío, no está a tu altura. <strong>(VA)</strong></div>
                        <input type="radio" name="q10" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Lo enfrentas de inmediato. <strong>(CF)</strong></div>
                        <input type="radio" name="q10" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Intentas disuadirlo con palabras. <strong>(VC)</strong></div>
                        <input type="radio" name="q10" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Le ofreces un trato para que se retire. <strong>(VN)</strong></div>
                        <input type="radio" name="q10" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Te retiras, no es tu pelea. <strong>(HC)</strong></div>
                        <input type="radio" name="q10" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Aceptas solo si hay una recompensa. <strong>(MT)</strong></div>
                        <input type="radio" name="q10" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Anticipas sus movimientos observando gestos y presagios. <strong>(VV)</strong></div>
                        <input type="radio" name="q10" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. Retrasas el duelo hasta el amanecer, cuando tengas ventaja. <strong>(VD)</strong></div>
                        <input type="radio" name="q10" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 11 -->
            <div class="question" data-q="11">
                <div class="question-title">
                    <div class="question-count">11</div>
                    <div>¿Qué sonido te resulta más reconfortante?</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. El latido lento y constante de un corazón dormido. <strong>(VA)</strong></div>
                        <input type="radio" name="q11" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. El crujir de una cuerda tensada en arco. <strong>(CF)</strong></div>
                        <input type="radio" name="q11" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. El murmullo del agua en una fuente. <strong>(VC)</strong></div>
                        <input type="radio" name="q11" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. El tintinear de copas en un banquete. <strong>(VN)</strong></div>
                        <input type="radio" name="q11" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. El canto de pájaros al amanecer. <strong>(HC)</strong></div>
                        <input type="radio" name="q11" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. El tintineo de monedas. <strong>(MT)</strong></div>
                        <input type="radio" name="q11" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. El susurro de hojas movidas por un viento premonitorio. <strong>(VV)</strong></div>
                        <input type="radio" name="q11" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. El bullicio de una plaza bajo la luz del día. <strong>(VD)</strong></div>
                        <input type="radio" name="q11" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 12 -->
            <div class="question" data-q="12">
                <div class="question-title">
                    <div class="question-count">12</div>
                    <div>Si pudieras viajar a un solo lugar, sería…</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Una fortaleza olvidada en lo alto de una montaña. <strong>(VA)</strong></div>
                        <input type="radio" name="q12" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Una ciudad amurallada famosa por su seguridad. <strong>(CF)</strong></div>
                        <input type="radio" name="q12" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Un santuario oculto entre bosques. <strong>(VC)</strong></div>
                        <input type="radio" name="q12" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Un castillo en plena celebración. <strong>(VN)</strong></div>
                        <input type="radio" name="q12" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Un pueblo pequeño y tranquilo. <strong>(HC)</strong></div>
                        <input type="radio" name="q12" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Un puerto donde todo se compra y vende. <strong>(MT)</strong></div>
                        <input type="radio" name="q12" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Una caverna donde se revelan visiones en las paredes. <strong>(VV)</strong></div>
                        <input type="radio" name="q12" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. Una terraza alta con vista al amanecer. <strong>(VD)</strong></div>
                        <input type="radio" name="q12" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 13 -->
            <div class="question" data-q="13">
                <div class="question-title">
                    <div class="question-count">13</div>
                    <div>Escuchas un rumor sobre ti. ¿Qué haces?</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. No lo desmientes ni lo confirmas. <strong>(VA)</strong></div>
                        <input type="radio" name="q13" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Averiguas quién lo dijo. <strong>(CF)</strong></div>
                        <input type="radio" name="q13" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Intentas que no dañe a otros. <strong>(VC)</strong></div>
                        <input type="radio" name="q13" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Lo aprovechas a tu favor. <strong>(VN)</strong></div>
                        <input type="radio" name="q13" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Lo ignoras, no vale la pena. <strong>(HC)</strong></div>
                        <input type="radio" name="q13" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Lo usas como moneda de cambio. <strong>(MT)</strong></div>
                        <input type="radio" name="q13" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Lo interpretas como un presagio sobre tu destino. <strong>(VV)</strong></div>
                        <input type="radio" name="q13" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. Lo desmientes públicamente bajo la luz del día. <strong>(VD)</strong></div>
                        <input type="radio" name="q13" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 14 -->
            <div class="question" data-q="14">
                <div class="question-title">
                    <div class="question-count">14</div>
                    <div>¿Qué don preferirías?</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Inmortalidad absoluta. <strong>(VA)</strong></div>
                        <input type="radio" name="q14" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Precisión infalible en combate. <strong>(CF)</strong></div>
                        <input type="radio" name="q14" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Curación instantánea. <strong>(VC)</strong></div>
                        <input type="radio" name="q14" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Influencia política ilimitada. <strong>(VN)</strong></div>
                        <input type="radio" name="q14" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Longevidad tranquila. <strong>(HC)</strong></div>
                        <input type="radio" name="q14" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Capacidad para rastrear cualquier criatura. <strong>(MT)</strong></div>
                        <input type="radio" name="q14" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Ver fragmentos del futuro con claridad. <strong>(VV)</strong></div>
                        <input type="radio" name="q14" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. Resistir sin daño la luz solar. <strong>(VD)</strong></div>
                        <input type="radio" name="q14" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 15 -->
            <div class="question" data-q="15">
                <div class="question-title">
                    <div class="question-count">15</div>
                    <div>Una criatura de sombras se ofrece a servirte.</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. La aceptas como parte de tu legado. <strong>(VA)</strong></div>
                        <input type="radio" name="q15" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. La usas como aliada en cacerías. <strong>(CF)</strong></div>
                        <input type="radio" name="q15" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. La liberas para que sane su propio camino. <strong>(VC)</strong></div>
                        <input type="radio" name="q15" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. La incorporas a tu guardia personal. <strong>(VN)</strong></div>
                        <input type="radio" name="q15" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. La rechazas con cautela. <strong>(HC)</strong></div>
                        <input type="radio" name="q15" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. La vendes a quien la necesite. <strong>(MT)</strong></div>
                        <input type="radio" name="q15" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. La consultas para conocer secretos velados. <strong>(VV)</strong></div>
                        <input type="radio" name="q15" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. La empleas para misiones durante el día. <strong>(VD)</strong></div>
                        <input type="radio" name="q15" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 16 -->
            <div class="question" data-q="16">
                <div class="question-title">
                    <div class="question-count">16</div>
                    <div>¿Qué harías por una reliquia valiosa?</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Esperar siglos a que vuelva a la superficie. <strong>(VA)</strong></div>
                        <input type="radio" name="q16" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Seguir su rastro sin descanso. <strong>(CF)</strong></div>
                        <input type="radio" name="q16" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Usarla para proteger vidas. <strong>(VC)</strong></div>
                        <input type="radio" name="q16" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Exhibirla como símbolo de estatus. <strong>(VN)</strong></div>
                        <input type="radio" name="q16" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Guardarla como recuerdo. <strong>(HC)</strong></div>
                        <input type="radio" name="q16" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Venderla al mejor postor. <strong>(MT)</strong></div>
                        <input type="radio" name="q16" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Interpretar su historia a través de visiones. <strong>(VV)</strong></div>
                        <input type="radio" name="q16" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. Portarla en un amuleto al sol como desafío. <strong>(VD)</strong></div>
                        <input type="radio" name="q16" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 17 -->
            <div class="question" data-q="17">
                <div class="question-title">
                    <div class="question-count">17</div>
                    <div>Cuando todo está en silencio, piensas en…</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Los siglos que has vivido. <strong>(VA)</strong></div>
                        <input type="radio" name="q17" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Las presas que esperan en la oscuridad. <strong>(CF)</strong></div>
                        <input type="radio" name="q17" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Los que necesitan tu ayuda. <strong>(VC)</strong></div>
                        <input type="radio" name="q17" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Las alianzas que mantener. <strong>(VN)</strong></div>
                        <input type="radio" name="q17" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Tu próxima comida o descanso. <strong>(HC)</strong></div>
                        <input type="radio" name="q17" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Tu próxima ganancia. <strong>(MT)</strong></div>
                        <input type="radio" name="q17" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Los símbolos que has visto en sueños. <strong>(VV)</strong></div>
                        <input type="radio" name="q17" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. El amanecer más cercano. <strong>(VD)</strong></div>
                        <input type="radio" name="q17" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 18 -->
            <div class="question" data-q="18">
                <div class="question-title">
                    <div class="question-count">18</div>
                    <div>Encuentras un diario antiguo.</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Reconoces tu propia escritura de hace siglos. <strong>(VA)</strong></div>
                        <input type="radio" name="q18" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Lo analizas para obtener información táctica. <strong>(CF)</strong></div>
                        <input type="radio" name="q18" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Lo lees buscando remedios olvidados. <strong>(VC)</strong></div>
                        <input type="radio" name="q18" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Lo añades a tu biblioteca privada. <strong>(VN)</strong></div>
                        <input type="radio" name="q18" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Lo dejas donde estaba. <strong>(HC)</strong></div>
                        <input type="radio" name="q18" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Lo vendes a un coleccionista. <strong>(MT)</strong></div>
                        <input type="radio" name="q18" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Descifras sus símbolos en busca de visiones. <strong>(VV)</strong></div>
                        <input type="radio" name="q18" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. Lo lees a plena luz para evitar trampas oscuras. <strong>(VD)</strong></div>
                        <input type="radio" name="q18" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 19 -->
            <div class="question" data-q="19">
                <div class="question-title">
                    <div class="question-count">19</div>
                    <div>¿Qué temes más?</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Olvidar quién eres. <strong>(VA)</strong></div>
                        <input type="radio" name="q19" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Fallar en tu misión. <strong>(CF)</strong></div>
                        <input type="radio" name="q19" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. No poder salvar a alguien querido. <strong>(VC)</strong></div>
                        <input type="radio" name="q19" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Perder influencia. <strong>(VN)</strong></div>
                        <input type="radio" name="q19" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Quedarte sin hogar. <strong>(HC)</strong></div>
                        <input type="radio" name="q19" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Perder una gran oportunidad. <strong>(MT)</strong></div>
                        <input type="radio" name="q19" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. No reconocer las señales del destino. <strong>(VV)</strong></div>
                        <input type="radio" name="q19" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8. Quedar atrapado bajo tierra sin ver el sol. <strong>(VD)</strong></div>
                        <input type="radio" name="q19" value="VD">
                    </label>
                </div>
            </div>

            <!-- Pregunta 20 -->
            <div class="question" data-q="20">
                <div class="question-title">
                    <div class="question-count">20</div>
                    <div>Si el amanecer se adelantara, tú…</div>
                </div>
                <div class="options">
                    <label class="option" data-value="VA">
                        <div class="radio"><div></div></div>
                        <div>1. Te ocultarías en la cripta más profunda. <strong>(VA)</strong></div>
                        <input type="radio" name="q20" value="VA">
                    </label>
                    <label class="option" data-value="CF">
                        <div class="radio"><div></div></div>
                        <div>2. Te asegurarías de que todos estén a salvo. <strong>(CF)</strong></div>
                        <input type="radio" name="q20" value="CF">
                    </label>
                    <label class="option" data-value="VC">
                        <div class="radio"><div></div></div>
                        <div>3. Protegerías a quienes no pueden huir. <strong>(VC)</strong></div>
                        <input type="radio" name="q20" value="VC">
                    </label>
                    <label class="option" data-value="VN">
                        <div class="radio"><div></div></div>
                        <div>4. Te encerrarías en tu sala privada. <strong>(VN)</strong></div>
                        <input type="radio" name="q20" value="VN">
                    </label>
                    <label class="option" data-value="HC">
                        <div class="radio"><div></div></div>
                        <div>5. Saldrías a disfrutarlo. <strong>(HC)</strong></div>
                        <input type="radio" name="q20" value="HC">
                    </label>
                    <label class="option" data-value="MT">
                        <div class="radio"><div></div></div>
                        <div>6. Aprovecharías para moverte sin ser visto. <strong>(MT)</strong></div>
                        <input type="radio" name="q20" value="MT">
                    </label>
                    <label class="option" data-value="VV">
                        <div class="radio"><div></div></div>
                        <div>7. Consultarías si esto es señal de un cambio mayor. <strong>(VV)</strong></div>
                        <input type="radio" name="q20" value="VV">
                    </label>
                    <label class="option" data-value="VD">
                        <div class="radio"><div></div></div>
                        <div>8 Lo expones al sol para purificarlo. <strong>(VD)</strong></div>
                        <input type="radio" name="q4" value="VD">
                    </label>
                </div>
            </div>
        </div>

        <div class="controls">
            <button type="button" class="btn" id="reveal">Revelar resultado</button>
            <button type="button" class="btn reset" id="reset">Reiniciar</button>
        </div>
    </form>

    <div id="output" class="result hidden" aria-live="polite">
        <!-- Resultado se inserta aquí -->
    </div>

    <div class="footer">
        © Sombras y Juramentos — Evolett Coffee. Revela tu esencia entre secretos, luces y destinos.
    </div>
</div>

<script>
    // Perfiles
    const profiles = {
        VA: {
            name: "Vampiro Ancestral",
            desc: `Tú eres de los que caminan entre siglos. Tu sombra es más antigua que muchas ciudades, y tus recuerdos se entrelazan con la historia misma. No buscas aprobación ni compañía, pues el tiempo te ha enseñado que todo llega y todo se pierde. Tu poder reside en la paciencia y en la comprensión de los ciclos eternos. Pocos pueden mirarte a los ojos sin sentir que se asoman a un abismo.`
        },
        CF: {
            name: "Cazador Formal",
            desc: `Portas un juramento tan afilado como el acero que manejas. No eres un ejecutor ciego, sino un guardián que mide cada paso, consciente de que tu misión está por encima de tu nombre. Tu vida se rige por el deber, y aunque la soledad pueda rozarte, la certeza de proteger a otros te mantiene firme. Allí donde otros ven sombras, tú ves objetivos claros.`
        },
        VC: {
            name: "Vampiro con Dones Curativos",
            desc: `Eres el susurro que calma, la mano que sana incluso cuando la oscuridad parece devorar todo. Tu existencia es una contradicción: criatura de la noche, portadora de alivio. No buscas gloria, sino alivio para quienes sufren. Muchos subestiman tu fuerza, pero tu capacidad de preservar vidas en un mundo de muerte te convierte en un faro improbable.`
        },
        VN: {
            name: "Vampiro de Familia Noble",
            desc: `La sangre que corre por tus venas es más que vida: es linaje, poder y legado. No eres simplemente un individuo; eres un representante de una historia que se extiende por generaciones. Tu presencia se anuncia antes que tus pasos, y tu palabra tiene el peso de un pacto antiguo. Mantener alianzas y preservar el prestigio es tu arte, y el mundo es tu escenario.`
        },
        HC: {
            name: "Humano Común",
            desc: `Podrías pensar que tu papel es pequeño, pero en la neutralidad hay fuerza. No te mueves por sed de poder o ansias de combate, sino por la búsqueda de estabilidad. A veces, la supervivencia no requiere colmillos ni acero, sino inteligencia y prudencia. Y aunque otros puedan verte como frágil, eres el recordatorio de lo que todos una vez fueron.`
        },
        MT: {
            name: "Mercenario y Traficante de Criaturas",
            desc: `Tu lealtad no es a una bandera, sino al contrato. Te mueves entre las sombras y las luces, vendiendo lo que otros consideran intocable. No hay criatura, reliquia o secreto que no pueda cambiar de manos si tú estás presente. Algunos te llaman oportunista, otros, visionario; lo cierto es que siempre sabes sacar ventaja, incluso en medio del caos.`
        },
        VV: {
            name: "Vampiro Vidente",
            desc: `Tu visión trasciende la simple mirada. Percibes hilos invisibles que conectan el presente con posibilidades infinitas. No vives solo en el ahora; caminas también en lo que aún no ha ocurrido. Tus palabras pueden ser advertencias o profecías, y aunque a veces te apartes del mundo, lo haces para escuchar mejor el eco del destino.`
        },
        VD: {
            name: "Vampiro Diurno",
            desc: `Has reclamado un privilegio casi imposible: la luz. Caminar bajo el sol no te priva de la noche, sino que te da acceso a dos mundos. Eres adaptable, astuto y capaz de mezclarse con humanos sin levantar sospechas. Sin embargo, esta libertad viene con el peso de elegir a qué lado servirás cuando llegue la oscuridad.`
        }
    };

    const tieBreaker = {
        prompt: `Desempate: Estás en medio de una noche sin luna, escuchas un grito en la distancia. Lo primero que haces es...`,
        options: {
            CF: "Correr hacia el sonido, arma en mano.",
            VA: "Buscar la fuente en silencio, ocultándote.",
            VC: "Preparar vendas y medicinas.",
            VN: "Enviar a tus guardias o aliados.",
            HC: "Encender una lámpara y pedir ayuda.",
            VV: "Esperar una visión que te guíe.",
            VD: "Salir inmediatamente, confiando en que el sol te protegerá al volver.",
            MT: "Aprovechar el caos para cerrar un trato."
        }
    };

    // Tally y actualización visual
    function tally() {
        const counts = { VA:0, CF:0, VC:0, VN:0, HC:0, MT:0, VV:0, VD:0 };
        for (let i=1;i<=20;i++) {
            const sel = document.querySelector(`input[name=q${i}]:checked`);
            if (sel) {
                counts[sel.value]++;
            }
        }
        // actualizar scoreboard con animación
        Object.entries(counts).forEach(([k,v])=>{
            const cell = document.getElementById(`score-${k}`);
            cell.textContent = v;
            const parent = cell.closest(".score-cell");
            if (v>0) parent.classList.add("active");
            else parent.classList.remove("active");
        });
        // progreso
        const answered = Object.values(counts).reduce((a,b)=>a+b,0);
        const percent = Math.min((answered / 20) * 100, 100);
        document.getElementById("progress-bar").style.width = percent + "%";
        return counts;
    }

    function decideResult(counts) {
        const max = Math.max(...Object.values(counts));
        const winners = Object.entries(counts).filter(([k,v])=>v === max && max>0).map(([k])=>k);
        return winners;
    }

    function renderTieBreaker(winners, output) {
        const tieDiv = document.createElement("div");
        tieDiv.className="tie-notice";
        tieDiv.innerHTML = `<div><strong>Empate entre:</strong> ${winners.map(k=>profiles[k].name).join(", ")}. Elige para desempatar:</div>`;
        const btnContainer = document.createElement("div");
        btnContainer.className="tie-buttons";
        Object.entries(tieBreaker.options).forEach(([key, text])=>{
            if (!winners.includes(key)) return; // solo mostrar los empatados
            const btn = document.createElement("button");
            btn.textContent = text;
            btn.dataset.choice = key;
            btn.onclick = (e)=>{
                e.preventDefault();
                // mostrar resultado final con esa elección
                showFinal(key, output, true);
            };
            btnContainer.appendChild(btn);
        });
        tieDiv.appendChild(btnContainer);
        output.appendChild(tieDiv);
    }

    function showFinal(key, output, fromTie=false) {
        const profile = profiles[key];
        output.innerHTML = "";
        const badge = document.createElement("div");
        badge.className="badge";
        badge.textContent = profile.name;

        const desc = document.createElement("div");
        desc.className="profile-desc";
        desc.textContent = profile.desc;

        const extra = document.createElement("div");
        extra.className="final-tagline";
        extra.textContent = fromTie 
            ? `Desempate resuelto: se eligió la esencia de ${profile.name}.` 
            : `Tu esencia dominante es ${profile.name}.`;

        output.appendChild(badge);
        output.appendChild(desc);
        output.appendChild(extra);
        output.classList.remove("hidden");
        output.scrollIntoView({behavior:"smooth", block:"center"});
    }

    function renderResult() {
        const counts = tally();
        const winners = decideResult(counts);
        const output = document.getElementById("output");
        output.innerHTML = "";
        if (winners.length === 0) {
            output.innerHTML = `<div class="badge">Incompleto</div><div class="profile-desc">Debes responder al menos una opción por pregunta para que el test pueda revelar tu esencia.</div>`;
            output.classList.remove("hidden");
            return;
        }
        if (winners.length === 1) {
            showFinal(winners[0], output, false);
        } else {
            renderTieBreaker(winners, output);
        }
    }

    // Interactividad: selección visual
    document.querySelectorAll(".option").forEach(label => {
        label.addEventListener("click", ()=>{
            const input = label.querySelector("input");
            if (!input) return;
            input.checked = true;
            // marcar seleccionado visualmente en su grupo
            const group = label.closest(".options");
            group.querySelectorAll(".option").forEach(o=>o.classList.remove("selected"));
            label.classList.add("selected");
            tally();
        });
    });

    document.getElementById("reveal").addEventListener("click", (e)=>{
        e.preventDefault();
        renderResult();
    });
    document.getElementById("reset").addEventListener("click", (e)=>{
        e.preventDefault();
        document.getElementById("test-form").reset();
        document.querySelectorAll(".option").forEach(o=>o.classList.remove("selected"));
        // reset scores & progress
        ["VA","CF","VC","VN","HC","MT","VV","VD"].forEach(k=>{
            document.getElementById(`score-${k}`).textContent="0";
            const parent = document.getElementById(`score-${k}`).closest(".score-cell");
            parent.classList.remove("active");
        });
        document.getElementById("progress-bar").style.width="0%";
        const output = document.getElementById("output");
        output.classList.add("hidden");
        output.innerHTML="";
    });

    // live tally when any radio changes (for accessibility)
    document.getElementById("test-form").addEventListener("change", ()=> tally());

    // Inicial
    tally();
</script>

</body>
</html>
