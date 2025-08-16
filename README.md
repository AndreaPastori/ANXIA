<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kit d'Ansia Tascabile</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #2f4156;
            --secondary: #587d8e;
            --light-blue: #c7dae6;
            --cream: #f4efeb;
            --white: #ffffff;
        }

        @import url('https://fonts.googleapis.com/css2?family=Abril+Fatface&family=Inter:wght@300;400;500;600;700&display=swap');

        body {
            font-family: 'Inter', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, var(--light-blue) 0%, var(--cream) 100%);
            min-height: 100vh;
            overflow-x: hidden;
        }

        .app-container {
            max-width: 414px;
            margin: 0 auto;
            min-height: 100vh;
            background: linear-gradient(135deg, var(--light-blue) 0%, var(--cream) 100%);
            position: relative;
        }

        .screen {
            display: none;
            padding: 20px;
            min-height: 100vh;
            animation: slideIn 0.3s ease-out;
        }

        .screen.active {
            display: block;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateX(30px); }
            to { opacity: 1; transform: translateX(0); }
        }

        .header {
            text-align: center;
            margin-bottom: 30px;
            padding-top: 40px;
        }

        .app-title {
            font-size: 28px;
            font-weight: 700;
            color: var(--primary);
            margin-bottom: 8px;
            text-shadow: 0 2px 4px rgba(0,0,0,0.1);
        }

        .app-subtitle {
            font-size: 16px;
            color: var(--secondary);
            font-style: italic;
            margin-bottom: 20px;
        }

        .welcome-message {
            background: var(--white);
            padding: 25px;
            border-radius: 25px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            text-align: center;
            border: 3px solid var(--light-blue);
        }

        .welcome-message h2 {
            color: var(--primary);
            font-size: 22px;
            font-weight: 600;
            margin-bottom: 15px;
        }

        .welcome-message p {
            color: var(--secondary);
            font-size: 16px;
            line-height: 1.5;
        }

        .menu-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 30px;
        }

        .menu-item {
            background: var(--white);
            padding: 25px 20px;
            border-radius: 25px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 8px 25px rgba(0,0,0,0.1);
            border: 3px solid transparent;
            position: relative;
            overflow: hidden;
        }

        .menu-item:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 35px rgba(0,0,0,0.15);
            border-color: var(--secondary);
        }

        .menu-item::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(199, 218, 230, 0.3), transparent);
            transform: rotate(45deg);
            transition: all 0.5s ease;
            opacity: 0;
        }

        .menu-item:hover::before {
            opacity: 1;
            animation: shimmer 1s ease-in-out;
        }

        @keyframes shimmer {
            0% { transform: translateX(-100%) translateY(-100%) rotate(45deg); }
            100% { transform: translateX(100%) translateY(100%) rotate(45deg); }
        }

        .menu-icon {
            width: 40px;
            height: 40px;
            margin: 0 auto 12px auto;
            display: block;
            fill: var(--secondary);
            stroke: var(--secondary);
            stroke-width: 2;
        }

        .menu-item h3 {
            font-size: 16px;
            color: var(--primary);
            font-weight: 600;
            margin-bottom: 8px;
        }

        .menu-item p {
            font-size: 12px;
            color: var(--secondary);
            line-height: 1.4;
        }

        .sos-button {
            background: linear-gradient(135deg, #ff6b6b, #ff8e8e);
            color: white;
            padding: 25px;
            border-radius: 25px;
            text-align: center;
            cursor: pointer;
            margin-bottom: 20px;
            box-shadow: 0 10px 30px rgba(255, 107, 107, 0.3);
            transition: all 0.3s ease;
            border: none;
            width: 100%;
            font-size: 18px;
            font-weight: 600;
        }

        .sos-button:hover {
            transform: scale(1.05);
            box-shadow: 0 15px 40px rgba(255, 107, 107, 0.4);
        }

        .breathing-exercise {
            background: var(--white);
            padding: 30px;
            border-radius: 25px;
            text-align: center;
            margin-bottom: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .breathing-circle {
            width: 150px;
            height: 150px;
            border: 4px solid var(--secondary);
            border-radius: 50%;
            margin: 20px auto;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            color: var(--primary);
            transition: all 4s ease-in-out;
            background: linear-gradient(135deg, var(--light-blue), var(--white));
        }

        .breathing-circle.expand {
            transform: scale(1.3);
            border-color: var(--primary);
        }

        .game-container {
            background: var(--white);
            padding: 25px;
            border-radius: 25px;
            margin-bottom: 20px;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .scratch-area {
            width: 250px;
            height: 150px;
            background: linear-gradient(45deg, var(--secondary), var(--primary));
            margin: 20px auto;
            border-radius: 15px;
            position: relative;
            cursor: pointer;
            overflow: hidden;
        }

        .scratch-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: #888;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 16px;
            transition: opacity 0.3s ease;
        }

        .hidden-message {
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 18px;
            font-weight: 600;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .emotion-slider {
            width: 100%;
            margin: 20px 0;
            -webkit-appearance: none;
            appearance: none;
            height: 10px;
            border-radius: 5px;
            background: linear-gradient(to right, #ff6b6b, #ffd93d, #6bcf7f);
            outline: none;
        }

        .emotion-slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 25px;
            height: 25px;
            border-radius: 50%;
            background: var(--white);
            border: 3px solid var(--secondary);
            cursor: pointer;
            box-shadow: 0 2px 10px rgba(0,0,0,0.2);
        }

        .mood-display {
            font-size: 24px;
            margin: 20px 0;
        }

        .diary-entry {
            background: var(--cream);
            padding: 15px;
            border-radius: 15px;
            margin: 10px 0;
            border-left: 4px solid var(--secondary);
        }

        .sticker-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin: 20px 0;
        }

        .sticker-item {
            background: var(--white);
            border-radius: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            text-align: center;
            min-height: 120px;
        }

        .sticker-item:hover {
            transform: scale(1.05) rotate(2deg);
            box-shadow: 0 8px 25px rgba(0,0,0,0.15);
        }

        .sticker-emoji {
            font-size: 40px;
            margin-bottom: 8px;
            display: block;
        }

        .sticker-text {
            font-size: 12px;
            color: var(--primary);
            font-weight: 600;
            line-height: 1.2;
        }

        .back-button, .nav-button {
            background: var(--secondary);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            margin: 10px 5px;
            font-size: 16px;
            transition: all 0.3s ease;
        }

        .back-button:hover, .nav-button:hover {
            background: var(--primary);
            transform: translateY(-2px);
        }

        .info-card {
            background: var(--white);
            padding: 20px;
            border-radius: 20px;
            margin: 15px 0;
            box-shadow: 0 8px 25px rgba(0,0,0,0.1);
            border-left: 5px solid var(--secondary);
        }

        .info-card h3 {
            color: var(--primary);
            margin-bottom: 10px;
        }

        .info-card p {
            color: var(--secondary);
            line-height: 1.6;
        }

        .contact-button {
            background: linear-gradient(135deg, var(--secondary), var(--primary));
            color: white;
            padding: 15px 30px;
            border-radius: 25px;
            text-decoration: none;
            display: inline-block;
            margin: 10px 0;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .contact-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.3);
        }

        .floating-elements {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }

        .floating-bubble {
            position: absolute;
            background: rgba(199, 218, 230, 0.3);
            border-radius: 50%;
            animation: float 6s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(180deg); }
        }

        .motivational-quote {
            background: linear-gradient(135deg, var(--light-blue), var(--white));
            padding: 20px;
            border-radius: 20px;
            text-align: center;
            margin: 20px 0;
            border: 2px solid var(--secondary);
            font-style: italic;
            color: var(--primary);
        }

        @media (max-width: 480px) {
            .menu-grid {
                grid-template-columns: 1fr;
                gap: 15px;
            }
            
            .app-container {
                max-width: 100%;
            }
            
            .screen {
                padding: 15px;
            }
        }

        .pulse {
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body>
    <div class="floating-elements">
        <div class="floating-bubble" style="width: 60px; height: 60px; top: 10%; left: 10%; animation-delay: 0s;"></div>
        <div class="floating-bubble" style="width: 40px; height: 40px; top: 70%; right: 10%; animation-delay: 2s;"></div>
        <div class="floating-bubble" style="width: 80px; height: 80px; top: 30%; right: 15%; animation-delay: 4s;"></div>
    </div>

    <div class="app-container">
        <!-- Home Screen -->
        <div class="screen active" id="home">
            <div class="header">
                <h1 class="app-title">Kit d'Ansia Tascabile</h1>
                <p class="app-subtitle">Il tuo compagno digitale antistress</p>
            </div>

            <div class="welcome-message">
                <h2>Benvenutə nel tuo kit d'ansia tascabile! 🌸</h2>
                <p>Spoiler: non muori, è solo ansia. Respira, gioca, e ricorda che anche questo momento passerà.</p>
            </div>

            <div class="menu-grid">
                <div class="menu-item" onclick="showScreen('sos')">
                    <svg class="menu-icon" viewBox="0 0 100 100">
                        <circle cx="50" cy="50" r="30" fill="none" stroke-width="4"/>
                        <rect x="45" y="35" width="10" height="20" rx="2"/>
                        <circle cx="50" cy="65" r="3"/>
                    </svg>
                    <h3>SOS Ansia</h3>
                    <p>Aiuto immediato quando serve</p>
                </div>

                <div class="menu-item" onclick="showScreen('games')">
                    <svg class="menu-icon" viewBox="0 0 100 100">
                        <rect x="25" y="35" width="50" height="30" rx="8" fill="none"/>
                        <circle cx="35" cy="55" r="4"/>
                        <circle cx="65" cy="45" r="3"/>
                        <circle cx="65" cy="55" r="3"/>
                        <rect x="40" y="25" width="20" height="10" rx="5"/>
                    </svg>
                    <h3>Giochi Flash</h3>
                    <p>Distrazioni veloci e rilassanti</p>
                </div>

                <div class="menu-item" onclick="showScreen('diary')">
                    <svg class="menu-icon" viewBox="0 0 100 100">
                        <rect x="30" y="20" width="40" height="55" rx="3" fill="none"/>
                        <line x1="38" y1="35" x2="62" y2="35" stroke-width="2"/>
                        <line x1="38" y1="45" x2="55" y2="45" stroke-width="2"/>
                        <line x1="38" y1="55" x2="60" y2="55" stroke-width="2"/>
                        <rect x="25" y="15" width="50" height="8" rx="2"/>
                    </svg>
                    <h3>Diario Emozioni</h3>
                    <p>Traccia il tuo umore</p>
                </div>

                <div class="menu-item" onclick="showScreen('stickers')">
                    <svg class="menu-icon" viewBox="0 0 100 100">
                        <path d="M50 20 L60 40 L80 40 L65 55 L70 75 L50 65 L30 75 L35 55 L20 40 L40 40 Z"/>
                        <circle cx="50" cy="50" r="8" opacity="0.3"/>
                        <circle cx="35" cy="25" r="2" opacity="0.6"/>
                        <circle cx="65" cy="30" r="2" opacity="0.6"/>
                    </svg>
                    <h3>Box Sticker</h3>
                    <p>La tua collezione digitale</p>
                </div>

                <div class="menu-item" onclick="showScreen('info')">
                    <svg class="menu-icon" viewBox="0 0 100 100">
                        <circle cx="50" cy="50" r="30" fill="none" stroke-width="4"/>
                        <circle cx="50" cy="35" r="3"/>
                        <rect x="45" y="45" width="10" height="20" rx="2"/>
                    </svg>
                    <h3>Info & Contatti</h3>
                    <p>Risorse e supporto</p>
                </div>
            </div>
        </div>

        <!-- SOS Screen -->
        <div class="screen" id="sos">
            <div class="header">
                <svg style="width: 40px; height: 40px; fill: var(--secondary); stroke: var(--secondary); stroke-width: 2; margin: 0 auto 10px; display: block;" viewBox="0 0 100 100">
                    <circle cx="50" cy="50" r="30" fill="none" stroke-width="4"/>
                    <rect x="45" y="35" width="10" height="20" rx="2"/>
                    <circle cx="50" cy="65" r="3"/>
                </svg>
                <h1 class="app-title">SOS Ansia</h1>
                <p class="app-subtitle">Aiuto immediato per te</p>
            </div>

            <button class="sos-button pulse" onclick="startBreathing()">
                🫁 RESPIRAZIONE GUIDATA
            </button>

            <div class="breathing-exercise">
                <h3 style="color: var(--primary); margin-bottom: 15px;">Respira con me</h3>
                <div class="breathing-circle" id="breathingCircle">
                    <span id="breathingText">Pronto?</span>
                </div>
                <button class="nav-button" onclick="toggleBreathing()">▶️ Inizia</button>
            </div>

            <div class="motivational-quote">
                <p>"Questo momento difficile non ti definisce. Sei più forte di quanto pensi. 💪"</p>
            </div>

            <button class="back-button" onclick="showScreen('home')">← Home</button>
        </div>

        <!-- Games Screen -->
        <div class="screen" id="games">
            <div class="header">
                <svg style="width: 40px; height: 40px; fill: var(--secondary); stroke: var(--secondary); stroke-width: 2; margin: 0 auto 10px; display: block;" viewBox="0 0 100 100">
                    <rect x="25" y="35" width="50" height="30" rx="8" fill="none"/>
                    <circle cx="35" cy="55" r="4"/>
                    <circle cx="65" cy="45" r="3"/>
                    <circle cx="65" cy="55" r="3"/>
                    <rect x="40" y="25" width="20" height="10" rx="5"/>
                </svg>
                <h1 class="app-title">Giochi Flash</h1>
                <p class="app-subtitle">Distrazioni veloci antistress</p>
            </div>

            <div class="game-container">
                <h3 style="color: var(--primary); margin-bottom: 15px;">Gratta via l'ansia</h3>
                <p style="color: var(--secondary); margin-bottom: 20px;">Tocca e tieni premuto per rivelare il messaggio nascosto</p>
                <div class="scratch-area" id="scratchArea" onmousedown="startScratch()" ontouchstart="startScratch()">
                    <div class="scratch-overlay" id="scratchOverlay">
                        Gratta qui! 👆
                    </div>
                    <div class="hidden-message">
                        Sei incredibile! ⭐
                    </div>
                </div>
                <button class="nav-button" onclick="resetScratch()">🔄 Reset</button>
            </div>

            <div class="game-container">
                <h3 style="color: var(--primary); margin-bottom: 15px;">Click Rilassante</h3>
                <div style="font-size: 60px; cursor: pointer; user-select: none;" onclick="changeEmoji(this)">
                    😊
                </div>
                <p style="color: var(--secondary); margin-top: 10px;">Clicca per cambiare espressione!</p>
            </div>

            <button class="back-button" onclick="showScreen('home')">← Home</button>
        </div>

        <!-- Diary Screen -->
        <div class="screen" id="diary">
            <div class="header">
                <svg style="width: 40px; height: 40px; fill: var(--secondary); stroke: var(--secondary); stroke-width: 2; margin: 0 auto 10px; display: block;" viewBox="0 0 100 100">
                    <rect x="30" y="20" width="40" height="55" rx="3" fill="none"/>
                    <line x1="38" y1="35" x2="62" y2="35" stroke-width="2"/>
                    <line x1="38" y1="45" x2="55" y2="45" stroke-width="2"/>
                    <line x1="38" y1="55" x2="60" y2="55" stroke-width="2"/>
                    <rect x="25" y="15" width="50" height="8" rx="2"/>
                </svg>
                <h1 class="app-title">Diario Emozioni</h1>
                <p class="app-subtitle">Come ti senti oggi?</p>
            </div>

            <div class="game-container">
                <h3 style="color: var(--primary); margin-bottom: 20px;">Il tuo umore ora</h3>
                <input type="range" min="1" max="10" value="5" class="emotion-slider" id="moodSlider" oninput="updateMood(this.value)">
                <div class="mood-display" id="moodDisplay">😐 Neutrale (5/10)</div>
                
                <textarea placeholder="Scrivi una nota veloce sui tuoi pensieri..." style="width: 100%; height: 80px; padding: 15px; border: 2px solid var(--light-blue); border-radius: 15px; margin: 15px 0; resize: none; font-family: inherit;" id="noteText"></textarea>
                
                <button class="nav-button" onclick="saveEntry()">💾 Salva Momento</button>
            </div>

            <div id="diaryEntries">
                <div class="diary-entry">
                    <strong>Oggi - 14:30</strong><br>
                    😊 Umore: Buono (7/10)<br>
                    <em>"Giornata produttiva, mi sento meglio dopo la pausa pranzo!"</em>
                </div>
            </div>

            <button class="back-button" onclick="showScreen('home')">← Home</button>
        </div>

        <!-- Stickers Screen -->
        <div class="screen" id="stickers">
            <div class="header">
                <svg style="width: 40px; height: 40px; fill: var(--secondary); stroke: var(--secondary); stroke-width: 2; margin: 0 auto 10px; display: block;" viewBox="0 0 100 100">
                    <path d="M50 20 L60 40 L80 40 L65 55 L70 75 L50 65 L30 75 L35 55 L20 40 L40 40 Z"/>
                    <circle cx="50" cy="50" r="8" opacity="0.3"/>
                    <circle cx="35" cy="25" r="2" opacity="0.6"/>
                    <circle cx="65" cy="30" r="2" opacity="0.6"/>
                </svg>
                <h1 class="app-title">Box Sticker</h1>
                <p class="app-subtitle">La tua collezione antistress</p>
            </div>

            <div class="game-container">
                <h3 style="color: var(--primary); margin-bottom: 20px;">Sticker Emotivi</h3>
                <div class="sticker-grid">
                    <div class="sticker-item" onclick="shareSticker('🌸 Respira profondo')">
                        <span class="sticker-emoji">🌸</span>
                        <div class="sticker-text">Respira profondo</div>
                    </div>
                    <div class="sticker-item" onclick="shareSticker('💪 Sei forte')">
                        <span class="sticker-emoji">💪</span>
                        <div class="sticker-text">Sei forte</div>
                    </div>
                    <div class="sticker-item" onclick="shareSticker('🌈 Tutto passa')">
                        <span class="sticker-emoji">🌈</span>
                        <div class="sticker-text">Tutto passa</div>
                    </div>
                    <div class="sticker-item" onclick="shareSticker('☀️ Sei al sicuro')">
                        <span class="sticker-emoji">☀️</span>
                        <div class="sticker-text">Sei al sicuro</div>
                    </div>
                    <div class="sticker-item" onclick="shareSticker('🦋 Un passo alla volta')">
                        <span class="sticker-emoji">🦋</span>
                        <div class="sticker-text">Un passo alla volta</div>
                    </div>
                    <div class="sticker-item" onclick="shareSticker('💝 Credici')">
                        <span class="sticker-emoji">💝</span>
                        <div class="sticker-text">Credici</div>
                    </div>
                    <div class="sticker-item" onclick="shareSticker('🌺 Vai avanti')">
                        <span class="sticker-emoji">🌺</span>
                        <div class="sticker-text">Vai avanti</div>
                    </div>
                    <div class="sticker-item" onclick="shareSticker('⭐ Sei amato')">
                        <span class="sticker-emoji">⭐</span>
                        <div class="sticker-text">Sei amato</div>
                    </div>
                    <div class="sticker-item" onclick="shareSticker('🕊️ Andrà tutto bene')">
                        <span class="sticker-emoji">🕊️</span>
                        <div class="sticker-text">Andrà tutto bene</div>
                    </div>
                </div>
                <p style="color: var(--secondary); text-align: center; margin-top: 15px;">Tocca uno sticker per condividerlo!</p>
            </div>

            <button class="back-button" onclick="showScreen('home')">← Home</button>
        </div>

        <!-- Info Screen -->
        <div class="screen" id="info">
            <div class="header">
                <svg style="width: 40px; height: 40px; fill: var(--secondary); stroke: var(--secondary); stroke-width: 2; margin: 0 auto 10px; display: block;" viewBox="0 0 100 100">
                    <circle cx="50" cy="50" r="30" fill="none" stroke-width="4"/>
                    <circle cx="50" cy="35" r="3"/>
                    <rect x="45" y="45" width="10" height="20" rx="2"/>
                </svg>
                <h1 class="app-title">Info & Contatti</h1>
                <p class="app-subtitle">Informazioni e risorse utili</p>
            </div>

            <div class="info-card">
                <h3>Cos'è l'ansia?</h3>
                <p>L'ansia è una risposta naturale del corpo allo stress. È normale provare ansia occasionale, ma quando diventa eccessiva può interferire con la vita quotidiana. Ricorda: non sei solo e l'ansia è trattabile.</p>
            </div>

            <div class="info-card">
                <h3>Tecniche rapide anti-ansia</h3>
                <p>• Respirazione 4-7-8: inspira per 4, trattieni per 7, espira per 8<br>
                • Tecnica 5-4-3-2-1: identifica 5 cose che vedi, 4 che senti, 3 che tocchi, 2 che annusi, 1 che assaggi<br>
                • Movimento: anche una breve camminata può aiutare</p>
            </div>

            <div class="info-card">
                <h3>Quando cercare aiuto</h3>
                <p>Se l'ansia interferisce significativamente con la tua vita quotidiana, considera di parlare con un professionista della salute mentale. Non c'è nulla di sbagliato nel chiedere aiuto.</p>
            </div>

            <div style="text-align: center; margin: 30px 0;">
                <h3 style="color: var(--primary); margin-bottom: 20px;">Risorse di supporto</h3>
                
                <a href="tel:0280253535" class="contact-button">📞 Telefono Amico (IT)</a>
                <a href="tel:800925970" class="contact-button">🆘 Linea Supporto Psicologico</a>
                
                <div style="margin-top: 20px; color: var(--secondary); font-size: 14px;">
                    <p>Ricorda: questa app è un supporto, non sostituisce il parere medico professionale.</p>
                </div>
            </div>

            <button class="back-button" onclick="showScreen('home')">← Home</button>
        </div>
    </div>

    <script>
        let breathingActive = false;
        let breathingInterval;
        let scratchRevealed = false;

        function showScreen(screenId) {
            document.querySelectorAll('.screen').forEach(screen => {
                screen.classList.remove('active');
            });
            document.getElementById(screenId).classList.add('active');
        }

        function startBreathing() {
            navigator.vibrate && navigator.vibrate([100, 50, 100]);
            toggleBreathing();
        }

        function toggleBreathing() {
            const circle = document.getElementById('breathingCircle');
            const text = document.getElementById('breathingText');
            
            if (!breathingActive) {
                breathingActive = true;
                let phase = 0; // 0: inhale, 1: hold, 2: exhale
                let count = 4;
                
                breathingInterval = setInterval(() => {
                    switch(phase) {
                        case 0: // Inhale
                            circle.classList.add('expand');
                            text.textContent = `Inspira ${count}`;
                            count--;
                            if (count < 0) {
                                phase = 1;
                                count = 7;
                            }
                            break;
                        case 1: // Hold
                            text.textContent = `Trattieni ${count}`;
                            count--;
                            if (count < 0) {
                                phase = 2;
                                count = 8;
                                circle.classList.remove('expand');
                            }
                            break;
                        case 2: // Exhale
                            text.textContent = `Espira ${count}`;
                            count--;
                            if (count < 0) {
                                phase = 0;
                                count = 4;
                            }
                            break;
                    }
                }, 1000);
                
                document.querySelector('#sos .nav-button').textContent = '⏸️ Stop';
            } else {
                breathingActive = false;
                clearInterval(breathingInterval);
                circle.classList.remove('expand');
                text.textContent = 'Pronto?';
                document.querySelector('#sos .nav-button').textContent = '▶️ Inizia';
            }
        }

        function startScratch() {
            if (!scratchRevealed) {
                document.getElementById('scratchOverlay').style.opacity = '0';
                scratchRevealed = true;
                navigator.vibrate && navigator.vibrate(200);
            }
        }

        function resetScratch() {
            document.getElementById('scratchOverlay').style.opacity = '1';
            scratchRevealed = false;
        }

        const emojis = ['😊', '😄', '🥰', '😎', '🤗', '😌', '🌟', '💪', '🦋', '🌸'];
        let emojiIndex = 0;

        function changeEmoji(element) {
            emojiIndex = (emojiIndex + 1) % emojis.length;
            element.textContent = emojis[emojiIndex];
            element.style.transform = 'scale(1.2)';
            setTimeout(() => {
                element.style.transform = 'scale(1)';
            }, 200);
        }

        const moods = [
            '😢 Molto triste (1/10)',
            '😟 Triste (2/10)', 
            '😔 Un po\' giù (3/10)',
            '😕 Non benissimo (4/10)',
            '😐 Neutrale (5/10)',
            '🙂 Abbastanza bene (6/10)',
            '😊 Bene (7/10)',
            '😄 Molto bene (8/10)',
            '😃 Ottimo (9/10)',
            '🤩 Fantastico! (10/10)'
        ];

        function updateMood(value) {
            document.getElementById('moodDisplay').textContent = moods[value - 1];
        }

        function saveEntry() {
            const mood = document.getElementById('moodSlider').value;
            const note = document.getElementById('noteText').value;
            const now = new Date();
            const time = now.toLocaleTimeString('it-IT', {hour: '2-digit', minute:'2-digit'});
            
            if (note.trim()) {
                const entry = document.createElement('div');
                entry.className = 'diary-entry';
                entry.innerHTML = `
                    <strong>Oggi - ${time}</strong><br>
                    ${moods[mood - 1]}<br>
                    <em>"${note}"</em>
                `;
                
                document.getElementById('diaryEntries').insertBefore(entry, document.getElementById('diaryEntries').firstChild);
                document.getElementById('noteText').value = '';
                
                navigator.vibrate && navigator.vibrate([100, 100, 100]);
            }
        }

        function shareSticker(stickerText) {
            if (navigator.share) {
                navigator.share({
                    title: 'Kit d\'Ansia Tascabile',
                    text: `${stickerText} - Dal mio kit antistress`,
                });
            } else {
                // Fallback: copy to clipboard
                navigator.clipboard.writeText(`${stickerText} - Dal mio Kit d'Ansia Tascabile`).then(() => {
                    showTemporaryMessage('Sticker copiato! 📋');
                });
            }
        }

        // Add some ambient interactivity
        document.addEventListener('click', (e) => {
            // Create a small ripple effect
            const ripple = document.createElement('div');
            ripple.style.position = 'fixed';
            ripple.style.left = e.clientX - 10 + 'px';
            ripple.style.top = e.clientY - 10 + 'px';
            ripple.style.width = '20px';
            ripple.style.height = '20px';
            ripple.style.borderRadius = '50%';
            ripple.style.background = 'rgba(199, 218, 230, 0.6)';
            ripple.style.pointerEvents = 'none';
            ripple.style.zIndex = '1000';
            ripple.style.animation = 'ripple 0.6s ease-out';
            
            document.body.appendChild(ripple);
            
            setTimeout(() => {
                ripple.remove();
            }, 600);
        });

        // Add ripple animation
        const style = document.createElement('style');
        style.textContent = `
            @keyframes ripple {
                0% {
                    transform: scale(1);
                    opacity: 0.6;
                }
                100% {
                    transform: scale(4);
                    opacity: 0;
                }
            }
        `;
        document.head.appendChild(style);

        // Add some random motivational quotes that appear
        const quotes = [
            "Sei più forte di quanto pensi 💪",
            "Un respiro alla volta 🌸",
            "Questo momento passerà 🌈",
            "Sei al sicuro qui e ora 🕊️",
            "Piccoli passi, grandi risultati ⭐",
            "La tua ansia non ti definisce 🦋",
            "Domani è un nuovo giorno ☀️"
        ];

        // Show a random quote every 30 seconds when on home screen
        setInterval(() => {
            if (document.getElementById('home').classList.contains('active')) {
                const randomQuote = quotes[Math.floor(Math.random() * quotes.length)];
                showTemporaryMessage(randomQuote);
            }
        }, 30000);

        function showTemporaryMessage(message) {
            const messageDiv = document.createElement('div');
            messageDiv.style.position = 'fixed';
            messageDiv.style.top = '20px';
            messageDiv.style.left = '50%';
            messageDiv.style.transform = 'translateX(-50%)';
            messageDiv.style.background = 'linear-gradient(135deg, var(--white), var(--light-blue))';
            messageDiv.style.padding = '15px 25px';
            messageDiv.style.borderRadius = '25px';
            messageDiv.style.boxShadow = '0 10px 30px rgba(0,0,0,0.2)';
            messageDiv.style.zIndex = '2000';
            messageDiv.style.color = 'var(--primary)';
            messageDiv.style.fontWeight = '600';
            messageDiv.style.fontSize = '16px';
            messageDiv.style.animation = 'slideDown 0.5s ease-out, fadeOut 0.5s ease-in 2.5s forwards';
            messageDiv.textContent = message;
            
            document.body.appendChild(messageDiv);
            
            setTimeout(() => {
                messageDiv.remove();
            }, 3000);
        }

        // Add slide down animation
        const slideStyle = document.createElement('style');
        slideStyle.textContent = `
            @keyframes slideDown {
                from {
                    transform: translateX(-50%) translateY(-100px);
                    opacity: 0;
                }
                to {
                    transform: translateX(-50%) translateY(0);
                    opacity: 1;
                }
            }
            
            @keyframes fadeOut {
                from { opacity: 1; }
                to { opacity: 0; }
            }
        `;
        document.head.appendChild(slideStyle);

        // Initialize app
        document.addEventListener('DOMContentLoaded', () => {
            // Add welcome vibration if supported
            if (navigator.vibrate) {
                navigator.vibrate([200, 100, 200]);
            }
            
            // Show welcome message after 2 seconds
            setTimeout(() => {
                showTemporaryMessage("Benvenutə! Sono qui per te 🌸");
            }, 2000);
        });

        // Add touch feedback for mobile
        document.addEventListener('touchstart', (e) => {
            const target = e.target.closest('.menu-item, .sos-button, .nav-button, .back-button, .sticker-item');
            if (target) {
                target.style.transform = 'scale(0.95)';
                setTimeout(() => {
                    target.style.transform = '';
                }, 150);
            }
        });

        // Enhanced scratch game with mouse/touch tracking
        let isScratching = false;
        let scratchProgress = 0;

        function handleScratchMove(e) {
            if (!isScratching) return;
            
            e.preventDefault();
            scratchProgress += 2;
            
            if (scratchProgress > 100) scratchProgress = 100;
            
            const overlay = document.getElementById('scratchOverlay');
            overlay.style.opacity = Math.max(0, 1 - (scratchProgress / 100));
            
            if (scratchProgress >= 80 && !scratchRevealed) {
                scratchRevealed = true;
                navigator.vibrate && navigator.vibrate([100, 50, 100, 50, 200]);
                showTemporaryMessage("Ben fatto! Hai grattato via l'ansia! 🎉");
            }
        }

        document.getElementById('scratchArea').addEventListener('mousemove', handleScratchMove);
        document.getElementById('scratchArea').addEventListener('touchmove', handleScratchMove);
        
        document.getElementById('scratchArea').addEventListener('mouseup', () => {
            isScratching = false;
        });
        
        document.getElementById('scratchArea').addEventListener('touchend', () => {
            isScratching = false;
        });

        // Enhanced reset function
        function resetScratch() {
            document.getElementById('scratchOverlay').style.opacity = '1';
            scratchRevealed = false;
            scratchProgress = 0;
            isScratching = false;
            navigator.vibrate && navigator.vibrate(100);
        }

        // Update startScratch function
        function startScratch() {
            isScratching = true;
            scratchProgress = 0;
        }
    </script>
</body>
</html>