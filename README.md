         <!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Invitation de Parrainage - 5.7 Cembassoise</title>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Cinzel:wght@400;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --gold: #d4af37;
            --bordeaux: #4a0404;
            --bordeaux-dark: #2d0202;
            --transition-speed: 1s;
        }

        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            background-color: black;
            font-family: 'Playfair Display', serif;
        }

        /* Conteneur pour les sections */
        .page {
            position: absolute;
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            transition: transform var(--transition-speed) cubic-bezier(0.65, 0, 0.35, 1), opacity var(--transition-speed);
            opacity: 0;
            pointer-events: none;
            box-sizing: border-box;
            padding: 20px;
        }

        .active {
            opacity: 1;
            pointer-events: all;
        }

        /* SECTION 1 : ENTREE (Image Casino) */
        #section1 {
            background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)), 
                        url('https://images.unsplash.com/photo-1596838132731-3301c3fd4317?q=80&w=1000') center/cover;
        }

        .casino-title {
            font-family: 'Cinzel', serif;
            color: white;
            font-size: 3.5rem; /* Réduit pour mobile */
            letter-spacing: 5px;
            text-shadow: 0 0 20px var(--gold);
            margin-bottom: 20px;
        }

        .btn-enter {
            color: var(--gold);
            border: 2px solid var(--gold);
            padding: 12px 35px;
            font-size: 1.2rem;
            text-transform: uppercase;
            cursor: pointer;
            background: rgba(0,0,0,0.4);
            transition: 0.3s;
            text-decoration: none;
            letter-spacing: 3px;
            margin-bottom: 15px;
        }

        .btn-enter:hover {
            background: var(--gold);
            color: black;
            box-shadow: 0 0 20px var(--gold);
        }

        /* Indication pour le swipe */
        .swipe-hint {
            color: rgba(255, 255, 255, 0.6);
            font-size: 0.9rem;
            letter-spacing: 1px;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-10px); }
            60% { transform: translateY(-5px); }
        }

        /* SECTION 2 : FOND BORDEAUX TEXTE PROGRESSIF */
        #section2 {
            background: radial-gradient(circle, var(--bordeaux), var(--bordeaux-dark));
        }

        .gold-text {
            color: var(--gold);
            font-size: 1.8rem;
            max-width: 90%;
            line-height: 1.5;
            filter: drop-shadow(0 2px 4px rgba(0,0,0,0.5));
        }

        /* Animation d'apparition par mot ou ligne */
        .fade-in-text {
            opacity: 0;
            transform: translateY(20px);
            transition: 0.8s ease-out;
        }

        .show-text {
            opacity: 1;
            transform: translateY(0);
        }

        /* SECTION 3 : JETONS ET CARTES */
        #section3 {
            background: linear-gradient(rgba(45, 2, 2, 0.8), rgba(45, 2, 2, 0.8)), 
                        url('https://images.unsplash.com/photo-1511193311914-0346f16bee90?q=80&w=1000') center/cover;
        }

        /* SECTION 4 : OSCAR FINAL */
        #section4 {
            background: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)), 
                        url('https://images.unsplash.com/photo-1485846234645-a62644f84728?q=80&w=1000') center/cover;
        }

        .oscar-img {
            width: 150px;
            margin-bottom: 30px;
            filter: drop-shadow(0 0 15px var(--gold));
        }

        /* Utilitaires de transition */
        .hidden-up { transform: translateY(-100%); }
        .hidden-down { transform: translateY(100%); }

    </style>
</head>
<body>

    <section id="section1" class="page active">
        <h1 class="casino-title">CASINO</h1>
        <a href="#" class="btn-enter" onclick="nextSection(1); return false;">Entrez</a>
        <div class="swipe-hint"> ou glissez vers le haut ↑</div>
    </section>

    <section id="section2" class="page hidden-down">
        <div id="msg1" class="gold-text">
            <p class="fade-in-text">L'attente touche à sa fin !!!</p>
            <p class="fade-in-text">Le grand jour est arrivé et nous serions heureux de le partager avec toi</p>
        </div>
        <div id="msg2" class="gold-text" style="display:none;">
            <p class="fade-in-text">Tu es cordialement invité à la soirée de parrainage de la 5.7 cembassoise</p>
            <p class="fade-in-text" style="font-weight: bold; font-size: 2rem;">Ce 11 avril au Pont Emana dès 20h</p>
        </div>
    </section>

    <section id="section3" class="page hidden-down">
        <div class="gold-text">
            <p class="fade-in-text">Sous le thème Casino...</p>
            <p class="fade-in-text" style="font-family: 'Cinzel'; font-size: 2.5rem;">NIGHT & Oscar Winning</p>
        </div>
    </section>

    <section id="section4" class="page hidden-down">
        <img src="https://upload.wikimedia.org/wikipedia/en/7/7f/Academy_Award_trophy.png" alt="Oscar" class="oscar-img">
        <h2 class="gold-text" style="font-family: 'Cinzel'; letter-spacing: 5px; font-size: 2rem;">Rendez-vous le 11.04.26</h2>
    </section>

    <script>
        // --- GESTION DU SWIPE POUR MOBILE ---
        let touchstartY = 0;
        let touchendY = 0;
        
        const s1 = document.getElementById('section1');

        s1.addEventListener('touchstart', e => {
            touchstartY = e.changedTouches[0].screenY;
        });

        s1.addEventListener('touchend', e => {
            touchendY = e.changedTouches[0].screenY;
            handleGesture();
        });

        function handleGesture() {
            // Si le glissement vers le haut est supérieur à 50px et qu'on est sur la section 1
            if (touchstartY - touchendY > 50 && s1.classList.contains('active')) {
                nextSection(1);
            }
        }
        // ------------------------------------

        function nextSection(current) {
            const s1 = document.getElementById('section1');
            const s2 = document.getElementById('section2');
            const s3 = document.getElementById('section3');
            const s4 = document.getElementById('section4');

            if(current === 1) {
                s1.classList.remove('active');
                s1.classList.add('hidden-up');
                s2.classList.remove('hidden-down');
                s2.classList.add('active');
                
                animateText('msg1', () => {
                    setTimeout(() => {
                        document.getElementById('msg1').style.transition = 'opacity 0.5s';
                        document.getElementById('msg1').style.opacity = '0';
                        setTimeout(() => {
                            document.getElementById('msg1').style.display = 'none';
                            document.getElementById('msg2').style.display = 'block';
                            animateText('msg2', () => {
                                setTimeout(() => nextSection(2), 3000);
                            });
                        }, 500);
                    }, 2500);
                });
            } else if (current === 2) {
                s2.classList.remove('active');
                s2.classList.add('hidden-up');
                s3.classList.remove('hidden-down');
                s3.classList.add('active');
                
                setTimeout(() => {
                    animateText('section3', () => {
                        setTimeout(() => nextSection(3), 3500);
                    });
                }, 500);
            } else if (current === 3) {
                s3.classList.remove('active');
                s3.classList.add('hidden-up');
                s4.classList.remove('hidden-down');
                s4.classList.add('active');
            }
        }

        function animateText(containerId, callback) {
            const container = document.getElementById(containerId);
            if (!container) return;
            
            const lines = container.querySelectorAll('.fade-in-text');
            if (lines.length === 0) {
                if (callback) callback();
                return;
            }

            lines.forEach((line, index) => {
                setTimeout(() => {
                    line.classList.add('show-text');
                    if(index === lines.length - 1 && callback) callback();
                }, index * 1000);
            });
        }
    </script>
</body>
</html>
   background-size: cover;
            background-position: center;
            border-radius: 25px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.6);
            width: 100%;
            max-width: 380px;
            height: 640px; /* Fixé à 640px dès le départ pour stabiliser l'image d'accueil */
            border: 2px solid rgba(244, 63, 94, 0.4);
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            padding: 20px;
            transition: all 0.5s ease;
            overflow-y: auto; 
            -webkit-overflow-scrolling: touch;
        }
        
        .fond-fleurs {
            background: linear-gradient(135deg, #ffe4e6 0%, #fecdd3 100%) !important;
            border: 2px solid #f43f5e;
        }
        .fond-fleurs p, .fond-fleurs h1, .fond-fleurs .question-text {
            color: #4c0519 !important;
            text-shadow: none !important;
        }
        
        .screen { display: none; height: 100%; flex-direction: column; justify-content: space-between; flex-grow: 1; }
        .screen.active { display: flex; }
        
        .poem-box {
            background: rgba(15, 23, 42, 0.9); 
            backdrop-filter: blur(8px);
            -webkit-backdrop-filter: blur(8px);
            padding: 14px;
            border-radius: 16px;
            font-style: italic;
            font-size: 14px;
            line-height: 1.5;
            color: #fda4af;
            margin-bottom: 12px;
            border-left: 3px solid #f43f5e;
            text-align: left;
            white-space: pre-line;
        }
        .fond-fleurs .poem-box {
            background: rgba(255, 255, 255, 0.85);
            border-left: 3px solid #e11d48;
            color: #4c0519 !important;
        }
        
        .question-text {
            font-weight: 700;
            font-size: 15px;
            color: #ffffff; 
            margin-top: 10px;
            margin-bottom: 15px;
            text-shadow: 0 2px 8px rgba(0,0,0,1), 0 1px 2px rgba(0,0,0,1); 
            line-height: 1.4;
        }
        
        .btn {
            display: block;
            width: 100%;
            padding: 12px 14px;
            margin: 8px 0;
            background: rgba(15, 23, 42, 0.95);
            color: white;
            border: 1px solid rgba(244, 63, 94, 0.5);
            border-radius: 15px;
            cursor: pointer;
            font-size: 13.5px;
            text-align: left;
            transition: all 0.2s;
            box-shadow: 0 4px 10px rgba(0,0,0,0.3);
        }
        .btn:active { transform: scale(0.98); }
        .btn-center { text-align: center; font-weight: bold; background: linear-gradient(90deg, #ec4899 0%, #f43f5e 100%); border: none; }
        
        .fond-fleurs .btn {
            background: rgba(255, 255, 255, 0.95);
            color: #4c0519;
            border: 1px solid #fda4af;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }
        .fond-fleurs .btn-center {
            color: white !important;
            background: linear-gradient(90deg, #ec4899 0%, #f43f5e 100%);
        }
        
        input {
            width: 100%;
            padding: 12px;
            margin: 8px 0;
            border-radius: 12px;
            border: 1px solid #fda4af;
            font-size: 15px;
            background: rgba(255, 255, 255, 0.9);
            color: #4c0519;
        }
        
        .popup-overlay {
            display: none;
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(15, 23, 42, 0.95);
            padding: 20px;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 10;
        }
        .popup-img { width: 100%; max-height: 180px; border-radius: 15px; object-fit: cover; margin-bottom: 15px; }
    </style>
</head>
<body>

<audio id="bg-music" src="ambiance.mp3" loop></audio>

<div class="wrapper">
    <div class="game-container" id="game-container" style="background-image: url('accueil .png');">

        <div class="screen active" id="screen1">
            <div style="margin-top: auto; margin-bottom: auto;">
                <h1 style="font-size: 26px; color: #f43f5e; text-shadow: 0 0 15px rgba(0,0,0,0.9); text-align: center; background: rgba(15, 23, 42, 0.75); padding: 20px; border-radius: 20px; border: 1px solid rgba(244,63,94,0.2);">The Perfect Date Simulator</h1>
            </div>
            <div style="margin-bottom: 20px;">
                <button class="btn btn-center" onclick="startGame()">Lancer la partie 🎮</button>
            </div>
        </div>

        <div class="screen" id="screen2">
            <div>
                <div class="poem-box" id="poem1"></div>
                <div class="question-text" id="q1-text" style="display:none;">Imaginons, PK t'écrit... Que fais-tu ?</div>
            </div>
            <div id="choices1" style="display:none; margin-bottom: 5px;">
                <button class="btn" onclick="validerEtape1()">A. Je réponds direct je suis trop contente qu'il m'ai écrit (j'espère pour toi 😑❤)</button>
                <button class="btn" onclick="showGameOver('Tu as encore mal à l\'oreille c\'est ça? 😭 quelqu\'un va te rendre !')">B. Je suis occupée je vais répondre plus tard</button>
                <button class="btn" onclick="showGameOver('Mais ekiee 😭... On fuit qui comme ça ?')">C. Euill je lance mon téléphone je fuis les hommes et leurs mensonges</button>
            </div>
        </div>

        <div class="screen" id="screen3">
            <div>
                <div class="poem-box" id="poem2"></div>
                <div class="question-text" id="q2-text" style="display:none;">PK sait que tu es timide et que tu ne marches pas sans ta Cecile... mais il prend son courage à 2 mains et t'invite seule...</div>
            </div>
            <div id="choices2" style="display:none; margin-bottom: 5px;">
                <button class="btn" onclick="showGameOver('😭 faut doser norh je devais faire comment')">A. Tu refuses ; trop tard ton anniversaire est passé qu'il aille en brousse</button>
                <button class="btn" onclick="showGameOver('😔 werrhh combat la timidité là norhh pardon')">B. Tu fuis parce que tu as pas envie de répondre tu es mal à l'aise</button>
                <button class="btn" onclick="validerEtape2()">C. Tu dis oui avec joie ça pouvait pas mieux tomber (ashh tu sais faire les bons choix 😉❤)</button>
            </div>
        </div>

        <div class="screen" id="screen4">
            <div>
                <div class="poem-box" id="poem3"></div>
                <div class="question-text">Si tu étais celle qui emmènerait une fleur comme toi dehors, que ferais-tu ?</div>
            </div>
            <div style="margin-bottom: 5px;">
                <button class="btn" onclick="saveProgramme('un ciné date 🎬')">A. Un ciné date (pas mal en soi mais... quel film 😭❤)</button>
                <button class="btn" onclick="saveProgramme('un restaurant en tête-à-tête 🍕')">B. Restaurant, belle ambiance nous deux et un peu d'effort (il a intérêt à réussir ! 😭)</button>
                <button class="btn" onclick="saveProgramme('un pique-nique romantique 🧺')">C. Pique-nique sous un beau temps (ash magnifique au pique-nique du cembas 😍❤)</button>
                <button class="btn" onclick="showAutreInput()">D. Autres...</button>
                <div id="autre-box" style="display:none;">
                    <input type="text" id="autre-texte" placeholder="Dis-moi ton programme idéal...">
                    <button class="btn btn-center" onclick="saveProgramme(document.getElementById('autre-texte').value)">Valider</button>
                </div>
            </div>
        </div>

        <div class="screen" id="screen5">
            <div>
                <div class="poem-box" id="poem4"></div>
                <div class="question-text">Quel jour le destin doit-il inscrire dans notre histoire ?</div>
            </div>
            <div style="margin-bottom: 15px;">
                <input type="date" id="jourInput">
                <button class="btn btn-center" onclick="saveJour()">Continuer ➡️</button>
            </div>
        </div>

        <div class="screen" id="screen6">
            <div>
                <div class="poem-box" id="poem5"></div>
                <div class="question-text">À quelle heure le temps devrait-il s'arrêter pour nous ?</div>
            </div>
            <div style="margin-bottom: 15px;">
                <input type="time" id="heureInput">
                <button class="btn btn-center" onclick="saveHeure()">Calculer l'alignement des étoiles ✨</button>
            </div>
        </div>

        <div class="screen" id="screen7">
            <div>
                <div class="poem-box" id="poemFinal"></div>
            </div>
            <div style="margin-bottom: 15px;">
                <button class="btn btn-center" onclick="sendWhatsApp()">Fin de l'histoire ❤️</button>
            </div>
        </div>

        <div class="popup-overlay" id="popup">
            <img class="popup-img" id="popup-img" src="" alt="Statut">
            <div class="poem-box" id="popup-text"></div>
            <button class="btn btn-center" id="popup-btn" style="display:none;">Continuer</button>
        </div>

    </div>
</div>

<script>
    let choixProgramme = "";
    let choixHeure = "";
    let choixJour = "";
    let grandPoeme = ""; 

    function typeWriterProgressive(baseText, newText, elementId, speed, callback) {
        const elem = document.getElementById(elementId);
        if (!elem) return;
        elem.innerHTML = baseText; 
        let i = 0;
        
        function type() {
            if (i < newText.length) {
                elem.innerHTML += newText.charAt(i);
                i++;
                setTimeout(type, speed);
            } else if (callback) {
                callback();
            }
        }
        type();
    }

    function startGame() {
        document.getElementById('bg-music').play().catch(e => console.log("Musique lancée."));
        document.getElementById('screen1').classList.remove('active');
        document.getElementById('screen2').classList.add('active');
        
        let introText = "Mais alors, comment réunir ces deux âmes solitaires égarées dans le tumulte du monde...\nImaginons, PK t'écrit...";
        typeWriterProgressive("", introText, "poem1", 35, function() {
            document.getElementById('q1-text').style.display = "block";
            document.getElementById('choices1').style.display = "block";
        });
    }

    function validerEtape1() {
        let nouveauxVers = "Dans le velours des nuits, ton souffle est un murmure,\nUn premier mot tremblant où le temps s'abandonne.\n";
        const popup = document.getElementById('popup');
        const btn = document.getElementById('popup-btn');
        document.getElementById('popup-img').src = "victoire.png";
        popup.style.display = "flex";
        btn.style.display = "none"; 
        
        typeWriterProgressive(grandPoeme, nouveauxVers, "popup-text", 35, function() {
            btn.style.display = "block"; 
        });
        grandPoeme += nouveauxVers;
        
        btn.innerText = "Continuer l'aventure";
        btn.onclick = function() {
            popup.style.display = "none";
            document.getElementById('screen2').classList.remove('active');
            document.getElementById('screen3').classList.add('active');
            document.getElementById('poem2').innerText = grandPoeme;
            document.getElementById('q2-text').style.display = "block";
            document.getElementById('choices2').style.display = "block";
        };
    }

    function validerEtape2() {
        let nouveauxVers = "Gwenaëlle, âme céleste où la grâce s'allume,\nLaisse nos pas tresser une invisible écume,\nTa douceur est l'abri où mon cœur se couronne.\n";
        const popup = document.getElementById('popup');
        const btn = document.getElementById('popup-btn');
        document.getElementById('popup-img').src = "victoire.png";
        popup.style.display = "flex";
        btn.style.display = "none";
        
        typeWriterProgressive(grandPoeme, nouveauxVers, "popup-text", 35, function() {
            btn.style.display = "block";
        });
        grandPoeme += nouveauxVers;
        
        btn.innerText = "Avancer vers le choix du décor";
        btn.onclick = function() {
            popup.style.display = "none";
            document.getElementById('screen3').classList.remove('active');
            document.getElementById('screen4').classList.add('active');
            document.getElementById('poem3').innerText = grandPoeme;
        };
    }

    function showAutreInput() {
        document.getElementById('autre-box').style.display = "block";
    }

    function saveProgramme(val) {
        if(!val) return;
        choixProgramme = val;
        let nouveauxVers = `Pour unique décor, tu as choisi : ${choixProgramme},\nDouce halte secrète où nos regards s'enflamment.\n`;
        
        document.getElementById('screen4').classList.remove('active');
        document.getElementById('screen5').classList.add('active');
        document.getElementById('game-container').classList.add('fond-fleurs');
        
        typeWriterProgressive(grandPoeme, nouveauxVers + "\n(Le destin attend son jour sacré... Choisis le jour)", "poem4", 35);
        grandPoeme += nouveauxVers;
    }

    function saveJour() {
        const rawDate = document.getElementById('jourInput').value;
        if(!rawDate) return;
        const d = new Date(rawDate);
        const jours = ['dimanche', 'lundi', 'mardi', 'mercredi', 'jeudi', 'vendredi', 'samedi'];
        const mois = ['janvier', 'février', 'mars', 'avril', 'mai', 'juin', 'juillet', 'août', 'septembre', 'octobre', 'novembre', 'décembre'];
        choixJour = `${jours[d.getDay()]} ${d.getDate()} ${mois[d.getMonth()]}`;
        let nouveauxVers = `En ce sacré ${choixJour}, laisse-toi m'éblouir,\n`;
        
        document.getElementById('screen5').classList.remove('active');
        document.getElementById('screen6').classList.add('active');
        
        typeWriterProgressive(grandPoeme, nouveauxVers + "\n(Le temps offre son absolu... Choisis ton heure)", "poem5", 35);
        grandPoeme += nouveauxVers;
    }

    function saveHeure() {
        choixHeure = document.getElementById('heureInput').value;
        if(!choixHeure) return;
        let nouveauxVers = `Et quand l'horloge offrira l'absolu de ${choixHeure},\nEt dans l'éternité, je volerai ton sourire.\n\n`;
        
        document.getElementById('screen6').classList.remove('active');
        document.getElementById('screen7').classList.add('active');
        
        let chuteFinale = nouveauxVers + 
                         "C'est ainsi que deux âmes se rencontrent, que les étoiles s'alignent et les cœurs s'emmêlent.\n" +
                         "Au plaisir de conclure cette histoire par : et ils sortirent ensemble et passèrent un merveilleux moment...";
        typeWriterProgressive(grandPoeme, chuteFinale, "poemFinal", 35);
    }

    function showGameOver(message) {
        const popup = document.getElementById('popup');
        const btn = document.getElementById('popup-btn');
        document.getElementById('popup-img').src = "game_over.gif"; 
        popup.style.display = "flex";
        btn.style.display = "block"; 
        document.getElementById('popup-text').innerText = "❌ GAME OVER\n\n" + message;
        btn.innerText = "Recommencer l'étape 🔄";
        btn.onclick = function() {
            popup.style.display = "none";
        };
    }

    function sendWhatsApp() {
        let message = `Je suis d'accord pour sortir avec toi, pourquoi pas un ${choixProgramme}, le ${choixJour} à ${choixHeure} ? 🥰`;
        let encoded = encodeURIComponent(message);
        window.location.href = `https://wa.me/237695189130?text=${encoded}`;
    }
</script>
</body>
</html>
