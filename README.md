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
