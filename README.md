<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Horloge de Paris - JWE1</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            transition: color 5s;
            padding: 20px;
            background-size: 300% 100%;
            animation: scrollBackground 10s linear infinite;
        }
        #clock {
            font-size: 4em;
            font-weight: bold;
            margin: 20px auto;
            padding: 10px;
            border: 3px solid black;
            display: inline-block;
            background: rgba(255, 255, 255, 0.7);
            border-radius: 10px;
            animation: pulse 1.5s infinite alternate;
        }
        @keyframes pulse {
            0% { transform: scale(1); opacity: 1; }
            100% { transform: scale(1.1); opacity: 0.8; }
        }
        @keyframes alert {
            0% { background: red; }
            50% { background: darkred; }
            100% { background: red; }
        }
        @keyframes smoke {
            0% { opacity: 0.2; }
            50% { opacity: 0.5; }
            100% { opacity: 0.2; }
        }
        @keyframes scrollBackground {
            0% { background-position: 0% 50%; }
            100% { background-position: 100% 50%; }
        }
        .theme-menu {
            position: fixed;
            bottom: 20px;
            left: 20px;
        }
        .theme-menu button {
            padding: 10px 15px;
            font-size: 1.2em;
            cursor: pointer;
            border-radius: 5px;
            margin: 5px;
            border: none;
        }
        .theme-selector {
            position: fixed;
            bottom: 60px;
            left: 20px;
            background: rgba(0, 0, 0, 0.8);
            color: white;
            padding: 15px;
            border-radius: 10px;
            display: none;
        }
        .smoke-effect {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.3);
            animation: smoke 5s infinite;
            display: none;
        }
    </style>
</head>
<body>
    <h1>Heure de Paris - Jurassic World Evolution</h1>
    <div id="clock"></div>
    
    <div class="theme-menu">
        <button onclick="toggleThemeMenu()">🎨 Choisir un Thème</button>
    </div>
    
    <div class="theme-selector" id="themeSelector">
        <button onclick="setTheme('jurassic')">🦖 Jurassic Park</button>
        <button onclick="setTheme('nature')">🌿 Parc Naturel</button>
        <button onclick="setTheme('futuriste')">⚡ Jurassic World</button>
        <button onclick="setTheme('danger')">🔥 Chaos & Danger</button>
        <button onclick="setTheme('nublar')">🌅 Île de Nublar</button>
        <button onclick="setTheme('sorna')">🌫️ Île de Sorna</button>
        <button onclick="setTheme('pena')">🏝️ Île Pena</button>
        <button onclick="setTheme('muerta')">🌴 Île Muerta</button>
        <button onclick="setTheme('matanceros')">☀️ Île Matanceros</button>
        <button onclick="toggleThemeMenu()">❌ Fermer</button>
    </div>
    
    <div class="smoke-effect" id="smokeEffect"></div>
    
    <script>
        // Fonction pour afficher ou masquer le menu des thèmes
        function toggleThemeMenu() {
            const menu = document.getElementById("themeSelector");
            if (menu.style.display === "none" || menu.style.display === "") {
                menu.style.display = "block";
            } else {
                menu.style.display = "none";
            }
        }

        // Mettre à jour l'heure
        function updateClock() {
            const options = { timeZone: 'Europe/Paris', hour12: false, hour: '2-digit', minute: '2-digit', second: '2-digit' };
            const now = new Date();
            const hour = now.getHours();
            document.getElementById('clock').innerText = new Intl.DateTimeFormat('fr-FR', options).format(now);
            
            if (hour >= 19 || hour < 8) {
                document.body.style.color = '#fff';
            }
        }
        setInterval(updateClock, 1000);
        updateClock();
        
        // Appliquer un thème spécifique
        function setTheme(theme) {
            const themes = {
                'jurassic': { 
                    background: 'linear-gradient(to right, #FFD700, #FF8C00, #228B22)', 
                    color: '#000',
                    animation: 'scrollBackground 15s linear infinite' 
                },
                'nature': { 
                    background: 'linear-gradient(to right, #90EE90, #ADD8E6, #FFFACD)', 
                    color: '#000',
                    animation: 'scrollBackground 15s linear infinite' 
                },
                'futuriste': { 
                    background: 'linear-gradient(to right, #00BFFF, #FFFFFF, #800080)', 
                    color: '#fff',
                    animation: 'scrollBackground 15s linear infinite' 
                },
                'danger': { 
                    background: 'linear-gradient(to right, #FF0000, #FF4500)', 
                    color: '#fff', 
                    alert: true, 
                    smoke: true, 
                    animation: 'none' // Pas d'animation pour le mode danger
                },
                'nublar': { 
                    background: 'linear-gradient(to right, #800080, #FF69B4, #191970)', 
                    color: '#fff',
                    animation: 'scrollBackground 15s linear infinite' 
                },
                'sorna': { 
                    background: 'linear-gradient(to right, #708090, #2E8B57, #4682B4)', 
                    color: '#fff',
                    animation: 'scrollBackground 15s linear infinite' 
                },
                'pena': { 
                    background: 'linear-gradient(to right, #2F4F4F, #556B2F, #8B4513)', 
                    color: '#fff',
                    animation: 'scrollBackground 15s linear infinite' 
                },
                'muerta': { 
                    background: 'linear-gradient(to right, #008000, #32CD32, #FFD700)', 
                    color: '#fff',
                    animation: 'scrollBackground 15s linear infinite' 
                },
                'matanceros': { 
                    background: 'linear-gradient(to right, #FFA500, #FFD700, #87CEEB)', 
                    color: '#fff',
                    animation: 'scrollBackground 15s linear infinite' 
                }
            };
            document.body.style.background = themes[theme].background;
            document.body.style.color = themes[theme].color;
            document.body.style.animation = themes[theme].animation;
            
            if (theme === 'danger') {
                document.body.style.animation = 'alert 3s infinite alternate';
                document.getElementById('smokeEffect').style.display = 'block';
            } else {
                document.body.style.animation = 'scrollBackground 15s linear infinite';
                document.getElementById('smokeEffect').style.display = 'none';
            }
        }
    </script>
</body>
</html>
